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

    [x*y for x in range(1,5) if x > 2 for y in range(1,4) if y < 3]

实际执行为:

    for x in range(1,5)
        if x > 2
            for y in range(1,4)
                if y < 3
                    x*y

## 字段推导式

    # { key_expr: value_expr for value in collection if condition }
    
    strings = ['import','is','with','if','file','exception']
    D = {key: val for val,key in enumerate(strings)}
    # {'exception': 5, 'file': 4, 'if': 3, 'import': 0, 'is': 1, 'with': 2}

## lambda

    lambda x:x+2
    # def func(x):
    #  return x+2

## Generator

利用`yield`关键字修饰的就是`generator`.简单语法如下:

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

`generator`跟`list`,`tulpe`等可以循环的元素不同的地方是,他内部的元素都是动态生成的,而不是一下子生成全部存到内存里面.

## *args, **kwargs

其实都是一种东西