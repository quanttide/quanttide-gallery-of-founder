# 构建与依赖

## Rust 与 cargo

- `cargo … --locked` 在 `Cargo.lock` 尚未生成时报 `cannot create the lock file … because --locked was passed` → 新建或改过包名后先不带 `--locked` 跑一次生成锁文件，再回门禁。
- `cargo` 要在含 `Cargo.toml` 的目录跑 → `qtcloud-*` 多组件仓的 `Cargo.toml` 在 `src/cli/`，在仓库根跑报 `could not find Cargo.toml`。
- 写完文件 cargo 仍报 `Fresh`，旧测试二进制「全部通过」→ 源 mtime 变了但没重编，极具误导性。`cargo clean -p <pkg>` 后重跑；改动后测试「秒过」就要怀疑。
- 给 `pub mod` 手写 `///` 注释 → 会破坏该模块 `//!` 里 `[`Step`]` 这类 in-scope 链接（rustdoc unresolved link）。模块级 `//!` 已经是文档，别加。
- 测试函数名可以中文，但不能含裸阿拉伯数字（`fn 走向停在第 4 步()` 被解析成参数列表）→ 写「第四步」或用下划线。
- `cargo clippy -D warnings` 的常见拦点：`ok_expect`（`.ok().expect()`）、`enum_variant_names`（变体名与枚举名重复）、`ptr_arg`（`&mut String` 参数，宏生成的用 `#[allow]` 挂在方法上）。
- `env!("CARGO_MANIFEST_DIR")` 定位数据文件 → 从 crates.io 装出的二进制里没有源码树，运行时报 No such file；要随包走就用 `include_str!` 编进二进制。
- 改 `Cargo.toml` 元数据（edition、版本、包名）后 → 全仓 grep 旧值，文档与 dev-guide 常留着旧号码。
- crate 的 API 不要凭记忆写 → 以 `.crate` 源码（`~/.cargo/registry/src/…`）为准；实测 tantivy 0.26 的 `doc!` 宏在 crate 根不在 `schema`、`Index` 无 `create_or_open`，凭记忆写会连错好几轮。

## Python 与包管理

- `pip install` 被 PEP 668 拦（externally-managed-environment）→ 用 `uv`：`uv pip install` 到临时 venv、或 `uv run --with <pkg> python3 <script>`，本机实测可行。
- PyPI 镜像实测：腾讯云 `mirrors.cloud.tencent.com/pypi/simple` 可用；阿里云偶发缺包 metadata（`pydantic_core` 404，uv 反复重试卡死）、清华 tuna 403 整体拒访、中科大 USTC 404。卡住先看错误里给出的 index URL 再换源。
- 安装命令长时间无输出、300s 超时 → 通常是镜像在反复重试 404/403，不是网络慢。中断看错误、换源；长安装拆步骤或后台跑，别原地重跑（会重复下载，永远跑不完）。
