# 标准模型

模型就是代码里的类，一个类装一组字段。字段含义见 [property.md](./property.md)，这页只说有哪些类、每个类装什么。类都还没对过，先按怀疑算。

## Contract（怀疑）

一次读进内存的归位契约，七个字段各装一组：

- `verdict`：阈值与默认话术。
- `domain`：领域。
- `cell`：十八格。
- `transition`：降格规则。
- `question`：分辨句。
- `model`：本体。
- `axiom`：公理。

## Cell（怀疑）

一格：`name`、`label`、`path`、`family`、`cues`、`description`、`skeleton`、`grade`。

## Domain（怀疑）

一个领域仓：`name`、`label`、`cues`。

## Grade（怀疑）

一档可信度：`label`、`cues`、`fallback`。

## Transition（怀疑）

一条降格规则：`from`、`to`、`require_any`、`lack_any`、`reason`。

## Question（怀疑）

一对分辨句：`pair`、`ask`。

## Model（怀疑）

本体：`description`、`family`。一族是 `ModelFamily`，装 `name`、`question`、`description`、`axis`；一条轴是 `Axis`，装 `name`、`values`。

## Axiom（怀疑）

一条公理：`name`、`description`、`why`、`status`。

## Verdict（怀疑）

契约里的阈值：`min_margin`、`min_hits`、`min_domain_hits`、`max_paragraphs`、`stay`、`archive_cues`、`question_fallback`。

## Card（怀疑）

一张落位卡：`verdict`、`domain`、`domain_form`、`domain_reason`、`cell`、`grade`、`rule`、`question`、`candidates`、`reason`、`axioms`。

## Candidate（怀疑）

一个候选格：`name`、`label`、`score`。

输出去向是另一个 `Verdict`，取值 place、move、reject、undecided——与阈值那个同名，不同模块。

## 怎么读这页

类名就是字段的边界：字段只在类里出现，换个类就换一套字段。要加字段，先看它属于哪个类；同一个意思不许在两个类里各起一个名字。

属性、关系与公理见 [property.md](./property.md)、[relation.md](./relation.md)、[axioms.md](./axioms.md)。模型的错法与正法，见后者的判例。
