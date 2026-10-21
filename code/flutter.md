# Flutter 测试与构建

- `testWidgets` 里直接 await 真实文件 I/O → 整轮 `flutter test` 挂死（300s 超时）。注入内存假仓库，或用 `runAsync` 包真实异步。
- `flutter build linux` 产物 → `build/linux/x64/debug/bundle/<project_name>`，可执行名由 `--project-name` 决定。
