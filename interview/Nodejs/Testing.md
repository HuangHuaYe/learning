# Testing

## 为什么要写测试

项目在多人合作的时候, 为了某个功能修改了某个模块的某部分代码, 实际的情况中修改一个地方可能会影响到别人开发的多个功能, 在自己不知情的情况下想要保证自己修改的代码不影响到其他功能, 最简单的办法是通过测试来保证.

## 测试方法

### 黑盒测试

测试应用程序的功能, 而不是其内部结构或运作. 测试者不需了解代码、内部结构等, 只需知道什么是应用应该做的事, 即当键入特定的输入, 可得到一定的输出. 测试者通过选择有效输入和无效输入来验证是否正确的输出.

### 白盒测试

在白盒测试时, 以编程语言的角度来设计测试案例. 白盒测试可以应用于单元测试 (Unit Testing)、集成测试 (Integration Testing) 和系统的软件测试流程, 可测试在集成过程中每一单元之间的路径, 或者主系统跟子系统中的测试.

### 单元测试

单元测试 (Unit Testing) 是白盒测试的一种, 用于针对程序模块进行正确性检验的测试工作. 单元 (Unit) 是指最小可测试的部件.

## 覆盖率

测试覆盖率 (Test Coverage) 是指代码中各项逻辑被测试覆盖到的比率, 比如 90% 的覆盖率, 是指代码中 90% 的情况都被测试覆盖到了.

- 行覆盖率 (line coverage) 是否每一行都执行了？
- 函数覆盖率 (function coverage) 是否每个函数都调用了？
- 分支覆盖率 (branch coverage) 是否每个if代码块都执行了？
- 语句覆盖率 (statement coverage) 是否每个语句都执行了？

## 集成测试

集成测试也称综合测试、组装测试、联合测试, 将程序**模块采用适当的集成策略组装起来, 对系统的接口及集成后的功能**进行正确性检测的测试工作. 集成测试可以是黑盒的, 也可以是白盒的, 其主要目的是检查软件单位之间的接口是否正确, 而集成测试的对象是**已经经过单元测试的模块**.