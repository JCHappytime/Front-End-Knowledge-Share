# Front-End-Interview

介绍一些常见的和自己曾经遇到过的面试题

## JavaScript 面试知识点总结
| 题目                 | 大概内容                   |
| ------------------- | -------------------------- |
| Javascript相关面试题 | js的基本数据类型，es6语法等等|

### 目录
- [1. js基本数据类型介绍](#1-js基本数据类型介绍)
- [2. undefined和null有什么区别](#2-undefined和null有什么区别)



#### 1. js基本数据类型介绍

```
js 一共有六种基本数据类型，分别是:
Undefined、Null、Boolean、Number、String，还有在 ES6 中新增的 Symbol 和 ES10 中新增的 BigInt 类型。
Symbol 代表创建后独一无二且不可变的数据类型，它的出现我认为主要是为了解决可能出现的全局变量冲突的问题。
BigInt 是一种数字类型的数据，它可以表示任意精度格式的整数，使用 BigInt 可以安全地存储和操作大整数，即
使这个数已经超出了 Number 能够表示的安全整数范围。
```

#### 2. undefined和null有什么区别

- 相同点：
```
首先 Undefined 和 Null 都是基本数据类型，这两个基本数据类型分别都只有一个值，就是 undefined 和 null。
```

- 不同点：
```
undefined 代表的含义是未定义，null 代表的含义是空对象。一般变量声明了但还没有定义的时候会返回 undefined，null
主要用于赋值给一些可能会返回对象的变量，作为初始化。
undefined 在 js 中不是一个保留字，这意味着我们可以使用 undefined 来作为一个变量名，这样的做法是非常危险的，它
会影响我们对 undefined 值的判断。但是我们可以通过一些方法获得安全的 undefined 值，比如说 void 0。
当我们对两种类型使用 typeof 进行判断的时候，Null 类型化会返回 “object”，这是一个历史遗留的问题。当我们使用双等
号对两种类型的值进行比较时会返回 true，使用三个等号时会返回 false。
```

## CSS


## HTML


## Vue框架
