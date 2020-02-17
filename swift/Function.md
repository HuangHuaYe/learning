# Function

## 隐式返回值

函数体只有一行的时候,会隐式返回值
```swift
    func greeting(for person: string) -> String {
    	"hello"
    }
```
## 参数标签和参数名

参数标签用于函数调用时使用,参数名在函数体内部使用.
```swift
    func someFunction(argumentLabel parameterName: Int) {
        // 在函数体内，parameterName 代表参数值
    }
    
    // 可以使用下划线在参数调用的时候不填入参数标签
    func someFunc(_ argName: String) {
    	
    }
    someFunc("q")
```

## 可变参数

可变参数是一个参数可以接受多个传参数,函数体调用的时候,会自动封装成一个数组类型.一个函数最多有一个可变参数.

```swift
    func arithmeticMean(_ numbers: Double...) -> Double {
        var total: Double = 0
        for number in numbers {
            total += number
        }
        return total / Double(numbers.count)
    }
    arithmeticMean(1, 2, 3, 4, 5)
    // 返回 3.0, 是这 5 个数的平均数。
    arithmeticMean(3, 8.25, 18.75)
    // 返回 10.0, 是这 3 个数的平均数。
```

## 输入输出函数

swift的正常状态下都是不能更改的,如果需要更能改,要在参数的类型批注前加入 inout 关键字,并且在函数调用的时候在参数名/标签前加入&符号.

```swift
    func swapTwoInts(_ a: inout Int, _ b: inout Int) {
        let temporaryA = a
        a = b
        b = temporaryA
    }
    swapTwoInts(&someInt, &anotherInt)
```