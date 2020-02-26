# compare

# == 与 === 的区别

## 概念

== 是相等运算符, 两边值不同的时候,会进行一次类型转换,将两边转换成同一种类型后,再进行判断

=== 是恒等运算符,不对两边进行类型转换转换,直接对比.

### IEA 算法 (=== 算法)

1. If both operands have *different types*, they are **not strictly equal**
2. If both operands are `null`, they are **strictly equal**
3. If both operands are `undefined`, they are **strictly equal**
4. If one or both operands are `NaN`, they are **not strictly equal**
5. If both operands are `true` or both `false`, they are **strictly equal**
6. If both operands are *numbers* and have *the same value*, they are **strictly equal**
7. If both operands are *strings* and have *the same value*, they are **strictly equal**
8. If both operands have reference to *the same object or function*, they are **strictly equal**
9. In all other cases operands are **not strictly equal**.

### OPCA算法(对象类型转换成原始类型算法)

1. If the method `valueOf()` exists it is called. If `valueOf()` returns a primitive, the object is converted to this value
2. In other case if the method `toString()` exists it is called. If `toString()` returns a primitive, the object is converted to this value
3. In other case JavaScript throws an error: `TypeError: Cannot convert object to primitive value`

Most of the native objects when calling the [valueOf()](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf) method returns the object itself. So the [toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString) method is used more often.A note about the `Date` objects: when converting to a primitive, the object is converted instantly to a string using `toString()` method. This way the rule 1 is skipped for `Date`. The plain JavaScript object, `{}` or `new Object()`, usually is converted to `"[object Object]"`.An array is converted to by joining it’s elements with `","` separator. For example `[1, 3, "four"]` is converted to `"1,3,four"`.

### EEA算法(== 算法)

1. If the operands have the same type, test them for strict equality using **IEA**. If they are not strictly equal, they **aren’t equal**, otherwise they are **equal**
2. If the operands have different types:
    1. If one operand is `null` and another `undefined`, they **are equal**
    2. If one operand is *number* and another is a *string*, convert the *string* to *number*. Compute the comparison again
    3. If one operand is *boolean*, transform `true` to `1` and `false` to `0`. Compute the comparison again
    4. If one operand is an *object* and another is a *number* or *string*, convert the *object* to a primitive using **OPCA**. Compute the comparison again
    5. In all other cases operands are **not equal**

**Example 1**

    1 == true // true

1. `1 == true` (Transform `true` to `1` using [EEA rule 2.3](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#eea-2.3))
2. `1 == 1` (Operands have the same type, numbers. Transform the equality to identity using [EEA rule 1](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#eea-1))
3. `1 === 1` (Both operands are numbers and have the same value. Based on [IEA rule 6](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#iea-6), it’s an equality)
4. `true`

**Example 2**

    '' == 0 // true

1. `'' == 0` (One operand is string and another is number, based on [EEA rule 2.2](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#eea-2.2) the `''` is transformed to a number)
2. `0 == 0` (Operands are the same type, transform the equality to identity using [EEA rule 1](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#eea-1))
3. `0 === 0` (Operands are the same type and have the same value, so based on [IEA rule 6](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#iea-6) it’s an identity)
4. `true`

**Example 3**

    null == 0 // false

1. `null == 0` (`null` is a primitive of type null and `0` is number. Apply the [EEA rule 3](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#eea-3))
2. `false`

**Example 4**

    null == undefined // true

1. `null == undefined` (Based on [EEA rule 2.1](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#eea-2.1) the operands are equal)
2. `true`

**Example 5**

    NaN == NaN // false

1. `NaN == NaN` (Both operands are numbers. Transform the equality to identity using [EEA rule 1](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#eea-1))
2. `NaN === NaN` (Based on rule [IEA rule 4](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#iea-4) the operands are not strictly equal)
3. `false`

**Example 6**

    [''] == '' // true

1. `[''] == ''` (`['']` is an array and `''` a string. Apply the [EEA rule 2.4](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#eea-2.4) and transform the array to a primitive using [OPCA rule 2](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#opca-2))
2. `'' == ''` (Both operands are strings, so transform the equality to identity)
3. `'' === ''` (Both operands are the same type and have the same value. Using the [IEA rule 7](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#iea-7) it’s an identity)
4. `true`

**Example 7**

    {} == true // false

1. `{} == true` (Using the [EEA rule 2.3](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#eea-2.3), transform the `true` operand to `1`)
2. `{} == 1` (First operand is an object, so it’s necessary to transform it to a primitive using OPCA)
3. `"[object Object]" == 1` (Because first operand is a string and second a number, we need to transform the `"[object Object]"` to a number using the [EEA rule 2.2](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#eea-2.2))
4. `NaN == 1` (Both operands are numbers, so transform the equality to identity using [EEA rule 1](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#eea-1))
5. `NaN === 1` (Based on [IEA rule 4](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#iea-4), which says that nothing is equal with a `NaN`, the result is `false`)
6. `false`

参考链接: 

[](https://blog.csdn.net/chenchunlin526/article/details/78850171)

[The Legend of JavaScript Equality Operator](https://dmitripavlutin.com/the-legend-of-javascript-equality-operator/#eea-3)
