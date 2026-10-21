# DevOps

## 定位

研发流程的自动化与形式化：让规划、编码、构建、测试、发布、部署、运维、监控八阶段里的每一步都能被工具自动、可重复、可审计地完成。每条写「现象 → 做法」，不写论证。

## 分类标准

DevOps 不产出业务价值，只产出确定性。因此判据不是「东西在哪」，而是「这条知识用来干什么」。

- 用来让某一步自动、可重复、可审计，归此。版本控制与仓库状态、构建与制品、依赖安装、命令与进程、运行环境、外部服务与基础设施。
- 用来判断产物本身对不对，归 [代码](../code/index.md)。语言、库与 API、算法、测试设计、源码编辑。

同一条链上也要分开：写断言与测试用例是代码；让测试能被自动执行、失败能被形式化判定是 DevOps。用 crate 的 API 是代码；锁文件、重编、lint 门禁、制品路径是 DevOps。

这一侧的知识注定琐碎：它不解释业务，只解释工具在什么条件下会不按预期工作，而工具闭环正是 DevOps 的纪律所在。

## 目录

- [git.md](./git.md)：版本控制与子模块——推送、改名、指针与锁文件。
- [build.md](./build.md)：构建与制品——锁文件、重编、lint 门禁与产物路径。
- [shell.md](./shell.md)：shell 与进程——引号、重定向、误杀与路径。
- [python.md](./python.md)：Python 与包管理——PEP 668、uv 与国内镜像。
- [environment.md](./environment.md)：本机图形环境——Wayland 截图与窗口注入。
- [external.md](./external.md)：外部工具与服务——gh、lark-cli、docker、Terraform、MyST。

## 来源

与代码、智能体两份同出一源：`data/profile/pi/pitfalls.md` 的 78 条按领域拆分，本目录 46 条。归仓清单见 [code/index.md](../code/index.md) 的同名一节。
