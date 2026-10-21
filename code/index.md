# 代码

## 定位

代码树里的坑：编辑源码、语言与库、构建与测试、检索与数据。每条写「现象 → 做法」，不写论证。

## 分类标准

以代码树为界。修复落在源码、测试、构建配置或依赖声明上，归此；修复要动的是树外的状态——仓库历史、进程、已安装环境、外部服务、基础设施，归 [DevOps](../devops/index.md)。

按 `quanttide-code` 的定义，这条界线覆盖的是软件工程本身：语言怎么用、库怎么调、测试怎么写、代码怎么盯着改。

## 目录

- [editing.md](./editing.md)：文件编辑工具——逐字匹配、区域重叠与批量改写。
- [rust.md](./rust.md)：Rust 与 cargo——锁文件、重编、lint 与 API。
- [flutter.md](./flutter.md)：Flutter 测试与构建——真实 I/O 挂死与产物路径。
- [search.md](./search.md)：检索与数据——中文索引、增量污染、统计口径与命名。

## 来源

与 DevOps、智能体两份同出一源：`data/profile/pi/pitfalls.md` 的 78 条按领域拆分，本目录 24 条，DevOps 38 条，智能体 16 条。

## 归仓清单

这些在池里也有条目，但内容只对某个仓成立，此处不收正文：`qtcloud-*` CLI 的内部实现与内存爆炸案例（quanttide-work / qtcloud-meta）、`pr4xis` / `lau-category-theory` 的 API 坑（quanttide-meta）、`qtconsult` 的 GoRouter 微任务风暴与 pumpAndSettle 不收敛（qtconsult）、OneBase-AI 的配置与 Dockerfile 覆盖链（一次性选型，已成结论）、`quanttide-feishu-lab` 的 runner 副作用缺口（quanttide-feishu）。它们该进各仓的 `docs/` 或 `AGENTS.md`，而不该长期待在记忆池里。

## 与记忆池的关系

池里 273 条（`tool-quirk` 186 + `failure` 87）在本目录与兄弟目录有对应的，都可以从 `failures.md` 删掉，只留这里作正本；归仓清单里那批要先搬进各仓再删。`correction` 115 条、`insight` 115 条、`convention` 50 条不是坑，归宿是 `data/profile/hermes/` 四份、技能与各仓 `AGENTS.md`。
