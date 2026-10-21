# 代码

## 定位

开发与运行环境的踩坑清单。每条写「现象 → 做法」，不写论证；同类问题再次出现时直接查做法。

## 来源

汇总自 pi 记忆池的 `tool-quirk` 186 条与 `failure` 87 条（合计 273 条、84,439 字符），逐条读过后归并为 78 条，按主题分入下列文件。只收没有仓内正本的通用坑；项目专属的列在文末的归仓清单。

## 目录

- [git.md](./git.md)：版本控制与子模块。
- [editing.md](./editing.md)：文件编辑工具与 shell。
- [build.md](./build.md)：Rust、Python 与包管理。
- [gui.md](./gui.md)：本机 GUI 与 Flutter。
- [external.md](./external.md)：外部工具、检索与数据。
- [discipline.md](./discipline.md)：协作纪律，从失败里长出来的，不是技术坑。
- [pi.md](./pi.md)：pi 运行时。

## 归仓清单

这些在池里也有条目，但内容只对某个仓成立，此处不收正文：`qtcloud-*` CLI 的内部实现与内存爆炸案例（quanttide-work / qtcloud-meta）、`pr4xis` / `lau-category-theory` 的 API 坑（quanttide-meta）、`qtconsult` 的 GoRouter 微任务风暴与 pumpAndSettle 不收敛（qtconsult）、OneBase-AI 的配置与 Dockerfile 覆盖链（一次性选型，已成结论）、`quanttide-feishu-lab` 的 runner 副作用缺口（quanttide-feishu）。它们该进各仓的 `docs/` 或 `AGENTS.md`，而不该长期待在记忆池里。

## 与记忆池的关系

池里 273 条（`tool-quirk` 186 + `failure` 87）在本目录有对应的，都可以从 `failures.md` 删掉，只留本目录作正本；归仓清单里那批要先搬进各仓再删。`correction` 115 条、`insight` 115 条、`convention` 50 条不是坑，归宿是 `data/profile/hermes/` 四份、技能与各仓 `AGENTS.md`。
