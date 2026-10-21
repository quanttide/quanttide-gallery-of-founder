# DevOps

## 定位

把代码交付并跑起来的坑：版本控制与仓库、安装与环境、命令与进程、外部服务与基础设施。每条写「现象 → 做法」，不写论证。

## 分类标准

与 [代码](../code/index.md) 的分界是「失败要改哪一头」：改仓库、命令、进程、安装环境、外部服务或基础设施，归此；改源码、依赖声明、构建配置或测试，归代码。

按 `quanttide-devops` 的生命周期（规划→编码→构建→测试→发布→部署→运维→监控），这里收的是编码之后仍在起作用的那部分：东西送不出去、环境起不来、命令杀错进程、外部服务调不通。

## 目录

- [git.md](./git.md)：版本控制与子模块——推送、改名、指针与锁文件。
- [shell.md](./shell.md)：shell 与进程——引号、重定向、误杀与批量替换。
- [python.md](./python.md)：Python 与包管理——PEP 668、uv 与国内镜像。
- [gui.md](./gui.md)：本机 GUI 与 Flutter——截图、注入与测试挂死。
- [external.md](./external.md)：外部工具与服务——gh、lark-cli、docker、Terraform 与 MyST。

## 来源

与代码、智能体两份同出一源：`data/profile/pi/pitfalls.md` 的 78 条按领域拆分，本目录 42 条。归仓清单见 [code/index.md](../code/index.md) 的同名一节。
