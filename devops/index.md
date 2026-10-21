# DevOps

## 定位

代码树之外的坑：仓库状态、依赖安装、命令与进程、运行环境、外部服务与基础设施。每条写「现象 → 做法」，不写论证。

## 分类标准

以代码树为界。修复要动的是 `.git` 里的历史与指针、已经装好的依赖、正在跑的进程、外部的服务与基础设施，归此；修复落在源码、测试、构建配置或依赖声明上，归 [代码](../code/index.md)。

按 `quanttide-devops` 的生命周期（规划→编码→构建→测试→发布→部署→运维→监控），这里收的是让代码树进入并运行于环境的那一段。它自带的纪律也解释了为什么这些坑集中在这里：DevOps 操作要通过工具闭环，不绕开工具手动执行，而工具的用法正是这些条目记下的事。

## 目录

- [git.md](./git.md)：版本控制与子模块——推送、改名、指针与锁文件。
- [shell.md](./shell.md)：shell 与进程——引号、重定向、误杀与路径。
- [python.md](./python.md)：Python 与包管理——PEP 668、uv 与国内镜像。
- [environment.md](./environment.md)：本机图形环境——Wayland 截图与窗口注入。
- [external.md](./external.md)：外部工具与服务——gh、lark-cli、docker、Terraform、MyST。

## 来源

与代码、智能体两份同出一源：`data/profile/pi/pitfalls.md` 的 78 条按领域拆分，本目录 38 条。归仓清单见 [code/index.md](../code/index.md) 的同名一节。
