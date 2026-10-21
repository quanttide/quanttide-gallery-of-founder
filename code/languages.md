# 语言与测试写法

- 测试函数名可以中文，但不能含裸阿拉伯数字（`fn 走向停在第 4 步()` 被解析成参数列表）→ 写「第四步」或用下划线。
- crate 的 API 不要凭记忆写 → 以 `.crate` 源码（`~/.cargo/registry/src/…`）为准；实测 tantivy 0.26 的 `doc!` 宏在 crate 根不在 `schema`、`Index` 无 `create_or_open`，凭记忆写会连错好几轮。
- `testWidgets` 里直接 await 真实文件 I/O → 整轮 `flutter test` 挂死（300s 超时）。注入内存假仓库，或用 `runAsync` 包真实异步。
