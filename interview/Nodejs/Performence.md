# Performence

## CPU profiling

    node --prof app.js

上面的命令会生成报告,通过下面的命令可以对报告进行查看.

    node --prof-process isolate-0xnnnnnnnnnnnn-v8.log