# 资产维护

资产维护的共同做法。边界与写法看 `asset contract`，在不在看 `asset catalog`。

本页是归位契约 `[maintain]` 段的镜像；两边对不上时以契约为准。

## 一、目录

内容只放在契约给的 path；同一份内容不跨类复制。

## 二、索引

新增内容同步 README 或 index.md，入口不留空。

## 三、变更记录

CHANGELOG 分新增、变更与移除；未发布段攒批，发布时定版。

## 四、版本

semver；标签与 CHANGELOG 段同名，已发布的段不回改。

## 五、发布

先推资产仓，再回主仓更新子模块指针，指针提交写清版本。

## 六、提交

Conventional Commits；迁移时源侧与目标侧各自提交。

## 七、迁移

归档只移动不改写；移交按目标侧体例改写。

## 八、闸门

提交前跑 language、docs 与 write；旧文本被拦不顺手改写。

## 九、只读

contract、catalog、relation 与 maintain 都不改文件。
