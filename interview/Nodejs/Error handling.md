# Error handling

## 如何处理未预料的出错

- callback(err, data) 回调约定
- throw / try / catch
- EventEmitter 的 error 事件

## Error-First Callback

只是一个约定,错误处理有限.

## uncaughtException

`uncaughtException` 是未经捕获的一场,可以使用`process.on('uncaughtException')` 来处理.