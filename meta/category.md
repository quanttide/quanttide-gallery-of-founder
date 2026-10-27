# 标准范畴

范畴是一个范式里的一个类目：它回答「这份内容属于哪一类」，凭的是成员条件——认哪些线索、不收什么、通常怎么写。十八格就是十八个范畴，分两族，各九格。两端不是格：context 是入口，archive 是出口，合起来二十种。

称呼、目录与界线照契约写。`meta category` 读契约，本页是给人看的镜像；两边对不上时跑 `qtfounder meta validate`。

## 陈述型

- 轴：时间（过去、现在、未来）
- 轴：类型（事件、语义、自我）

### report

- 称呼：Report 报告
- 目录：`data/report/`
- 收什么：这一轮已经结束，收的是履行完毕的契约。

### library

- 称呼：Library 图书馆
- 目录：`data/library/`
- 收什么：收的是外面的东西，不是自己的判断；出处必须写清。

### history

- 称呼：History 历史
- 目录：`data/history/`
- 收什么：说的是组织怎么走到今天，不是某一轮工作。

### journal

- 称呼：Journal 日志
- 目录：`data/journal/`
- 收什么：记得住日期和当事人；抽掉这些，这句话就空了。

### profile

- 称呼：Profile 档案
- 目录：`data/profile/`
- 收什么：跨事稳定，改起来要动整个人的判断方式，才是档案。

### brochure

- 称呼：Brochure 宣传册
- 目录：`data/brochure/`
- 收什么：写给外面的人看，讲的是「它是什么」，不是内部怎么想。

### roadmap

- 称呼：Roadmap 路线图
- 目录：`data/roadmap/`
- 收什么：回答「下一步干什么」，讲先后与取舍。只在解释为什么必须这样排、没有当前动作的，不是路线图。

### insight

- 称呼：Insight 洞察
- 目录：`data/insight/`
- 收什么：一句话能被推翻，推翻之后做法会变；抽掉日期和当事人还成立。

### intention

- 称呼：Intention 愿景
- 目录：`data/intention/`
- 收什么：收原话：「要 X，不要 Y」。提炼过的结论不是愿景。

## 程序型

- 轴：约束力（宪法、法律、法理）
- 轴：消费对象（人读、AI 解析、直接运行）

### bylaw

- 称呼：Bylaw 章程
- 目录：`docs/bylaw/`
- 收什么：涉及授权与权责划分，要人签字放行才生效。

### specification

- 称呼：Specification 工程标准
- 目录：`docs/specification/`
- 收什么：回答「必须满足什么」，每条能单独求值；概念入体系、阈值有数据。

### toolkit

- 称呼：Toolkit 标准库
- 目录：`packages/`
- 收什么：直接运行的代码资产，不是关于代码的说明。

### handbook

- 称呼：Handbook 手册
- 目录：`docs/handbook/`
- 收什么：收一类情况的判断尺子：换一个实例仍然成立。

### gallery

- 称呼：Gallery 案例
- 目录：`docs/gallery/`
- 收什么：收一次具体工作：时间、参与人、做法与结果；换一个实例就散架。

### platform

- 称呼：Platform 平台
- 目录：`apps/`
- 收什么：承载能力的产品本体，不是用法说明。

### tutorial

- 称呼：Tutorial 教程
- 目录：`docs/tutorial/`
- 收什么：带人从不会到会，一步一步走；讲原理的不是教程。

### essay

- 称呼：Essay 论文
- 目录：`docs/essay/`
- 收什么：讲原理与方法论，约束力最低；同一主题已有规格的，只写解释与例外。

### laboratory

- 称呼：Laboratory 实验室
- 目录：`examples/`
- 收什么：还没被验证的东西先在这里跑；验证通过就升进正式入口，实验室不留复制件，Skill 与文档只指向正式入口。

## 两端

两端不是格，是位置：context 记还没归好类，archive 记已经退出。两处都不判类型，上面的十八格才判。

### context

- 称呼：Context 入口
- 目录：`data/context/`
- 收什么：按「领域 / 资产」先放进来、还没通过整理校验的稿子；校验通过就搬去对应的长期记忆。

### archive

- 称呼：Archive 归档
- 目录：`data/archive/`
- 收什么：已经退出使用的内容，只移动不改写，留一份可追溯的底。

## 怎么用

- 判完一条，用 name 查这一页，确认它收的与卡上说的一致。
- 加一格之前，先看它落在哪条轴上（见 [model/index.md](./model/index.md)）；轴上报不出位置，就不是新范畴。
- 这一页只管收什么。写法与分档看 `asset contract`，迁移看 [relation.md](./relation.md)。

范畴的错法与正法，见 [axioms.md](./axioms.md) 的判例。
