# 导出 iCloud 照片

把 iCloud 相册里的照片与视频同步到工作站，转成通用格式，供后续加工与发布使用。一个 work 覆盖两条分支：图片走 JPG、视频走 MP4，共用同一套认证与目录约定。

适用于需要把拍摄素材集中到工作站、又不想逐台手动导出的场景。

本篇分两半：**命令与取舍**给人执行，**流程与判据**给执行器读。

## 首次认证（人做，一次性）

```bash
uv tool install icloudpd
icloudpd --domain cn --username <Apple ID> --auth-only
```

会话保存在 `~/.pyicloud/`，之后命令自动续期；2FA 过期后重新执行认证命令。双重认证码一次性有效，不写入脚本或文档。中国区账号所有请求必须带 `--domain cn`。

## 目录约定

```
<素材目录>/images   只放 JPG
<素材目录>/videos   只放 MP4
```

同步后直接转码，不保留 HEIC 与 MOV 原格式；需要留原片时先另存。

## 流程与判据

```yaml work
work: export-icloud-photo
标题: 导出 iCloud 照片
版本: 1

输入:
  账号: { 必填: true }
  素材目录: { 默认: ./素材 }
  相册: { 可选: true }
  试跑: { 类型: 布尔, 默认: false }

前置:
  - 检查: 会话有效
    参数: { 账号: "{{输入.账号}}" }
    不成立: 提示先完成认证，不继续

步骤:
  - id: 同步照片
    做: 从相册导出
    参数: { 账号: "{{输入.账号}}", 类型: 照片, 目录: "{{输入.素材目录}}/images", 相册: "{{输入.相册}}", 试跑: "{{输入.试跑}}" }
    判据: 退出码为 0
    幂等: 增量

  - id: 同步视频
    做: 从相册导出
    参数: { 账号: "{{输入.账号}}", 类型: 视频, 目录: "{{输入.素材目录}}/videos", 相册: "{{输入.相册}}", 试跑: "{{输入.试跑}}" }
    判据: 退出码为 0
    幂等: 增量

  - id: 照片转码
    做: 转为通用格式
    参数: { 类型: 照片, 目录: "{{输入.素材目录}}/images" }
    判据: "images: 无 *.HEIC 残留"

  - id: 视频转码
    做: 转为通用格式
    参数: { 类型: 视频, 目录: "{{输入.素材目录}}/videos", 附带来源: "{{输入.素材目录}}/images" }
    判据: "videos: 无 *.MOV 残留"

  - id: 确认颜色
    执行者: 人
    待办: 抽样打开转码后的视频，确认 HDR 片源未发灰

校验:
  - "images: 只含 *.jpg"
  - "videos: 只含 *.mp4"
  - "images: 数量与 相册条数 一致"

偏差:
  - 现象: 退出码 0 但列不出相册
    处置: 网页端接受条款后重试
  - 现象: 视频颜色发灰
    处置: 片源为 HDR，转码前需 tonemap
  - 现象: 登录响应 webservices 为空
    处置: 先检查网页端条款，仍为空则删除 ~/.pyicloud/ 重新认证

不做:
  - 选题、选图、文案与标签、发布
```

## 同步的实际命令

查看相册（判断用哪个 `--album`）：

```bash
icloudpd --domain cn --username <Apple ID> --list-albums
```

照片单独执行，用 `--skip-videos` 跳过视频：

```bash
icloudpd --domain cn --username <Apple ID> \
  --directory <素材目录>/images \
  --skip-videos \
  --size original \
  --folder-structure none \
  --set-exif-datetime
```

视频单独执行，用 `--skip-photos` 跳过图片：

```bash
icloudpd --domain cn --username <Apple ID> \
  --directory <素材目录>/videos \
  --skip-photos \
  --folder-structure none \
  --set-exif-datetime
```

正式执行前先用 `--recent 5 --dry-run` 试跑，确认选中的文件和落盘路径。重复执行同一命令即增量同步，工具按文件名和大小识别已下载文件。

参数取舍：

- `--size original`：拉原图，避免拿到 iCloud 优化存储的缩略图
- `--folder-structure none`：所有文件直接放在目标目录，路径固定，便于引用
- `--set-exif-datetime`：文件缺少 EXIF 拍摄时间时用创建时间补齐
- `--until-found N`：增量同步时，遇到 N 个已下载项即停止

## 转码的实际命令

### HEIC 转 JPG

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

### MOV 转 MP4

iPhone 视频多为 HEVC 编码，转成 H.264 以便剪辑软件和平台直接使用：

```bash
ffmpeg -hide_banner -loglevel error -i input.MOV \
  -map 0:v:0 -map 0:a? \
  -c:v libx264 -preset medium -crf 20 -pix_fmt yuv420p \
  -c:a aac -b:a 192k -movflags +faststart \
  output.mp4
```

`videos/` 下的 MOV 原地转成 MP4，转换成功后删除 MOV。

转码前用 `ffprobe` 查看 `color_transfer`：SDR（`bt709`）直接转；HDR（`arib-std-b67` 或 `smpte2084`）需要先做 tonemap，否则颜色会发灰。

Live Photo 会连同配对的 MOV 一起下载，这个 MOV 可能落在 `images/` 下：按上面同一命令转成 MP4 后移到 `videos/`。只需要静态图时，在同步照片那步加 `--skip-live-photos`。

## 自动化

长期同步可用 cron 或 systemd timer 定时执行同一命令。`--watch-with-interval 3600` 可以常驻轮询，但进程退出后不会自行恢复，不适合无人值守。
