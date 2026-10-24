# pi 运行时

- `memory_replace` 是整条替换：多行记录的新内容必须带上旧记录首行以外的全部行，否则报 `Refusing replace`；`old_text` 要逐字且够长。
- `memory_search` 无命中时会回显当前全部记忆（输出极长），是工具行为不是故障。
- `STANDING.md` 的解析规则：每行非空且非 `#` 开头都算一条规则，说明文字只能写成 `#` 标题行。口径见 `data/profile/pi/runtime.md`。
