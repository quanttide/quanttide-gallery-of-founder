# 导出 iCloud 照片

把 iCloud 相册里的照片与视频同步到工作站，转成通用格式，供后续加工与发布使用。一个 work 覆盖两条分支：图片走 JPG、视频走 MP4，共用同一套认证与目录约定。

适用于需要把拍摄素材集中到工作站、又不想逐台手动导出的场景。

## 前置

**认证**：已完成手册 `auth/icloud.md` 中的账号认证（`icloudpd` 安装与首次登录）。中国区账号所有请求必须带 `--domain cn`。

**目录**：素材目录固定为两个，各放一种格式，路径固定便于正文引用。

```
<素材目录>/images   只放 JPG
<素材目录>/videos   只放 MP4
```

同步后直接转码，不保留 HEIC 与 MOV 原格式；需要留原片时先另存。

## 步骤 1：查看相册

```bash
icloudpd --domain cn --username <Apple ID> --list-albums
```

不加 `--album` 时操作整个图库；只同步指定相册时加 `--album "相册名"`。

## 步骤 2：同步照片

照片单独执行，用 `--skip-videos` 跳过视频：

```bash
icloudpd --domain cn --username <Apple ID> \
  --directory <素材目录>/images \
  --skip-videos \
  --size original \
  --folder-structure none \
  --set-exif-datetime
```

## 步骤 3：同步视频

视频单独执行，用 `--skip-photos` 跳过图片：

```bash
icloudpd --domain cn --username <Apple ID> \
  --directory <素材目录>/videos \
  --skip-photos \
  --folder-structure none \
  --set-exif-datetime
```

正式执行前先用 `--recent 5 --dry-run` 试跑，确认选中的文件和落盘路径。

重复执行同一命令即增量同步，工具按文件名和大小识别已下载文件。

## 参数取舍

- `--size original`：拉原图，避免拿到 iCloud 优化存储的缩略图
- `--folder-structure none`：所有文件直接放在目标目录，路径固定，便于引用
- `--set-exif-datetime`：文件缺少 EXIF 拍摄时间时用创建时间补齐
- `--until-found N`：增量同步时，遇到 N 个已下载项即停止

## 步骤 4：HEIC 转 JPG

ImageMagick 缺少 HEIC 解码插件、ffmpeg 只能读到 HEIC 分块流时，用 pillow-heif：

```bash
uv run --no-project --with pillow-heif python - <<'PY'
from pathlib import Path
import io

from PIL import Image, ImageOps, ImageCms
import pillow_heif

pillow_heif.register_heif_opener()
for src in Path("<素材目录>/images").glob("*.HEIC"):
    im = Image.open(src)
    exif = im.getexif()
    im = ImageOps.exif_transpose(im)
    icc = im.info.get("icc_profile")
    if icc:
        im = ImageCms.profileToProfile(
            im,
            ImageCms.ImageCmsProfile(io.BytesIO(icc)),
            ImageCms.createProfile("sRGB"),
            outputMode="RGB",
        )
    exif[274] = 1
    im.convert("RGB").save(
        src.with_suffix(".jpg"),
        "JPEG",
        quality=92,
        optimize=True,
        exif=exif.tobytes(),
    )
    src.unlink()
PY
```

脚本把 Display P3 等内嵌配置转到 sRGB、保留 EXIF，并在成功后删除 HEIC。PNG 截图同样转为 JPG，扩展名统一用小写 `.jpg`。

## 步骤 5：MOV 转 MP4

iPhone 视频多为 HEVC 编码，转成 H.264 以便剪辑软件和平台直接使用：

```bash
ffmpeg -hide_banner -loglevel error -i input.MOV \
  -map 0:v:0 -map 0:a? \
  -c:v libx264 -preset medium -crf 20 -pix_fmt yuv420p \
  -c:a aac -b:a 192k -movflags +faststart \
  output.mp4
```

`videos/` 下的 MOV 原地转成 MP4。转码成功后删除 MOV。

转码前用 `ffprobe` 查看 `color_transfer`：SDR（`bt709`）直接转；HDR（`arib-std-b67` 或 `smpte2084`）需要先做 tonemap，否则颜色会发灰。

## 步骤 6：Live Photo 归位

Live Photo 会连同配对的 MOV 一起下载，这个 MOV 可能落在 `images/` 下。处理方式：按步骤 5 转成 MP4，转到 `videos/`。只需要静态图时，在同步照片那步加 `--skip-live-photos`。

## 收尾校验

1. `images/` 里不再有 `.HEIC` 或 `.MOV`，`videos/` 里不再有 `.MOV`
2. 两个目录的扩展名统一小写
3. 抽样打开转码后的 JPG 与 MP4，确认颜色不发灰、方向正确
4. 与相册条数对一遍，确认没有漏拉

## 常见偏差

- **退出码 0 不代表成功**。不报错但列不出相册、日志出现 `Apple iCloud setup is not complete`，通常是账号还没在网页端完成初始化：登录 iCloud 网页版接受条款，确认图库能打开后再试
- 首次请求返回 `421` 属于会话续期流程，随后会用保存的 session token 自动重新认证
- 登录响应的 `webservices` 为空：先检查网页端条款，仍为空则删除 `~/.pyicloud/` 重新认证
- 2FA 过期后需要重新交互认证，无法通过参数绕过
- 视频颜色发灰：HDR 片源没做 tonemap，回看 `color_transfer`
- 双重认证码一次性有效，不写入脚本或文档；会话文件权限 `600`

## 自动化

长期同步可用 cron 或 systemd timer 定时执行同一命令。`--watch-with-interval 3600` 可以常驻轮询，但进程退出后不会自行恢复，不适合无人值守。

## 本 work 不负责

选题、选图、文案与标签、发布——这些属于媒体的加工与发布环节，见手册 `media/index.md`。
