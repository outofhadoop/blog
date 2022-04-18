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





