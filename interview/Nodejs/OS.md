# OS

## TTY

TTY差不多是终端的意思,node中可以通过stdio的isTTY变量来判断是否是TTY环境.

## EOL换行符

UNIX,Linux中使用LR(\n)

CR+LF 微软家族,非Unix系统使用(\r\n)

## 负载

Nodejs进程中可以使用`os.loadavg()`来查看当前负载情况.或者可以使用`pidusage`来查看.