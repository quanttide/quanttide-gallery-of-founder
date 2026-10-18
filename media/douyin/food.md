# 抖音美食推荐视频

## 选题

一家泰式小馆的探店视频。现场只记下三段观察：

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

视频都在 iCloud 相册。用 icloudpd 同步到 `<素材目录>/videos`，加 `--skip-photos` 跳过照片；账号在中国区时加 `--domain cn`。

完整参数见手册的「视频素材」一篇。

### 转码

iPhone 的视频是 HEVC 编码，部分平台和剪辑软件不认。素材目录只留 MP4：

- MOV → MP4：用 ffmpeg 转 H.264，`-pix_fmt yuv420p`，音频转 AAC；
- Live Photo 的配对 MOV 转成 MP4 后放进视频目录；
- 转换成功后删除 MOV。

转码前用 `ffprobe` 查看 `color_transfer`：SDR（`bt709`）直接转；HDR（`arib-std-b67` 或 `smpte2084`）先做 tonemap，否则颜色会发灰。

## 正文
