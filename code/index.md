# 代码

## 定位

写对代码所需的坑：语言与库、构建配置、测试写法、编辑与检索源码。每条写「现象 → 做法」，不写论证。

## 分类标准

与 [DevOps](../devops/index.md) 的分界是「失败要改哪一头」：改源码、依赖声明、构建配置或测试，归此；改仓库、命令、进程、安装环境或外部服务，归 DevOps。

同一条边界也适用于构建与测试：改 lock、改 lint 规则、改代码，归此；换镜像、换安装命令、调环境，归 DevOps。

## 目录

- [editing.md](./editing.md)：文件编辑工具——逐字匹配、区域重叠与批量改写。
- [rust.md](./rust.md)：Rust 与 cargo——锁文件、重编、lint 与 API。
- [search.md](./search.md)：检索与数据——中文索引、增量污染与统计口径。

## 来源

与 DevOps、智能体两份同出一源：`data/profile/pi/pitfalls.md` 的 78 条按领域拆分，本目录 20 条，DevOps 42 条，智能体 16 条。

## 归仓清单

这些在池里也有条目，但内容只对某个仓成立，此处不收正文：`qtcloud-*` CLI 的内部实现与内存爆炸案例（quanttide-work / qtcloud-meta）、`pr4xis` / `lau-category-theory` 的 API 坑（quanttide-meta）、`qtconsult` 的 GoRouter 微任务风暴与 pumpAndSettle 不收敛（qtconsult）、OneBase-AI 的配置与 Dockerfile 覆盖链（一次性选型，已成结论）、`quanttide-feishu-lab` 的 runner 副作用缺口（quanttide-feishu）。它们该进各仓的 `docs/` 或 `AGENTS.md`，而不该长期待在记忆池里。

## 与记忆池的关系

池里 273 条（`tool-quirk` 186 + `failure` 87）在本目录与兄弟目录有对应的，都可以从 `failures.md` 删掉，只留这里作正本；归仓清单里那批要先搬进各仓再删。`correction` 115 条、`insight` 115 条、`convention` 50 条不是坑，归宿是 `data/profile/hermes/` 四份、技能与各仓 `AGENTS.md`。
