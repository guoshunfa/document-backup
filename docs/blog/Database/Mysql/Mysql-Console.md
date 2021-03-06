# Mysql 控制台使用说明

## 进入控制台

打开终端输入```mysql -uroot -p```，随后输入密码。

root可替换成其他用户名。

## 提示符信息

| 提示符                                            | 含义                                              |
| ------------------------------------------------- | ------------------------------------------------- |
| mysql>                                            | 准备好接受新的命令。                              |
| ->                                                | 等待多行的下一行，或等待以分号（;）结束。         |
| '>                                                | 等待多行的下一行，或等待以单引号（'）结束。       |
| ">                                                | 等待多行的下一行，或等待以双引号（"）结束。       |
| \`>	|等待多行的下一行，或等待以反斜点（\`）结束。 |
| /\*>                                              | 等待多行的下一行，或等待以注释终止符（\*/）结束。 |

## 客户端帮助
> 所有 MySQL 命令的列表：注意，所有文本命令必须在一行的开头，并且以分号“;”结束
> 
| 命令                     | 缩写 | 说明                                                                  | 示例                             |
| ------------------------ | ---- | --------------------------------------------------------------------- | -------------------------------- |
| ?                        | ?    | “help”的同义词。                                                      | mysql> ?                         |
| clear                    | c    | 清除当前输入的语句。一般用于多行命令。                                | mysql> c                         |
| connect                  | r    | 重新连接到服务器。可选参数是 db 和 host。连接 ID 将会改变。           | mysql> r                         |
| mysql> r [数据库] [主机] |
| delimiter                | d    | 设置语句定界符。默认为“;”。                                           | mysql> d 定界符                  |
| ego                      | G    | 发送命令到 MySQL 服务器，垂直显示结果。                               | mysql> SHOW DATABASESG           |
| exit                     | q    | 退出 MySQL。与 quit 相同。                                            | mysql> exit                      |
| go                       | g    | 发送命令到 MySQL 服务器。                                             | mysql> SELECT \`id\` FROM \`table\`g |
| help                     | h    | 显示该帮助信息。                                                      | mysql> h                         |
| notee                    | t    | 不要写到 outfile 中。                                                 | mysql> notee                     |
| print                    | p    | 打印当前命令。                                                        | mysql> SHOW TABLESp;             |
| prompt                   | R    | 改变你的 MySQL 提示符。                                               | mysql> prompt -->                |
| quit                     | q    | 退出 MySQL。                                                          | mysql> q                         |
| rehash                   | #    | 重建完整的 hash（用于自动完成名称）。                                 | mysql> #                         |
| source                   | .    | 执行一个 SQL 脚本文件。使用一个文件名作为参数。                       | mysql> source D:my.sql           |
| status                   | s    | 从服务器取得状态信息。                                                | mysql> status                    |
| tee                      | T    | 设置 outfile 为 [to_outfile]。向已给出的 outfile 文件中追加所有东西。 | mysql> tee E:store.txt           |
| use                      | u    | 使用另一个数据库。使用一个数据库名作为参数。                          | mysql> use 数据库                |
| charset                  | C    | 切换到其它字符集。可能需要使用多字节字符集来处理二进制日志。          | mysql> charset 字符集            |
| warnings                 | W    | 在每一个语句后面显示警告。                                            | mysql> W                         |
| nowarning                | w    | 不在每一个语句后面显示警告。                                          | mysql> w                         |
要获得服务器端的帮助信息，键入“help contents”