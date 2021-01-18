# Front-End-Interview

该库主要用来分享一些前端常见的面试题目，包括：JS，CSS，HTML和Vue相关的内容。<br>
如果大家在浏览时发现有不对的地方，欢迎留言指正。

## JavaScript 面试知识点总结
| 题目                 | 大概内容                   |
| ------------------- | -------------------------- |
| Javascript相关面试题 | js的基本数据类型，es6语法，原型链，|

### 目录
- [1. js基本数据类型介绍](#1-js基本数据类型介绍)
- [2. undefined和null有什么区别](#2-undefined和null有什么区别)
- [3. Javascript 有几种类型的值，内存图长啥样？](#3-Javascript-有几种类型的值内存图长啥样)
- [4. 内部属性[[Class]]是什么？](#4-内部属性Class是什么)
- [5. 介绍一下Proxy是什么？](#5-介绍一下Proxy是什么)
- [6. 什么是闭包，为什么要用它？](#6-什么是闭包为什么要用它)
- [7. js类型判断有哪些方式？](#7-js类型判断有哪些方式)



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

#### 3. Javascript 有几种类型的值，内存图长啥样？

```
知识点：
- 栈：基本数据类型（Undefined, Null, Boolean, Number, String, Symbol, BigInt）
- 堆：引用数据类型（Object, Array，Function）
以上两种类型的区别是：存储位置不同。
- 基本数据类型直接存储在栈（Stack）中的简单数据段，占据空间小，大小固定且是频繁使用的数据。
- 引用数据类型存储在堆（Heap）中的对象，占据空间大，大小不固定。但是如果存储在栈中，将会影响程序运行的性能；引用数据
  类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器找到引用值时，首先检索其在栈中的地址，取得内存地址后
  从堆中获得实体。
```
答案：

```
js可以分为两种类型的值，一种是基本数据类型，一种复杂数据类型。
基本数据类型可以参考问题1.
复杂数据类型指的是：Object类型，如Array, Date等数据类型都可以理解为Object类型的子类。
*** 两种类型的主要区别是它们的存储位置不同，基本数据类型的值直接保存在栈中，复杂数据类型的值保存在堆中，通过使用在栈
    中保存对应的指针来获取堆中的值。
```
#### 4. 内部属性[[Class]]是什么？

```
所有typeof返回值为Object的对象都包含一个内部属性。这个属性无法直接访问，一般通过Object.prototype.toString(..)
来查看。如：
Object.prototype.toString.call(['a', 'b', 'c'])
=>"[object Array]"

Object.prototype.toString.call(/regex-literal/i/);
=>"[object RegExp]"

但是我们自己创建的类就不会有这样的待遇，因为toString()找不到toStringTag属性，只能返回默认的Object标签。
默认情况下，类的[[Class]]返回[object Object]，如：
class Person {}
Object.prototype.toString.call(new Person());
=>"[object Object]"
**这个时候需要定制我们自己的[[Class]]
class Person1 {
  get [Symbol.toStringTag]() {
    return 'Person1';
  }
 }
 Object.prototype.toString.call(new Person1());
 => "[object Person1]"
```
#### 5. 介绍一下Proxy是什么？
```
- Proxy用于修改某些操作的默认行为，相当于在语言层面做出修改，即对编程语言进行编程。
- Proxy可以认为是：在目标对象之前假设一层拦截，外界对该对象的访问，都必须首先通过这层拦截，因此提供了一种机制，
  可以对外界的访问进行过滤和改写。
  Proxy意思是代理，在这里表示由它来“代理”某些操作，可以译为代理器。
```
#### 6. 什么是闭包，为什么要用它？
```
1）闭包是指有权访问另一个函数作用域中变量的函数，创建闭包的最常见方式就是在一个函数内创建另一个函数，创建的函数
可以访问到当前函数的局部变量；
2）闭包有两个常用的用途：
  2.1 使我们在函数外部能够访问到函数内部的变量。通过使用闭包，我们可以在外部调用闭包函数，从而在外部访问到函数
  内部的变量，可以使用这种方法来创建私有变量。
  2.2 使已经运行结束的函数上下文中的变量对象继续留在内存中，因为闭包函数保留了这个变量对象的引用，所以这个变量
  对象不会被回收。
其实闭包的本质就是作用域链的一个特殊应用，只要了解了作用域链的创建过程，就能够理解闭包的实现原理。经典例子如下：
function createFunctions() {
  let result = new Array();
  for (var i=0;i<10;i++) {
    result[i] = function() {
      console.log(i);
    }
  }
  return result;
}
=>
result[0](); // 9
result[1](); // 9
result[2](); // 9
result[3](); // 9
result[4](); // 9
result[5](); // 9
为什么上述结果都一样，而不是返回自己的索引呢？
  这是因为在执行全局代码之前，js引擎会对全局代码进行解析，创建全局执行上下文globalContext。之后进入到全局代码的执行阶段，
首先将全局执行上下文压入执行上下文栈中，然后按顺序依次执行代码。
```
#### 7. js类型判断有哪些方式？
```
一共有4种方法：
（1）typeof
  typeof是一个操作符而不是函数，右侧跟一个一元表达式，并返回这个表达式的数据类型。返回的结果用该类型的字符串(全小写字母)形
  式表示，包括以下 7 种：number、boolean、symbol、string、object、undefined、function 等。有些时候，typeof 操作符会返
  回一些令人迷惑但技术上却正确的值：
  - 对于基本类型，除 null 以外，均可以返回正确的结果。
  - 对于引用类型，除 function 以外，一律返回 object 类型。
  - 对于 null ，返回 object 类型。
  - 对于 function 返回  function 类型。
  其中，null 有属于自己的数据类型 Null ， 引用类型中的 数组、日期、正则 也都有属于自己的具体类型，而 typeof 对于这些类型的
  处理，只返回了处于其原型链最顶端的 Object 类型，没有错，但这不是我们想要的最终结果。
（2）instanceof

（3）Object.prototype.toString.call()

（4）constructor
```


## CSS
| 题目         | 大概内容                    |
| ------------ | -------------------------- |
| CSS常见面试题 | 垂直居中方式，双栏/三栏布局方式，header+main+footer布局|

## HTML


## Vue框架
