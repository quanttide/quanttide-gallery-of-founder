# 归位

## 定位

一份内容该放哪：先定域，再定格，再过准入，最后给写法。这一节收归位时不再论证的前提——每条都压着一类反复出现的错，错的代价写在同一行里。

前提与规则分开。规则写在 `apps/qtfounder/src/cli/src/meta/default-contract.toml` 的 `[[cell]]`、`[[transition]]` 与 `[[question]]` 里，参与算分；前提不参与算分，只在落位卡上点名出处。改规则改契约，改前提要先说服人。

## 目录

- [axioms.md](./axioms.md)：公理清单——九条前提与各自的代价，验过的标确认，没验的标怀疑。判例按现象、错法、正法写在管的公理下面。
- [property.md](./property.md)：标准属性——id、name、label、key、path、family、status 与内容、关系字段各是什么。

## 卡上点哪几条

落位卡只点名这次真用到的，不摊全表：

- 每张卡：`domain-before-cell`
- 指了域：`text-only`、`archive-vs-transfer`
- 收了（落位或搬走）：`one-place`、`template-scope`
- 不收：`no-fit`

对不上时先看这一行，再决定改哪里：前提不成立改契约，前提成立而卡错，是规则或执行的问题。

## 怎么用

- 评审里直接写名字，不重述原话：「这里违反 `no-fallback`」比复述一段省字，也不会每次复述都变形。
- 判错先分层：前提错改 `[[axiom]]`，相邻格分不开改 `[[question]]`，执行错改人、改提示词。三层混着改，本体就一点点漂走。
- 一条前提如果天天被引用，说明它其实该是一条规则，下沉到 `[[transition]]` 或代码检查。
