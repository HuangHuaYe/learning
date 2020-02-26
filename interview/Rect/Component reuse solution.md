# Component reuse solution

## 组件复用

- HOC

    一个接受一个组件然后返回另一个组件的组件.

- render props

    接受一个render函数作为`props` 可以父组件可以直接调用,并使用它的state.

- react hooks

    函数式生命组件的方式

mixin、hoc、render props、react-hooks的优劣如何？

Mixin的缺陷：

组件与 Mixin 之间存在隐式依赖（Mixin 经常依赖组件的特定方法，但在定义组件时并不知道这种依赖关系）

多个 Mixin 之间可能产生冲突（比如定义了相同的state字段）

Mixin 倾向于增加更多状态，这降低了应用的可预测性（The more state in your application, the harder it is to reason about it.），导致复杂度剧增

隐式依赖导致依赖关系不透明，维护成本和理解成本迅速攀升：

- 难以快速理解组件行为，需要全盘了解所有依赖 Mixin 的扩展行为，及其之间的相互影响
- 组价自身的方法和state字段不敢轻易删改，因为难以确定有没有 Mixin 依赖它
- Mixin 也难以维护，因为 Mixin 逻辑最后会被打平合并到一起，很难搞清楚一个 Mixin 的输入输出

**HOC相比Mixin的优势:**

HOC通过外层组件通过 Props 影响内层组件的状态，而不是直接改变其 State不存在冲突和互相干扰,这就降低了耦合度

不同于 Mixin 的打平+合并，HOC 具有天然的层级结构（组件树结构），这又降低了复杂度

**HOC的缺陷:**

扩展性限制: HOC 无法从外部访问子组件的 State因此无法通过shouldComponentUpdate滤掉不必要的更新,React 在支持 ES6 Class 之后提供了React.PureComponent来解决这个问题

Ref 传递问题: Ref 被隔断,后来的React.forwardRef 来解决这个问题

Wrapper Hell: HOC可能出现多层包裹组件的情况,多层抽象同样增加了复杂度和理解成本

命名冲突: 如果高阶组件多次嵌套,没有使用命名空间的话会产生冲突,然后覆盖老属性

不可见性: HOC相当于在原有组件外层再包装一个组件,你压根不知道外层的包装是啥,对于你是黑盒

**Render Props优点:**

上述HOC的缺点Render Props都可以解决

**Render Props缺陷:**

使用繁琐: HOC使用只需要借助装饰器语法通常一行代码就可以进行复用,Render Props无法做到如此简单

嵌套过深: Render Props虽然摆脱了组件多层嵌套的问题,但是转化为了函数回调的嵌套

**React Hooks优点:**

简洁: React Hooks解决了HOC和Render Props的嵌套问题,更加简洁

解耦: React Hooks可以更方便地把 UI 和状态分离,做到更彻底的解耦

组合: Hooks 中可以引用另外的 Hooks形成新的Hooks,组合变化万千

函数友好: React Hooks为函数组件而生,从而解决了类组件的几大问题:

- this 指向容易错误
- 分割在不同声明周期中的逻辑使得代码难以理解和维护
- 代码复用成本高（高阶组件容易使代码量剧增）

**React Hooks缺陷:**

额外的学习成本（Functional Component 与 Class Component 之间的困惑）

写法上有限制（不能出现在条件、循环中），并且写法限制增加了重构成本

破坏了PureComponent、React.memo浅比较的性能优化效果（为了取最新的props和state，每次render()都要重新创建事件处函数）

在闭包场景可能会引用到旧的state、props值

内部实现上不直观（依赖一份可变的全局状态，不再那么“纯”）

React.memo并不能完全替代shouldComponentUpdate（因为拿不到 state change，只针对 props change）