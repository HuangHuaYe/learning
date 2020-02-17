# Basics

## Assertion

使用 assert 方法进行判断,如果判断为 false 程序会直接退出.

```swift
    let age = -3
    assert(age >= 0, "A person's age can't be less than zero.")
    // This assertion fails because -3 is not >= 0.
```

## Precondition

使用 precondition 方法同样跟 assert 一样会退出程序
```swift
    // In the implementation of a subscript...
    precondition(index > 0, "Index must be greater than zero.")
```