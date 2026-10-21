# 文件编辑与 shell

## 文件编辑工具

- `cat` 读含中文的文件出现乱码（输出成 `M-cM-^@M-^A` 这类转义）→ 编码环境没设好，先确认 `LANG`/`LC_ALL` 是 UTF-8 再读，别当成文件损坏。
- `old_text` / `oldText` 必须与原文逐字一致（含空白、换行、全角半角）→ 凭记忆改写必报 `Could not find the exact text` / `No entry matched`；先读或 grep 拿原文再替换。片段过短会命中多处，报 `must be unique` / `Multiple entries matched`，加长到唯一，不要缩短试错。
- 报 `ENOENT: no such file or directory` 但文件明明在 → 先自查路径拼写（实测最常见的错是漏一段 `examples/`），路径修好再怀疑工具；确认路径无误才改用「读全文 + 整文件写入」绕过。
- 替换后标题粘到上一行行尾（`…能检查的东西。## 哲学阐述`）→ 换行写少了。改完 grep `^## ` 与代码围栏前后空行做结构复核。
- 删除类编辑写反成插入（README 目录表出现两行同一项）→ 每批编辑后 grep 目标行核对，删除方向最容易写反。
- 同一文件多处 `edit` 区域重叠报 `edits[1] and edits[0] overlap` → 合并成一次 edit，或划成互不相交的区域。
- python heredoc 批量改文档时三引号块内的全角冒号等与外部引号冲突 → 解析期 SyntaxError、整批未执行但后续测试照跑，容易误判完成。小批下发、每批锚点唯一、打印回执。

## shell

- 命令里有裸反引号 → `寻找匹配的 \` 时遇到了未预期的 EOF`（exit 2）。含反引号的文本一律用单引号包裹或走 heredoc。
- `bash -c` 里塞重定向进 `for` 列表、写裸括号（含中文括号）→ 「未预期的记号」语法错误。重定向写在 `done` 之后或命令上，提示语避开裸括号。
- `pkill -f <pattern>` 会匹配到自己那条 `bash -c` → 把当前 shell 一起杀掉（exit 143，后续输出全丢）。杀自己起的进程用 `pkill -x <进程名>` 或先 `pgrep` 拿 PID 再 kill。
- cwd 常不是仓库根 → `cat Cargo.toml` 报 No such file，`find` 会扫进 `target/debug/incremental`。先确认目录或用绝对路径。
- `sed` 整文件批量替换极易把前缀插到每一行（实测把源文件全行污染、还造出怪名目录）→ 批量改代码一律逐文件精确替换；出错先 `git restore` 回被污染的文件，再手工重做，别用第二次 sed 修补。
