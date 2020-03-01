# Flutter

## Dart 部分

### mixin extends implements

- extends,继承.跟传统的面向对象的继承,dart是单继承语言.
- implements,在dart继承接口和抽象类,但是需要重写类或者抽象类的所有方法,可以继承多个.
- mixin,因为在dart中没有接口,只有抽象类和类,而抽象类的方法可以由具体实现,使用mixin来继承就是可以直接继承了具体方法的实现.

mixin的with的时候遵循覆盖原则,而原类中最为有限

### Future与Stream的区别

相同点:
- `Future`和`Stream`都是异步执行
不同点:
- `Stream`是很多个`Future`的集合
- `Future`只有一个返回,`Stream`可能存在多个返回.

## Flutter部分

### 生命周期

- initState() 初始化
- didChangeDependencies() 依赖关系变化后
- deactivate() 页面切换,或者被从视图移除,销毁会调用
- dispose() widget销毁的时候
- didUpdateWidget() 状态改变会调用

### Widget,RenderObjects,Element

Widget相当于一个容器,里面是我们写的渲染配置.
RenderObjects使用Widget的配置信息来渲染.
而Element构成了Flutter页面的最小单位,RenderObjects就是通过创建Elements来进行渲染的.

### 常见Widget

- Text
- RichText
- Image
- Icon
- TextField