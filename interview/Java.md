# Java

## String StringBuffer StringBuilder 的区别

可变:
- String不可变
- StringBuilder StringBuffer不可变
  
线程安全:

- String不可变线程安全
- StringBuffer加了同步锁所以线程安全
- StringBuilder线程不安全

性能:

- String性能最差
- StringBuffer性能中等
- StringBuilder性能最快,但是性能不安全

适用:

- 操作少的时候
- 单线程需要操作大量数据,使用StringBuilder
- 多线程大量数据,使用StringBuffer

## 静态成员和静态方法

Java中静态方法不能访问静态变量

## == 与 equals 的区别

- == 用来判断对象的时候,是判断两个对象值是否相等
- equals() 判断的时候如果覆盖了实现方法,调用实现方法,如果不是,等价于 ==

## hasCode 与 equals

对象加入hashSet的时候,会调用hashCode对已有的对象进行比较,如果hasCode相等,调用equals进行对比,不同加入集合,相同就不会加入.
所以重写hasCode会大大提高性能.

## 反射机制

反射机制是在运行时能获取任意一个对象或者类的所有属性和方法.

- 优点: 运行时对类型进行判断,动态加载类,代码灵活
- 缺点: 性能比较差

主要用来设计框架比如spring

## JVM JDK JRE

JVM是java的虚拟机,是运行java编译后的字节码的环境
JDK是java开发套件,他与JRE是包含关系,有编译器和工具.
JRE是java的运行环境,java程序跑起来的环境.

## 字节码

java的字节码是把java代码编译成字节码然后在jvm中运行.这样子既有性能比较高的优点,又有跨平台的优点.

## 上下文切换

在运行多线程的时候,某个程序进入阻塞状态,cpu时间切换去运行其他阻塞等待的程序时,需要把环境切换到下一个运行线程需要的环境.这就是上下文切换.

## sleep 和 wait 方法

sleep没有释放锁,wait释放了锁.
sleep会主动醒过来,wait需要设置超时时间或者其他进程唤起才可以.

## 线程运行

[线程运行](images/thread.png)

