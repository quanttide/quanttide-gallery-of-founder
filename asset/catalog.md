# 资产清单

清单回答一件事：一类内容在这套仓库里叫什么、住在哪、处在前两段的哪一层。结构怎么走见 [relation.md](./relation.md)，怎么搬见 [maintain.md](./maintain.md)。

## 一条资产要说清的事

- 名字：机器可读，小写单词，与路径互相印证。
- 中文名：给人看，出现在索引和标题里。
- 角色：入口、常驻、出口，三选一。
- 路径：这一类唯一的存放位置，不在别处再开一份。
- 布局：前两段是领域在前，还是资产在前。

名字与路径是一一对应的，改路径就要改名字旁边的那一行，不能只改一处。

## 三种角色

入口只有 context，出口只有 archive，中间十八类是常驻。判断一个目录算不算资产，先看它是不是这二十种之一，不看它有没有内容。

## 二十种

| 名字 | 中文名 | 路径 | 角色 | 布局 |
|------|--------|------|------|------|
| context | Context 入口 | `data/context/` | 入口 | 领域 / 资产 |
| archive | Archive 归档 | `data/archive/` | 出口 | 领域 / 资产 |
| report | Report 报告 | `data/report/` | 常驻 | 资产 / 领域 |
| library | Library 图书馆 | `data/library/` | 常驻 | 资产 / 领域 |
| history | History 历史 | `data/history/` | 常驻 | 资产 / 领域 |
| journal | Journal 日志 | `data/journal/` | 常驻 | 资产 / 领域 |
| profile | Profile 档案 | `data/profile/` | 常驻 | 资产 / 领域 |
| brochure | Brochure 宣传册 | `data/brochure/` | 常驻 | 资产 / 领域 |
| roadmap | Roadmap 路线图 | `data/roadmap/` | 常驻 | 资产 / 领域 |
| insight | Insight 洞察 | `data/insight/` | 常驻 | 资产 / 领域 |
| intention | Intention 愿景 | `data/intention/` | 常驻 | 资产 / 领域 |
| bylaw | Bylaw 章程 | `docs/bylaw/` | 常驻 | 资产 / 领域 |
| specification | Specification 工程标准 | `docs/specification/` | 常驻 | 资产 / 领域 |
| toolkit | Toolkit 标准库 | `packages/quanttide-founder-toolkit/` | 常驻 | 资产 / 领域 |
| handbook | Handbook 手册 | `docs/handbook/` | 常驻 | 资产 / 领域 |
| gallery | Gallery 案例 | `docs/gallery/` | 常驻 | 资产 / 领域 |
| platform | Platform 平台 | `apps/qtfounder/` | 常驻 | 资产 / 领域 |
| tutorial | Tutorial 教程 | `docs/tutorial/` | 常驻 | 资产 / 领域 |
| essay | Essay 论文 | `docs/essay/` | 常驻 | 资产 / 领域 |
| laboratory | Laboratory 实验室 | `examples/quanttide-founder-lab/` | 常驻 | 资产 / 领域 |

路径写的是仓库内位置，不是父目录。`docs/` 下有六类，`data/` 下有九类，说「在 docs 里」等于没说。

## 清单不做的

- 不判断一条内容该去哪一类，那是二次整理时的事。
- 不判断两类之间怎么搬，那是关系。
- 只看路径在不在，不看内容写得对不对。
- 缺一类不算错，只说明这一类还没开始。
