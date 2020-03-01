# Design Pattern

- 工厂模式
  创造对象的时候不对使用者暴露创造逻辑,使用者只需要知道什么产品就行.
- 抽象工厂模式
  抽象工厂是生产其他工厂的超级工厂.对生产产品的工厂进行约束.
- 单例模式
  一个类只有一个对象生产.
- 建造者模式
  Builder,传入多个对象,然后一步步生产一个浮渣的对象.
- 观察者模式
  一个对象修改后,通知其所有依赖关系对象被修改了.也称为订阅者模式.
- MVC
  视图-控制器-模型,更改数据模型的时候,控制器根据控制模型修改view.
  1. 控制器负责管理视图和模型
  2. 视图负责显示模型的内容
- MVP
  视图-模型-呈现者,MVC的变种.主要跟MVC的区别是,视图与模型并不交互,完全不知道彼此的存在.
- MVVM
  模型-视图-视图层.视图层是不断地同步视图和模型的更改.