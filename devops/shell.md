# shell 与进程

- 命令里有裸反引号 → `寻找匹配的 \` 时遇到了未预期的 EOF`（exit 2）。含反引号的文本一律用单引号包裹或走 heredoc。
- `bash -c` 里塞重定向进 `for` 列表、写裸括号（含中文括号）→ 「未预期的记号」语法错误。重定向写在 `done` 之后或命令上，提示语避开裸括号。
- `pkill -f <pattern>` 会匹配到自己那条 `bash -c` → 把当前 shell 一起杀掉（exit 143，后续输出全丢）。杀自己起的进程用 `pkill -x <进程名>` 或先 `pgrep` 拿 PID 再 kill。
- cwd 常不是仓库根 → `cat Cargo.toml` 报 No such file，`find` 会扫进 `target/debug/incremental`。先确认目录或用绝对路径。
- `sed` 整文件批量替换极易把前缀插到每一行（实测把源文件全行污染、还造出怪名目录）→ 批量改代码一律逐文件精确替换；出错先 `git restore` 回被污染的文件，再手工重做，别用第二次 sed 修补。
