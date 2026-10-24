# 代码

## 定位

产物本身对不对：语言与库怎么用、算法怎么保证结果、测试怎么写、源码怎么改。每条写「现象 → 做法」，不写论证。

## 分类标准

分界不在文件在哪个目录，而在知识用来回答哪个问题。

- 用来判断「产物对不对」，归此。语言语义、库与 API、算法正确性、测试设计、源码编辑。
- 用来让研发流程的某一步自动、可重复、可审计，归 [DevOps](../devops/index.md)。DevOps 是围绕规划、编码、构建、测试、发布、部署、运维、监控八阶段的自动化方法论，不产出业务价值，只产出确定性。

同一条链上也要分开：写断言与测试用例是代码；让测试能被自动执行、失败能被形式化判断是 DevOps。用 crate 的 API 是代码；锁文件、重编、lint 门禁、制品路径是 DevOps。

## 目录

- [editing.md](./editing.md)：文件编辑工具——逐字匹配、区域重叠与批量改写。
- [languages.md](./languages.md)：语言与测试写法——API 以源码为准，测试不碰真实 I/O。
- [search.md](./search.md)：检索与数据——中文索引、增量污染、统计口径与命名。

## 来源

与 DevOps、智能体两份同出一源：`data/profile/pi/pitfalls.md` 的 78 条按领域拆分，本目录 16 条，DevOps 46 条，智能体 16 条。

## 归仓清单

这些在池里也有条目，但内容只对某个仓成立，此处不收正文：`qtcloud-*` CLI 的内部实现与内存爆炸案例（quanttide-work / qtcloud-meta）、`pr4xis` / `lau-category-theory` 的 API 坑（quanttide-meta）、`qtconsult` 的 GoRouter 微任务风暴与 pumpAndSettle 不收敛（qtconsult）、OneBase-AI 的配置与 Dockerfile 覆盖链（一次性选型，已成结论）、`quanttide-feishu-lab` 的 runner 副作用缺口（quanttide-feishu）。它们该进各仓的 `docs/` 或 `AGENTS.md`，而不该长期待在记忆池里。

## 与记忆池的关系

池里 273 条（`tool-quirk` 186 + `failure` 87）在本目录与兄弟目录有对应的，都可以从 `failures.md` 删掉，只留这里作正本；归仓清单里那批要先搬进各仓再删。`correction` 115 条、`insight` 115 条、`convention` 50 条不是坑，归宿是 `data/profile/hermes/` 四份、技能与各仓 `AGENTS.md`。
