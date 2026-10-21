# 外部工具与服务

- GitHub 没有「创建组织」的 API → REST/GraphQL/gh CLI 都做不到，只能在网页建。
- `gh search repos` 没有 stargazers 字段 → 查 stars / pushed_at / archived 用 `gh api repos/<owner>/<repo>`。
- `gh api …/contents/<path> -q .content | base64 -d` → 仓库或路径不存在时 gh 报 404，base64 随后连锁报 invalid input；第一个错误才是根因。
- crates.io API 必须带 User-Agent（curl 403），且返回结构是顶层不是 PyPI 那种 `{"crate": …}` 嵌套。
- `lark-cli`：`--as bot` 不能配 `--mailbox me`（须显式邮箱）；`--print-output-schema` 不存在；分页时 stdout 会混入 `[page N] fetching...` 进度行，子进程调用不能直接 `json.loads`；查技能用 `lark-cli skills list` / `skills read <path>`；取群消息两条路径（`+messages-search` 关键词与 `+chat-messages-list` 全量本地匹配）结果可能不一致，要取集合差再报数。
- `aliyun` CLI：很多产品是「插件可装但未安装」，未装时命令集不全；`domain` 产品没有询价接口，查价走 `bssopenapi QuerySkuPriceList`（参数是 `--CommodityCode/--PriceEntityCode`）。
- `snap saved --list` 不存在（unknown flag）→ 直接 `snap saved` 列出快照，`snap forget <组号>` 删。
- `docker pull` 的进度写在 containerd 存储（不在 `/var/lib/docker`），普通用户读不到；国内镜像对 `sickcodes/docker-osx` 一律拉不动，且它没有 `sonoma` 这类版本 tag（README 里的 Sonoma/Ventura 只是 SHORTNAME 示例）。
- Terraform 拉 alicloud provider 超时 → 走本地文件系统镜像（把 provider 解到 `~/.terraform.d/plugin-cache/…` 后用 `-plugin-dir`）。
- Dart/pub.dev 取数：`/api/packages/<name>` 只返回元数据、不含 README；要正文得下 `https://pub.dev/api/archives/<name>-<ver>.tar.gz` 解包（带 `+` 的版本号要原样带）。
- 服务「同步接口正常、异步接口全部挂起」（FastAPI/uvicorn 实证）→ 典型是事件循环被首个失败请求阻塞：先重启服务看是否自愈（最小动作），再进容器逐层查；别一上来改代码。
- `py-spy` 抓挂起的 Python 进程 → 目标进程在容器里就在容器里装（`docker exec <容器> pip install py-spy`），装在宿主机抓不到。
- MyST 的 tab 块：`{tab-set}` 与 `tab-item` 围栏必须成对闭合（层级不同），批量生成极易漏；写完跑围栏配对检查。README 这类直接在 GitHub 渲染的页面不放 MyST 标签。
- rdflib 的本地名（QName）不能含空格 → 含空格的条目名要么改成下划线并在档案侧统一，要么改用 `rdfs:label` 承载。
