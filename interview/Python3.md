# Python3

## **python2和python3区别**

1、Python3 使用 print 必须要以小括号包裹打印内容，比如 print('hi')

Python2 既可以使用带小括号的方式，也可以使用一个空格来分隔打印内容，比 如 print 'hi'

2、python2 range(1,10)返回列表，python3中返回迭代器，节约内存

3、python2中使用ascii编码，python中使用utf-8编码

4、python2中unicode表示字符串序列，str表示字节序列

python3中str表示字符串序列，byte表示字节序列

5、python2中为正常显示中文，引入coding声明，python3中不需要

6、python2中是raw_input()函数，python3中是input()函数

## 列表推导式

如下的代码:
```python
    [x*y for x in range(1,5) if x > 2 for y in range(1,4) if y < 3]
```
实际执行为:
```python
    for x in range(1,5)
        if x > 2
            for y in range(1,4)
                if y < 3
                    x*y
```
## 字段推导式
```python
    # { key_expr: value_expr for value in collection if condition }
    
    strings = ['import','is','with','if','file','exception']
    D = {key: val for val,key in enumerate(strings)}
    # {'exception': 5, 'file': 4, 'if': 3, 'import': 0, 'is': 1, 'with': 2}
```
## lambda
```python
    lambda x:x+2
    # def func(x):
    #  return x+2
```
## Generator
利用`yield`关键字修饰的就是`generator`.简单语法如下:
```python
    def createGenerator():
    	myList = range(3)
    	for i in myList:
    		yield i*i
    
    mygenerator = createGenerator()
    for i in mygenerator:
    	print(i)
    
    # 0
    # 1
    # 4
    
    # 也可以使用next()获取下一个元素
```

`generator`跟`list`,`tulpe`等可以循环的元素不同的地方是,他内部的元素都是动态生成的,而不是一下子生成全部存到内存里面.

## *args, **kwargs

其实都是一种东西,`*args`习惯用来无命名参数,`**kwargs`习惯用来标明带命名的参数.
 
## Decorator

使用`functools`模块的`wrap`的帮助装饰类创建`decorator`.语法如下:

```python
def my_decorator(func: types.FunctionType):
    def wrapper(*args, **kwargs):
        print('start wrapper')
        func(*args, **kwargs)
        print('end of wrapper')
    return wrapper

@my_decorator
def test():
    print('function body')
```

## `__new__`和`__init__`的区别

`__new__`创新新实例的时候调用,`__init__`是实例初始化的时候调用.


## 单例模式

```python
# 装饰器版本,利用闭包
def singleton(cls):
    instances = {}
    def getinstance(*args, **kw):
        if cls not in instances:
            instances[cls] = cls(*args, **kw)
        return instances[cls]
    return getinstance

@singleton
class MyClass:
    pass


# __new__方法
class Singleton(object):
    def __new__(cls, *args, **kw):
        if not hasattr(cls, '_instance'):
            orig = super(Singleton, cls)
            cls._instance = orig.__new__(cls, *args, **kw)
        return cls._instance

class MyClass(Singleton):
    a = 1
```

## GIL(global interpreter lock) 全局锁
Python为了保证线程安全而采取的独立线程运行的限制,说白了就是一个核只能在同一时间运行一个线程.对于io密集型任务，python的多线程起到作用，但对于cpu密集型任务，python的多线程几乎占不到任何优势，还有可能因为争夺资源而变慢。

## 协程

与多线程不同:
- 是单线程,没有线程开销
- 极高的执行效率
- 没有锁

传统的生产者-消费者模型是一个线程写消息，一个线程取消息，通过锁机制控制队列和等待，但一不小心就可能死锁。

如果改用协程，生产者生产消息后，直接通过yield跳转到消费者开始执行，待消费者执行完毕后，切换回生产者继续生产，效率极高：

**子线程就是协程的一种特例**

```python
import time

def consumer():
    r = ''
    while True:
        n = yield r
        if not n:
            return
        print('[CONSUMER] Consuming %s...' % n)
        time.sleep(1)
        r = '200 OK'

def produce(c):
    c.next()
    n = 0
    while n < 5:
        n = n + 1
        print('[PRODUCER] Producing %s...' % n)
        r = c.send(n)
        print('[PRODUCER] Consumer return: %s' % r)
    c.close()

if __name__=='__main__':
    c = consumer()
    produce(c)
```

## 可变类型和不可变类型

- 不可变: int,string,tuple
- 可变: list,dict

## Python的垃圾回收机制

1. 引用计数
2. 标记-清除
   等到没有空闲内存的时候从寄存器和程序栈上的引用出发，遍历以对象为节点、以引用为边构成的图，把所有可以访问到的对象打上标记，然后清扫一遍内存空间，把所有没标记的对象释放
3. 分代技术
   将系统中的所有内存块根据其存活时间划分为不同的集合，每个集合就成为一个“代”，垃圾收集频率随着“代”的存活时间的增大而减小，存活时间通常利用经过几次垃圾回收来度量。
   Python默认定义了三代对象集合，索引数越大，对象存活时间越长。