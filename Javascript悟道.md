[TOC]

# 第一章 命名

作者认为并不推荐使用 **new** 关键字，因为需要区分构造函数和普通函数，而把函数名首字母大写，作者认为所有变量名都应该使用小写开头

这里引用原文：
> 因为这个世界上每天都有成堆使用new 的粗鄙代码出现，简直可怕。

作者认为一门编程语言不应该有保留字，而JavaScript有很多：

> arguments await break case catch class const continue debugger default delete do else
> enum eval export extends false finally for function if implements import in Infinity
> instanceof interface let NaN new null package private protected public return static
> super switch this throw true try typeof undefined var void while with yield


# 第二章 数值

## 关于零这个数

```javascript

Object.is(0, -0) // false

Infinity === -Infinity // false

Infinity === Infinity // true

1/-0 === 1/0 // false

```

> 建议你不要拿零做除数，也永远不要使用Object.is()

## 数值字面量

> JavaScript 内置了18 437 736 874 454 810 627 个不可变的number 对象，每个对象表示一个数

没有提到为什么是这个数字

> 数值字面量本质上是一个对与该字面量真实值最接近的内置number 对象的引用。有时候，字面量与该值完全吻合，但有时候会相差9.979 201 547 673 599 058 281 863 565 184 2e+291。



内置这么多对象？？
怎么内置？？
什么时候会完全吻合？？

表示数字有：二进制、八进制、十进制、十六进制；和表示特殊的 科学计数法、Infinity、NaN

值得吐槽的是 NaN ，很容易让开发者困惑，NaN意思是 Not a Number，但是 typeof NaN 的结果却是 'number'；还有 ```NaN != NaN && NaN !== NaN```；当我们要判断一个值是不是NaN 时，应当使用 ```Number.isNaN(value)```

> 当字符串转换成数值失败时，结果就是NaN；当转换失败时，程序并不会抛出异常或者直接退出，而是返回NaN


## Number



