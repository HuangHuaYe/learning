# shell

## 字符串

### 字符串可以直接拼接

```shell
your_name="runoob"
# 使用双引号拼接
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting  $greeting_1
# 使用单引号拼接
greeting_2='hello, '$your_name' !'
greeting_3='hello, ${your_name} !'
echo $greeting_2  $greeting_3
```

### 获取字符串长度

```shell
string="123213"
echo ${#string} # 6
```

### 截取字符串

```shell
string="123123"
echo ${string:1:2} # 2
```

### 获取索引

```shell
string="1231231"
echo `expr index "${string}" io`
```

## 数组

用小括号扩起来,注意没有逗号

```shell
array=(val val2)

first_val=${array[0]}
all_val=${array[@]}
length=${#array[*]}
```

## 获取脚本参数

### 按顺序获取

```shell
echo "Shell 传递参数实例！";
echo "执行的文件名：$0";
echo "第一个参数为：$1";
echo "第二个参数为：$2";
echo "第三个参数为：$3";

```

上面的代码输出如下:

```
第一个参数为：1
第二个参数为：2
第三个参数为：3
```

### 其他获取参数的特殊变量

参数处理 |	说明
---|---
$# | 传递到脚本的参数个数
$* |	以一个单字符串显示所有向脚本传递的参数 如 $* 用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。
$! |	后台运行的最后一个进程的ID号
$@ |	与$*相同，但是使用时加引号，并在引号中返回每个参数。如"$@"用「"」括起来的情况、以"$1" "$2" … "$n" 的形式输出所有参数。
$- |	显示Shell使用的当前选项，与set命令功能相同。
$? | 显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。

## 操作符

shell不支持算术运算,但是可以利用`expre`来实现

```shell
echo `expr 2 + 2`
```

### 关系运算符

关系运算符只支持数字,不支持字符串,除非字符串是数字

运算符 | 说明
---|---
-eq | 等于
-ne | 不等于
-gt | 大于
-lt | 小于
-ge | 大于等于
-le | 小于等于

### 字符串运算符

运算符 | 说明
---|---
=  | 等于
!= | 不等于
-z | 长度是否为零
-n | 长度是否不为零
$  | 长度是否为空

## if else

```shell
if [ condition ]
then
  command
  ...
fi

# 嵌套
if [ condition ]
then 
  command
  ...
elif [ condition2 ]
then
  command2
  ...
fi
```

## for while util

```shell
for var in item1 item2 ... itemN
do
    command1
    command2
    ...
    commandN
done

while(( $int<=5 ))
do
    echo $int
    let "int++"
done
```

### case

```shell
echo '输入 1 到 4 之间的数字:'
echo '你输入的数字为:'
read aNum
case $aNum in
    1)  echo '你选择了 1'
    ;;
    2)  echo '你选择了 2'
    ;;
    3|4)  echo '你选择了 3或者4'
    ;;
    *)  echo '你没有输入 1 到 4 之间的数字'
    ;;
esac
```

## 函数

函数跟其他语言几乎一样,就是使用 `$n` 获取参数, 调用也有点区别

```shell
unWithParam(){
    echo "第一个参数为 $1 !"
    echo "第十一个参数为 ${11} !"
    echo "参数总数有 $# 个!"
    echo "作为一个字符串输出所有参数 $* !"
}
funWithParam 1 2 3 4 5 6 7 8 9 34 73
```

## 引入文件

```shell
# test1.h
#!/bin/bash

url="http://www.runoob.com"

# end

# test2.h
#!/bin/bash

#使用 . 号来引用test1.sh 文件
. ./test1.sh

# 或者使用以下包含文件代码
# source ./test1.sh

echo "菜鸟教程官网地址：$url"
```