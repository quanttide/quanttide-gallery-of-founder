# 本机 GUI 与 Flutter

- 截图（Ubuntu 26.04 + Wayland 会话）：ImageMagick `import -window root` / `import -window <id>` 报 `missing an image filename` 或 `X_GetImage BadMatch`；`ffmpeg -f x11grab` 报 Not yet implemented。可用路径是 Python + Xlib `XGetImage` 取像素再交 PIL，或整体降级为「不截图、只跑测试」。
- 文件大小正常 ≠ 截图成功 → `import` 有时静默失败但写出正常大小的文件；要读图看内容，或统计非黑像素数确认界面真的渲染了。
- 用 `xdotool` 给 Xwayland 下的 Flutter 窗口注入点击 → 能定位、能激活，事件送不到应用。动作链改由 widget/Bloc 层测试覆盖，截屏只用于确认渲染。
- `testWidgets` 里直接 await 真实文件 I/O → 整轮 `flutter test` 挂死（300s 超时）。注入内存假仓库，或用 `runAsync` 包真实异步。
- `flutter build linux` 产物 → `build/linux/x64/debug/bundle/<project_name>`，可执行名由 `--project-name` 决定。
