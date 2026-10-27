# 标准关系

关系是两类模型之间的边。代码里用带 `from`、`to` 一类字段的类表示，边上只存两端的 `name`，不存对象——名字改了，边就断。都还没对过，先按怀疑算。

## Transition（怀疑）

一条有向边：`from` 是起点，`to` 是终点。`require_any` 与 `lack_any` 决定什么时候连得上，`reason` 说明为什么连。先后不靠排列顺序，靠这两个条件。

## Question（怀疑）

一条无向边：`pair` 装两端的名字，`ask` 是把两者分开的那句问话。正着问、反着问是同一对。

## Edges（怀疑）

查某一端时把相邻的边收成三组：`outgoing` 从它出发，`incoming` 指向它，`questions` 与它成对。

## 不成边的

家族与目录是按字段分的组，不是模型之间的边；定域是内容离开本仓去领域仓，也不落进 from 与 to 这套类。分组看 `family`，目录看 `path` 的第一段，定域看正文里的领域词。

属性、模型与公理见 [property.md](./property.md)、[model.md](./model.md)、[axioms.md](./axioms.md)。关系的错法与正法，见后者的判例。
