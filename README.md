# Front-End-Interview

## 前言


该库主要用来分享一些前端常见的面试题目，包括：JS，CSS，HTML和Vue相关的内容。<br>
如果大家在浏览时发现有不对的地方，欢迎留言指正。

## JavaScript 面试知识点总结
| 题目                 | 大概内容                   |
| ------------------- | -------------------------- |
| Javascript相关面试题 | js的基本数据类型，es6语法，原型链，事件循环等|

### 目录
- [1. JS数据类型有哪些？如何进行类型判断？不同类型的内存图大致是怎样的？](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/2)
- [2. 闭包是什么，原理是什么，怎么用？哪些场景下会用到？](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/3)
- [3. 讲讲深拷贝与浅拷贝，如何实现，有哪些方式？](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/4)
- [4. 讲一讲 JavaScript 的垃圾回收机制](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/5)
- [5. Vue的生命周期有哪些？每个周期内完成的功能是什么？](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/6)
- [6. 垂直居中的几种实现方案 ](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/7)
- [7. 你能用几种方案实现双栏布局？](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/8)
- [8. webpack中有哪些常用的plugin，分别是什么作用？](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/9)
- [9. 原型，原型链和继承的关系，如何实现继承？](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/10)
- [10. 讲讲es6的新特性主要有哪些？](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/11)
- [11. http协议，缓存协议（强缓存+协商缓存）](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/12)
- [12. 具体详细的讲一讲MVVM数据绑定的原理+实现](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/13)
- [13. call, bind, apply,三者的关系和区别](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/14)
- [14. 介绍一下Vue与React之间有什么相同点与不同点](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/15)



## CSS
| 题目         | 大概内容                    |
| ------------ | -------------------------- |
| CSS常见面试题 | 垂直居中方式，双栏/三栏布局方式，header+main+footer布局等|

### 目录

- [1. 垂直居中的实现方式有哪些？](#1-垂直居中的实现方式有哪些)




## Vue框架

| 题目                 | 大概内容                   |
| ------------------- | -------------------------- |
| Vue相关面试题 | Vue生命周期，MVVM原理，Vue3与Vue2对比，|

### 目录
- [1. Vue的生命周期钩子有哪些,每个生命周期实现什么功能？](#1-Vue的生命周期钩子有哪些每个生命周期实现什么功能)
- [2. MVVM的原理是什么](#2-MVVM的原理是什么)



#### 1. Vue的生命周期钩子有哪些,每个生命周期实现什么功能？

【参考文章】

1. [Vue-生命周期函数](https://mp.weixin.qq.com/s/rzkrHlNW9g9RhwdMHaQkDA)

- 生命周期每个阶段作用分析

（1）beforeCreate

实例初始化之后调用beforeCreate，此时的数据观察和事件配置都没有准备好。此时实例中的data和el都还是undefined，不可用。

（2）created

在实例创建完成之后立即调用created，此时我们能够读取到数据data的值，但是dom还没有生成，所以属性el还不存在。

（3）beforeMount

在挂载开始之前被调用，此阶段为即将挂载，此时el不再是undefined，而是成功关联到我们制定的dom节点，但此时的变量如：{{ name }}还没有被成功地渲染成我们data中的数据。

（4）mounted

挂载完毕后调用，到了这个阶段，数据就会被成功渲染出来。如果此时打印属性$el，就会看到{{name}}已经被成功的渲染成data.name里面的内容了。

（5）beforeUpdate

我们知道，当修改vue实例的data时，vue就会自动帮我们更新渲染视图，在这个过程中，vue提供了beforeUpdate这个钩子，在检测到我们要修改数据时，更新渲染视图
之前就会触发钩子beforeUpdate。


#### 2. MVVM的原理是什么



## 性能优化相关

### 目录

- [1. 前端性能优化之webpack](#1-前端性能优化之webpack)


#### 1. 前端性能优化之webpack

【参考文章】

[前端性能优化-webpack](https://juejin.cn/post/6911472693405548557)



