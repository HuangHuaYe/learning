# Babel

Babel是js的语法转换器,把现代版本的js转化成低版本的js,并提供polyfill实现高版本的一些特性.

## 工作流程

1. 解析,将代码(字符串)解析成AST(抽象语法树)
2. 转换,将上一个的AST转换成旧版本js的抽象语法树
3. 生成,根据转换之后的AST生成代码(字符串)

## 解析(parser)

解析中主要的工作有:

- 词法分析:将代码分割成token流,就是**语法单元**组成的数组
- 语法分析:分析词法分析生成的token流,生成AST

### 词法分析

js中,下面的都属于语法单元:

- 数字：JavaScript 中的科学记数法以及普通数组都属于语法单元.
- 括号：『(』『)』只要出现,不管任何意义都算是语法单元
- 标识符：连续字符,常见的有变量,常量(例如: null true),关键字(if break)等等
- 运算符：+、-、*、/等等
- 当然还有注释,中括号等

比如下面的代码:
```js
const add = (a, b) => a + b
```
生成的token数组是这样的:
```js
[
  { type: "identifier", value: "const" },
  { type: "whitespace", value: " " },
  ...
]
```

### 语法分析

对生成的token流做一些语法上的分析,比如函数,箭头函数,运算符
