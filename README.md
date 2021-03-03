# Front-End-Interview

## 前言


该库主要用来分享一些前端常见的面试题目，包括：JS，CSS，HTML和Vue相关的内容。<br>
如果大家在浏览时发现有不对的地方，欢迎留言指正。

## JavaScript 面试知识点总结
| 题目                 | 大概内容                   |
| ------------------- | -------------------------- |
| Javascript相关面试题 | js的基本数据类型，es6语法，原型链，事件循环，|

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









#### 16. 什么是CSP？

CSP指的是安全策略，它的本质是一个白名单，告诉浏览器哪些外部资源可以加载和执行。我们只需要配置规则，如何拦截由浏览器自己来实现。
通常有2种方式来开启CSP，一种是设置HTTP首部中的Content-Security-Policy,一种是设置meta标签的方式<meta http-equiv="Content-Security-Policy">

可以参考：[《内容安全策略（CSP）》](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CSP)

#### 17. 什么是CSRF攻击？如何防范CSRF攻击？

CSRF攻击指的是跨站请求伪造攻击，攻击者诱导用户进入一个第三方网站，然后该网站向被攻击网站发送跨站情趣。如果用户在被攻击网站中保存了
登录状态，那么攻击者就可以利用这个登录状态，绕过后台的用户验证，冒充用户向服务器执行一些操作。
CSRF攻击的本质是利用cookie会在同源请求中携带发送给服务器的特点，以此来实现用户的冒充。
一般的CSRF攻击类型有三种：
1. GET类型的CSRF攻击，比如在网站中的一个img标签里构建一个请求，当用户打开这个网站的时候就会自动发起提交。
2. POST类型的CSRF攻击，比如说构建一个表单，然后隐藏它，当用户进入页面时，自动提交这个表单。
3. 链接类型的CSRF攻击，比如说在a标签的href属性里构建一个请求，然后诱导用户去点击。

  
#### 19. 虚拟DOM以及diff算法

【参考文章】<br>
1. [详解Vue的diff算法](https://juejin.cn/post/6844903607913938951)<br>


![捕获](https://user-images.githubusercontent.com/10249805/107166141-0ca2de80-69f0-11eb-891d-5fe740374302.PNG)

首先抛出几个问题：

- 1.当数据发生变化时，vue是怎么更新节点的？ 

要知道渲染真实DOM的开销是非常大的。比如有时候我们修改了某个数据，如果直接渲染到真实dom上会引起整个dom树的重绘和重排，有没有可能我们只更新我们修改的那一小块dom
而不要更新整个dom呢？diff算法就可以帮助我们。
  我们先根据真实的dom生成一颗Virtual DOM，当Virtual DOM某个节点的数据改变后会生成一个新的Vnode，然后Vnode与oldVnode对比，发现有不一样的地方就直接修改在真实的
DOM上，然后使oldVnode的值为Vnode。
  diff的过程就是调用名为patch的函数，比较新旧节点，一边比较一边给真实的DOM打补丁。

- 2.Virtual DOM和真实DOM的区别是什么？

Virtual DOM就是将真实DOM的数据抽取出来，以对象的形式模拟树形结构。比如dom是下面这样的：
```
<div>
  <p>test</p>
</div>
```
抽象的Virtual DOM如下：
```
var Vnode = {
  tag: 'div',
  children: [
    {
      tag: 'p',
      text: 'test',
    }
  ],
};
```
可以看出，Vnode是一个对象，跟我们的oldVnode一样。
- 3.diff的比较方式是什么？

在采取diff算法比较新旧节点的时候，比较只会在同层级进行，不会跨层级比较。
```
<div>
  <p>test-01</p>
</div>

<div>
  <span>test-02</span>
</div>
```
上面的代码会分别比较同一层的两个div以及第二层的p和span，但是不会拿div和span作比较。如下面图片所示（来自大神）:

![捕获](https://user-images.githubusercontent.com/10249805/107167168-15e17a80-69f3-11eb-9b67-5958b43e7941.PNG)

这里，我们又可以参考由此延申出来的另一个问题：[20. Vue3和Vue2 diff算法之间的区别](#20-Vue3和vue2-diff算法之间的区别)

- 4.那么diff算法的流程是什么呢？

当数据发生改变时，set方法会调用Dep.notify通知所有订阅者Watcher，订阅者就会调用patch方法给真实的DOM打补丁，从而更新相应的视图。

![捕获](https://user-images.githubusercontent.com/10249805/107310373-3e3aa900-6ac7-11eb-93db-d1ae404bf492.PNG)

那我们来具体分析一下patch时如何打补丁的，下面时patch方法的核心部分：
```
function patch (oldVnode, vnode) {
    // 省略一些代码
    if (sameVnode(oldVnode, vnode)) {
    	patchVnode(oldVnode, vnode)
    } else {
    	const oEl = oldVnode.el; // 当前oldVnode对应的真实元素节点
    	let parentEle = api.parentNode(oEl);  // 父元素
    	createEle(vnode)  // 根据Vnode生成新元素
    	if (parentEle !== null) {
            api.insertBefore(parentEle, vnode.el, api.nextSibling(oEl)); // 将新元素添加进父元素
            api.removeChild(parentEle, oldVnode.el);  // 移除以前的旧元素节点
            oldVnode = null;
    	}
    }
    // 省略一些代码
    return vnode;
}
```


#### 20. Vue3和Vue2 diff算法之间的区别


#### 21. 事件冒泡与事件捕获

【参考文章】
1. [你真的了解事件冒泡与事件捕获吗？](https://juejin.cn/post/6844903834075021326)


PS: 文章中描述得比较清楚，不再单独讲述，请参考以上文章。

#### 22. javascript的垃圾回收机制

【参考文章】
1. [JavaScript 垃圾回收机制](https://juejin.cn/post/6844903858972409869)

PS: 文章中描述得比较清楚，不再单独讲述，请参考以上文章。

#### 23. JS防抖和节流

【参考文章】

1. [JS的防抖与节流](https://juejin.cn/post/6844903618827517965)

- 前言

在进行窗口的resize、scroll，输入框内容校验等操作时，如果事件处理函数调用的频率去限制，会加重浏览器的负担，导致用户体验非常差。
此时我们就可以使用debounce(防抖)和throottle（节流）的方式来减少调用频率，同时也不影响实际效果。

**什么是防抖？**

当持续触发事件时，一定时间段内没有再触发事件，事件处理函数才会执行一次，如果设定的时间到来之前，又一次触发了时间，就重新开始延时。
如下图，持续触发scroll事件时，并不执行handle函数，当1000ms内没有触发scroll事件时，才会延时触发scroll事件。
![捕获](https://user-images.githubusercontent.com/10249805/108584744-ba15da80-737e-11eb-9561-06672d5fd28a.PNG)

那一起来看看如何实现一个简单的debounce吧。

```
function debounce(fun, delay) {
  let time = null;
  return function() {
    if (time !== null) {
      clearTimeout(time);
      time = setTimeout(func, delay);
    }
  }
}

// 处理函数
function handle() {
  console.log('我被触发了');
}

// 滚动事件
window.addEventListener('scroll', debounce(handle, 1000));
```
可以看到，当持续触发scroll事件时，事件处理函数handle只在停止滚动1000毫秒之后才会调用一次，也就是说在持续触发scroll事件的过程中，事件处理函数handle一直没有执行。

**什么是节流？**

函数节流(throttle)：当持续触发事件时，保证一定时间段内只调用一次事件处理函数。节流通俗解释就比如我们水龙头放水，阀门一打开，水哗啦啦的就往下流，我们就会想着要把水
龙头关小一点，最好是按照我们的意愿按照一定规律在某个时间间隔内一滴一滴地往下滴。如下图：持续触发scroll事件时，并不立即执行handle函数，每隔100毫秒才会执行一次handle函数。

![捕获](https://user-images.githubusercontent.com/10249805/108589105-b17dce00-7397-11eb-936d-0642eb62ca55.PNG)

函数节流主要有2种实现方法：时间戳和定时器。接下来分别用2种方法来实现throttle。

1. 时间戳

```
throttle_timestamp(func, delay) {
    let prev = Date.now();
    return function() {
      let context = this;
      let args = arguments;
      let now = Date.now();
      if (now - prev >= delay) {
        func.apply(context, args);
        prev = Date.now();
      }
    };
  }
  
// 处理函数
function handle() {
  console.log('我被触发了');
}

// 滚动事件
window.addEventListener('scroll', throttle_timestamp(handle, 1000));
```
当高频事件触发时，第一次会立即执行（给scroll事件绑定函数与真正触发事件的间隔一般大于delay），而后再怎么频繁地触发事件，也都是每delay时间才执行一次。
而当最后一次事件触发完毕后，事件再也不会被执行了。

2. 定时器

```
throttle_timer(func, delay) {
    let timer = null;
    return function() {
      let context = this;
      let args = arguments;
      if (!timer) {
        timer = setTimeout(function() {
          func.apply(context, args);
          timer = null;
        }, delay);
      }
    };
  }
  
// 处理函数
function handle() {
  console.log('我被触发了');
}

// 滚动事件
window.addEventListener('scroll', throttle_timer(handle, 1000));
```
当触发事件的时候，我们设置一个定时器，再次触发事件的时候，如果定时器存在，就不执行，直到delay时间后，定时器执行函数并清空定时器，这样就可以设置下一个定时器。
当第一次触发事件时，不会立即执行函数，而是在delay秒后才执行。而后再怎么频繁触发事件，也都是每delay时间才执行一次。当最后一次停止触发后，由于定时器delay延迟，
可能还会执行一次函数。

- 总结
```
函数防抖：将几次操作合并为一次操作进行。原理是维护一个计时器，规定在delay时间后触发函数，但是在delay时间内再次触发的话，就会取消之前的计时器而重新设置。这样一来，
	 只有最后一次操作能被触发。
	 
函数节流：使得一定时间内只触发一次函数。原理是通过判断是否到达一定时间来触发函数。

区别： 函数节流不管事件触发有多频繁，都会保证在规定时间内一定会执行一次真正的事件处理函数，而函数防抖只是在最后一次事件后才触发一次函数。 比如在页面的无限加载场景
      下，我们需要用户在滚动页面时，每隔一段时间发一次 Ajax 请求，而不是在用户停下滚动页面操作时才去请求数据。这样的场景，就适合用节流技术来实现。
```


## CSS
| 题目         | 大概内容                    |
| ------------ | -------------------------- |
| CSS常见面试题 | 垂直居中方式，双栏/三栏布局方式，header+main+footer布局|

### 目录

- [1. 垂直居中的实现方式有哪些？](#1-垂直居中的实现方式有哪些)








#### 1. 垂直居中的实现方式有哪些？

【参考文章】

1. [CSS实现垂直居中的几种方法](https://juejin.cn/post/6844903843193470983)

- 前言

水平居中的实现方式比较简单，对于块级元素而言，设置margin: 0 auto; 对于行内元素而言设置text-align: center就可以实现。垂直居中相对而言就要复杂一些。

- flex布局

flex布局可以很方便的实现垂直与水平居中，好处很多，在移动端使用比较广泛，不好的地方就是浏览器兼容性不好。代码如下：

```
//html
<div class="main">
  <div class="middle"></div>
</div>

//css
.main {
  width: 60px;
  height: 10%;
  background: #dddddd;
  display: flex;
  justify-content: center;
  align-items: center;
}
.middle{
  width: 30%;
  height: 50%;
  background: red;
}
```
- 绝对定位/相对定位

1. 在不知道自己高度和父容器高度的情况下，利用绝对定位.

```
.parent {
  position: relative;
}

.children {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
```
2. 若父容器下只有一个元素，且父容器设置了高度，则只需要使用相对定位即可。

```
.parent {
  height: 200px;
}

.children {
  position: relative;
  top: 50%;
  transform: translateY(-50%);
}
```
- 定位+top, left, margin-top, margin-left

```
.item-middle {
  position: absolute;
  width: 100px;
  height: 100px;
  top: 50%;
  left: 50%;
  margin-top: -50px;
  margin-left: -50px;
  background: blue;
}
```
如下图所示：

![捕获](https://user-images.githubusercontent.com/10249805/108591327-31f5fc00-73a3-11eb-898c-a6b145eae8da.PNG)



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



