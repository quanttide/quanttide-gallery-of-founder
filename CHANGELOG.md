# CHANGELOG

所有显著变更都将记录在此文件中。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)。

版本遵循语义化版本规范：0.0.x（探索期）→ 0.x.y（验证期）→ x.y.z（正式期）

---

## [Unreleased]

### 变更

- `work/export-icloud-photo.md`：按《work 语法》规格改写——散文管命令与取舍，块管步骤、判据、偏差与边界；收尾校验与常见偏差合并进块

### 新增

- `work/background-api-implementation.md`：后台实现任务的派单——从一条发给 Hermes、转给 Pi 的短指令整理出对象、任务、交付、合格线四项，并列接口契约缺失、覆盖率无阈值、回传与验收未记录四处缺口，给出五条可复用的派单模板
- `work/export-icloud-photo.md`：从 iCloud 相册导出照片与视频的工作流（认证前置、目录约定、照片/视频两条同步分支、HEIC→JPG 与 MOV→MP4 转码、Live Photo 归位、收尾校验与常见偏差），自手册的素材两篇合并迁入，来源侧不留副本；工作域在本仓重开
- 初始化案例集仓库：`README.md`（定位与同域分工）、`index.md`（入口，待补充）、`myst.yml`
- 新增 `media/` 目录：美食图文（`media/food.md`）

### 变更

- `media/food.md`：补全素材过程（同步、转码）与正文，店名与地址脱敏
- `media/food.md`：按探店方案修正选题定位，补入选图排序、封面、标题、文案、标签与待补清单
- `media/food.md`：补入滁州吾悦广场地址、人均与套餐价格、排队与停车信息
- `media/food.md`：画面无人出镜，按正常吃饭的口吻写，不标注合作角色
- `media/food.md`：补充店内多为 2–4 人、三四个人五六个菜的体验建议
- `media/food.md`：补全六道菜口感与茶饮温度，移除待补清单
- `media/food.md`：标题与说明改为图文，同一篇图文发在小红书和抖音
- `media/food.md`：补充平台标签上限与抖音只写后 4 个标签的策略
- `media/food.md`：补充 icloudpd 与 WorkBuddy 的工具说明，加工下的文案流程单独成节
- `media/douyin/food.md`：删除；平台拆分取消，案例合并到 `media/food.md`
- `work/rename.md`、`work/index.md`：迁出至 `quanttide-gallery-of-github-platform` 的 `second-brain/rename-files.md`，工作域在本仓清空
