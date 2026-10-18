# 小红书美食推荐贴

## 选题

一家泰式小馆的探店笔记。现场只记下三段观察：

```markdown
## 环境

暖黄的灯光，精致的装修。

## 人员

绿色的工作服，三四个人。

## 菜品

特色是泰式饭和鸡爪。鸡爪是自己改良的。
```

## 素材过程

### 同步

照片都在 iCloud 相册。用 icloudpd 同步到 `<素材目录>/images`，加 `--skip-videos` 跳过视频；用 `--size original` 拉原图，避免拿到 iCloud 优化存储的缩略图。账号在中国区时加 `--domain cn`。

完整参数见手册的「照片素材」一篇。

### 转码

iPhone 的原格式是 HEIC 和 HEVC，部分平台和剪辑软件不认。素材目录只留 JPG 和 MP4：

- HEIC → JPG：用 pillow-heif 转换，Display P3 等内嵌配置转到 sRGB，保留 EXIF；
- MOV → MP4：用 ffmpeg 转 H.264，`-pix_fmt yuv420p`，音频转 AAC；
- Live Photo 的配对 MOV 转成 MP4 后放进视频目录；
- 转换成功后删除 HEIC 和 MOV。

先统一格式，后续使用时就不用再考虑平台兼容。

## 正文
