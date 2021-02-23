# Front-End-Interview

## 前言


该库主要用来分享一些前端常见的面试题目，包括：JS，CSS，HTML和Vue相关的内容。<br>
如果大家在浏览时发现有不对的地方，欢迎留言指正。

## JavaScript 面试知识点总结
| 题目                 | 大概内容                   |
| ------------------- | -------------------------- |
| Javascript相关面试题 | js的基本数据类型，es6语法，原型链，事件循环，|

### 目录
- [1. js基本数据类型介绍](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/2)
- [2. undefined和null有什么区别](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/2)
- [3. Javascript 有几种类型的值，内存图长啥样？](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/2)
- [4. 内部属性[[Class]]是什么？](#4-内部属性Class是什么)
- [5. 介绍一下Proxy是什么？](#5-介绍一下Proxy是什么)
- [6. 什么是闭包，为什么要用它？](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/3)
- [7. js类型判断有哪些方式？](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/2)
- [8. Vue3和Vu2之间有什么区别？](#8-Vue3和Vu2之间有什么区别)
- [9. this的指向问题](#9-thisthis的指向问题)
- [10. 作用域和作用域链](#10-作用域和作用域链)
- [11. 浏览器预解析变量提升](#11-浏览器预解析变量提升)
- [12. js中的深浅拷贝实现？](https://github.com/JCHappytime/Front-End-Interview-Vue/issues/4) 
- [13. 手写call, apply以及bind函数](#13-手写call-apply以及bind函数)
- [14. Vue3相比Vue2新增了哪些功能？](#14-Vue3相比Vue2新增了哪些功能)
- [15. 什么是XSS攻击？如何防范XSS攻击？](#15-什么是XSS攻击如何防范XSS攻击)
- [16. 什么是CSP？](#16-什么是CSP)
- [17. 什么是CSRF攻击？如何防范CSRF攻击？](#17-什么是CSRF攻击如何防范CSRF攻击)
- [18. 原型和原型链有什么特点？](#18-原型和原型链有什么特点)
- [19. 虚拟DOM以及diff算法](#19-虚拟DOM以及diff算法)
- [20. Vue3和Vue2 diff算法之间的区别](#20-Vue3和vue2-diff算法之间的区别)
- [21. 事件冒泡与事件捕获](#21-事件冒泡与事件捕获)
- [22. javascript的垃圾回收机制](#22-javascript的垃圾回收机制)
- [23. JS防抖和节流](#23-JS防抖和节流)

#### 4. 内部属性[[Class]]是什么？

```
所有typeof返回值为Object的对象都包含一个内部属性。这个属性无法直接访问，一般通过Object.prototype.toString(..)
来查看。如：
Object.prototype.toString.call(['a', 'b', 'c'])
=>"[object Array]"

Object.prototype.toString.call(/regex-literal/i/);
=>"[object RegExp]"

但是我们自己创建的类就不会有这样的待遇，因为toString()找不到toStringTag属性，只能返回默认的Object标签。
（PS：有时候也可以用来判断数据的类型）
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
  
#### 8. Vue3和Vu2之间有什么区别？

我们首先关注一下Vue3.0与Vue2.x的一些最主要的区别。Vue是一种典型的 MVVM 模式的框架，我们知道 MVVM 模式在于数据与视图的保持同步，意思是说数据改变时会自动更新视图，视图发生变化时会更新数据。

![捕获](https://user-images.githubusercontent.com/10249805/107138658-8d120280-6950-11eb-83ba-b9354a81824b.PNG)

- 双向绑定实现的区别
 Vue采用的是数据劫持与发布订阅相结合的方式实现双向绑定。
 
【参考文章】

1. [Vue2和Vue3双向数据绑定的区别](https://juejin.cn/post/6844904045237272583)<br>
2.[Vue双向绑定原理](https://zhuanlan.zhihu.com/p/47541415)

【Vue2.x】

```
Vue2.x采用es5中的Object.defineproperity()来实现双向绑定。
```

【Vue3.0】

```
Vue3.0采用es6中新增的proxy()方法来实现。
```

```
1. Vue3.0的响应数据是包含在一个反应状态中的，因此当我们在HTML中取数据时应该这样{{ state.username }}而不是像以前一样{{ username }};

2. 建立数据data的方式不同。
  - Vue2.0 把两个数据放入data属性中
  export default {
  props: {
    title: String
  },
  data () {
    return {
      username: '',
      password: ''
    }
  }
}
- Vue3.0 在Vue3.0，我们就需要使用一个新的setup()方法，此方法在组件初始化构造的时候触发。为了可以让开发者对反应型数据有更多的控制，我们可
以直接用到 Vue3 的反应API（reactivity API）。从以下三个步骤来建立反应性数据：
（1）从vue引入reactive
（2）使用reactive()方法来声名我们的数据为反应性数据
（3）使用setup()方法来返回我们的反应性数据，从而我们的template可以获取这些反应性数据
import { reactive } from 'vue'

export default {
  props: {
    title: String
  },
  setup () {
    const state = reactive({
      username: '',
      password: ''
    })

    return { state }
  }
}
这里构造的反应性数据就可以被template使用，可以通过state.username和state.password获得数据的值。

3. 对比二者的methods写法
  - Vue2.0 直接将方法包含在methods属性中就可以使用了。
  - Vue3.0 需要在setup中定义并返回，如下所示：
  export default {
  props: {
    title: String
  },
  setup () {
    const state = reactive({
      username: '',
      password: ''
    })

    const login = () => {
      // 登陆方法
    }
    return { 
      login,
      state
    }
  }
}

4. 生命周期钩子 lifecycle hooks
  - Vue2.0 我们可以直接在组件属性中调用Vue的生命周期的钩子，如mounted():
  export default {
  props: {
    title: String
  },
  data () {
    return {
      username: '',
      password: ''
    }
  },
  mounted () {
    console.log('组件已挂载')
  },
  methods: {
    login () {
      // login method
    }
  }
}
- Vue 3.0 合成型API里面的setup()方法可以包含了基本所有东西。生命周期的钩子就是其中之一。
  但是在 Vue3 生周期钩子不是全局可调用的了，需要另外从vue中引入。和刚刚引入reactive一样，生命周期的挂载钩子叫onMounted。
  引入后我们就可以在setup()方法里面使用onMounted挂载的钩子了。
  
  import { reactive, onMounted } from 'vue'

export default {
  props: {
    title: String
  },
  setup () {
    // ..

    onMounted(() => {
      console.log('组件已挂载')
    })

    // ...
  }
}

```
#### 9. this的指向问题

```
1. 方法函数：对象.方法() ; this->调用方法的对象；

2. 普通函数：( window.) 函数名() this->window；

3. 事件处理函数： Div.οnclick= function(){} Div.onclick() this->添加事件的元素；

4. 全局中的this指向window对象。

```

#### 10. 作用域和作用域链

【作用域】
  它是指对某一变量和函数具有访问权限的代码空间，在js中只有两种作用域
  1.全局作用域：script标签内部的区域就是全局作用域
  2.局部作用域：函数大括号内部的区域就是局部作用域
  在js中只有函数可以划分作用域，因此每个函数的大括号内部都是一个局部作用域，因此我们称局部作用域为函数作用域：
  - 全局变量 声明在全局的变量
  - 全局作用域就是全局变量起作用的范围（也就是script标签包起来的部分）
  - 局部变量 在函数内部声明的变量
  - 局部作用域就是局部变量起作用的范围
【作用域链】
  会在当前作用域查找变量，当前没有则向上一级查询。
  1. 当前有则使用当前的变量。
  ```
  var fun = function(){
    function a(){
      var a = 5;
      console.log(a); // 5
    }
    a(); //调用函数
    console.log(a); // 在fun函数中访问a变量，fun中的a函数
  }
  fun(); // 结果应该是什么？(如图展示所示)
  ```
  ![打印结果](https://user-images.githubusercontent.com/10249805/105433756-3096be00-5c95-11eb-88d4-2cbaa84c687e.png)

  首先，函数不调用不执行，所以调用了fun函数，在fun函数中，有一个函数a，调用了函数a，打印了a，调用a会执行a函数，里面var了一个a赋值为10，
  所以在函数a中打印a出的结果为10，在fun函数中打印a的结果是函数a这个函数体。
  
  2.当前没有向上一级查找变量，一直到全局作用域为止，如果还是没有会报错，xxx is not defined。
  
#### 11. 浏览器预解析变量提升

提升的对象包括：
- 函数声明；
- 变量声明；
- 函数内部作用域默认形参声明。

1. 函数声明和变量声明是同一个变量名
当函数声明和变量声明冲突的时候,变量声明无法覆盖函数声明，变量赋值可以覆盖函数声明 所以最后结果为10，具体代码：

```
a(a)  //调用函数 a = 10;  //变量
var a;  //全局变量 //或者 var a = 10;  同上面两句
function a(a) {  //函数 } console.log(a)//10

```
浏览器对js代码的预解析，这是代码执行之前的操作，也叫变量提升。函数和定义变量会被提升到当前作用域最顶端，当函数名和定义变量名字一样时，函数名会覆盖变量定义。
预解析完成后的代码：
```

上面预解析完成后是
  function a(a) { }
  a(a) //调用函数
  a = 10; //给变量a重新赋值覆盖函数体
  console.log(a) //10
```

2. 函数形参和变量声明是同一个变量
3. 
```
  a(a)  //调用函数
  a = 10;  //变量
  b=20;//变量
  var a;  //全局变量
  function a(a) {  //函数
    var a = 100;
    b=200;
    console.log(a,b)  //100  200
  }
  var b;
  console.log(a)//10
  
```
当函数调用的时候，就要进入函数的局部作用域，浏览器还要重新在局部作用域中进行预解析，变量名定义提前，赋值不会提前。
- 参数传递和函数中变量名冲突，函数形参的值会覆盖预解析的效果；
- 在函数执行之前进行预解析，这时候参数还没传递
- 预解析以后 函数内代码开始执行 传参
- 在函数中如果没有定义这个变量 就要在全局作用域中查找
- 赋值的时候函数中没有这个变量根据作用域链也会将全局这个变量的值发生改变

**【本质理解-总括】**
  JS中奇怪的一点是你可以在变量和函数声明之前使用它们。感觉上就像是变量声明和函数声明被提升了到了代码的顶部一样。
  ```
  sayHi() // Hi there!

  function sayHi() {
    console.log('Hi there!')
  }

  name = 'John Doe'
  console.log(name)   // John Doe 
  var name
  ```
  然而JavaScript并不会移动你的代码，所以JavaScript中“变量提升”并不是真正意义上的“提升”。
  JavaScript是单线程语言，所以执行肯定是按顺序执行。但是并不是逐行的分析和执行，而是一段一段地分析执行，会先进行编译阶段然后才是执行阶段。
  在编译阶段阶段，代码真正执行前的几毫秒，会检测到所有的变量和函数声明，所有这些函数和变量声明都被添加到JavaScript数据结构内的内存中。所以
  这些变量和函数能在它们真正被声明之前使用。
**【本质理解-函数提升】**

```
  sayHi() // Hi there!

  function sayHi() {
      console.log('Hi there!')
  }
```

因为函数声明在编译阶段会被添加到词法环境（Lexical Environment）中，当JavaScript引擎遇到sayHi()函数时，它会从词法环境中找到这个函数并执行它。
**【本质理解-var变量提升】**

```
  console.log(name)   // 'undefined'
  var name = 'John Doe'
  console.log(name)   // John Doe
```

上面的代码实际上分为两个部分：
- var name表示声明变量name
- = 'John Doe'表示的是为变量name赋值为'John Doe'。
- 
```
  var name    // 声明变量
  name = 'John Doe' // 赋值操作
```

只有声明操作var name会被提升，而赋值这个操作并不会被提升，但是为什么变量name的值会是undefined呢?
原因是当JavaScript在编译阶段会找到var关键字声明的变量会添加到词法环境中，并初始化一个值undefined，在之后执行代码到赋值语句时，会把值赋值到这个变量。
而let和const声明的变量，是存放在一个暂时性死区（dead zone）中，不会进行undefined的初始化，所以就会导致提前访问该变量时出现typeError，看起来像没有
变量提升一样。

  
#### 13. 手写call, apply以及bind函数

  首先了解一下三者的作用以及他们区别<br>
  1. [call, apply, bind的作用和区别](https://juejin.cn/post/6844903866358562824)
  2. [this, apply, call, bind](https://juejin.cn/post/6844903496253177863)
  
首先了解一下这三者的关系和区别：
```
相同点：
  它们都是用来改变函数的执行上下文的。Javascript中一大特点是：函数存在【定义时上下文】、【运行时上下文】以及【上下文是可以改变的】这样的概念。
不同点：
1. call和apply都是为了改变某个函数运行时的上下文而存在的，换句话说就是为了改变函数体内部this的指向。
  比如：
  function fruits() {}
  fruits.prototype = {
    color: 'red',
    show: function() {
      console.log('My color is: ' + this.color);
    }
  };
  var apple = new fruits;
  apple.show(); // My color is red
2. bind：我们一般说的绑定函数就是由bind来创建的
```
  
- call函数实现

**作用**

call和apply都是为了改变某个函数运行时的上下文（context）而存在的，换句话说，就是为了改变函数体内部this的指向。

**实现步骤**

1.判断调用对象是否为函数，即使我们是定义在函数原型上的，但是可能出现使用call等方式调用的情况。
2.判断传入上下文对象是否存在，如果不存在，则设置为window;
3.处理传入的参数，截取第一个参数后的所有参数；
4.将函数作为上下文对象的一个属性；
5.使用上下文对象来调用这个方法，并保存返回结果；
6.删除刚才新增的属性。
7.返回结果。
8.
```
Function.prototype.myCall = function(context) {
  // 判断调用对象
  if (typeof this!== "function") {
    console.error("type error");
  }
  
  // 获取参数
  let args = [...arguments].slice(1);
  let result = null;
  
  // 判断context是否传入，如果未传入则设置为window
  context = context || window;
  
  // 将调用函数设为对象的方法
  context.fn = this;
  
  // 调用函数
  result = context.fn(...agrs);
  
  // 将属性删除
  delete context.fn;
  
  return result;
  
}
```
- apply函数实现

**作用**<br>call和apply都是为了改变某个函数运行时的上下文（context）而存在的，换句话说，就是为了改变函数体内部this的指向。<br>
**实现步骤**<br>
1.判断调用对象是否为函数，即使我们是定义在函数的原型上的，但是可能出现使用 call 等方式调用的情况。
2.判断传入上下文对象是否存在，如果不存在，则设置为 window;
3.将函数作为上下文对象的一个属性。
4.判断参数值是否传入;
5.使用上下文对象来调用这个方法，并保存返回结果;
6.删除刚才新增的属性;
7.返回结果。
```
Function.prototype.myApply = function(context) {
  // 判断调用对象是否为函数
  if (typeof this !== "function") {
    throw new TypeError("Error");
  }
  
  let result = null;
  
  //判断context是否存在，如果未传入则为window
  context = context || window;
  
  //将函数设为对象的方法
  context.fn = this;
  
  // 调用方法
  if (arguments[1]) {
    result = context.fn(...arguments[1]);
  } else {
    result = context.fn();
  }
  
  // 将属性删除
  delete context.fn;
  
  return result;
}
```
- bind函数实现

**作用**<br>bind()方法会创建一个新函数，称为绑定函数，当调用这个绑定函数时，绑定函数会以创建它时传入bind()方法的第一个参数作为this，传入bind()方法的第二
个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数。<br>
**实现步骤**<br>
1.判断调用对象是否为函数，即使我们是定义在函数的原型上的，但是可能出现使用 call 等方式调用的情况。
2.保存当前函数的引用，获取其余传入参数值。
3.创建一个函数返回
4.函数内部使用 apply 来绑定函数调用，需要判断函数作为构造函数的情况，这个时候需要传入当前函数的 this 给 apply 调用，其余情况都传入指定的上下文对象。
```
Function.prototype.myBind = function(context) {
  // 判断调用对象是否为函数
  if (typeof this !== "function") {
    throw new TypeError("Error");
  }

  // 获取参数
  var args = [...arguments].slice(1),
    fn = this;

  return function Fn() {
    // 根据调用方式，传入不同绑定值
    return fn.apply(
      this instanceof Fn ? this : context,
      args.concat(...arguments)
    );
  };
};
```
三者之间的比较：
```
var obj = {
    x: 81,
};

var foo = {
    getX: function () {
      return this.x;
    }
}

console.log(foo.getX.bind(obj)());  //81
console.log(foo.getX.call(obj));    //81
console.log(foo.getX.apply(obj));   //81

三个输出的都是81，但是注意看使用 bind() 方法的，他后面多了对括号。当你希望改变上下文环境之后并非立即执行，而是回调执行的时候，使用 bind() 方法。
而 apply/call 则会立即执行函数。
```

```
// 修改前
var module= {
  bind: function () {
    $btn.on('click', function () {
      console.log(this); //this指向当前执行上下文$btn
      this.showMsg(); // 当前执行上下文$btn没有showMsg()方法，无法调用
    });
  },

  showMsg: function () {
    console.log('饿了么');
  }
};

// 修改后
var module= {
  bind: function () {
    const _this = this; //将this指向的当前执行上下文module保存为_this
    $btn.on('click', function () {
      console.log(this); //this指向当前执行上下文$btn
      _this.showMsg(); // _this即module，可以调用showMsg()方法
    });
  },

  showMsg: function () {
    console.log('饿了么');
  }
};
```
**总结：**

- 1.apply、call、bind三者都是用来改变函数的this的指向的；
- 2.apply、call、bind三者第一个参数都是this要指向的调用对象，也就是想指定的上下文；
- 3.apply、call、bind三者都可以利用后续参数传参；
- 4.bind是返回对应函数，便于稍后调用；apply 、call则是立即调用。

#### 14. Vue3相比Vue2新增了哪些功能？

【参考文章】

1. [Vue2和Vue3的区别](https://www.jianshu.com/p/ad38a1f27d0f)
2. [Vue2和Vue3双向绑定的区别](https://juejin.cn/post/6844904149239201800)

- 前言

版本的升级带来的副作用就是需要更多的时间去适应新的设计理念，但升级的目的是为了更好更快的跟紧前端发展的步伐。

- 双向绑定区别

Vue2实现双向绑定原理，主要是利用Object.defineProperty来给实例data的属性添加setter和getter，并通过发布者订阅者模式(一对多的依赖
关系，当状态发生改变，它的所有依赖都将被通知)来实现响应。

这个环节中包含了三个部分：
```
1. Observer用来监听拦截data的属性为监察者；
 
3. Dep用来添加订阅者，为订阅器；

5. Watcher就是订阅者。
监察者通过Dep向Watcher发布更新消息。
```
**简单实现**

(1) 通过对set和get的拦截，在get阶段进行依赖收集，在set阶段通知该属性上所有绑定的依赖。如下所示，我们将data的value属性绑定在set和get上，通过_value来进行操作。
```
HTML:
  <input type="text" id="inputId" oninput="handleInput(this.value)">
  <div id="div"></div>

JS:
  var inputId = document.getElementById('inputId');
  var div = document.getElementById('div');
  var data = {
    value:''
  }
  var _data = {
    value:''
  }
  Object.defineProperty(_data, 'value', {
    enumerable: true,
    configurable: true,
    set: function (newValue) {
        data.value = newValue; //watcher
        div.innerText = data.value
    },
    get: function () {
        return data.value;
    }
  })
  function handleInput(value) {
    _data.value = value;
  }

如果只需要实现一个简单的双向绑定，那么上面的代码就已经实现了。
```
（2）进一步完善模拟Vue实现
```
首先我们将watcher抽出来，备用。
  function watcher(params) {
    div.innerText = inputId.value = params; // 派发watcher
  }

声明一个vm来模拟vue的实例，并初始化：
var vm = {
  //类似vue实例上的data
  data: {
      value: ''
  }, 

  // vue私有, _data的所有属性为data中的所有属性被改造为 getter/setter 之后的。
  _data: {
      value: ''
  }, 
  // 代理到vm对象上，可以实现vm.value
  value: '', 
  //value的订阅器用来收集订阅者 
  valueWatchers:[] 
}

遍历data上的属性，进行改造，如下所示：
// 利用 Object.defineProperty 定义一个属性 (eg：value) 描述符为存取描述符的属性
  Object.defineProperty(vm._data, 'value', {
    enumerable: true, //是否可枚举
    configurable: true, //是否可配置
    set: function (newValue) { //set 派发watchers
      vm.data.value = newValue; 
      vm.valueWatchers.map(fn => fn(newValue));
   },
      get: function () {  
        // 收集wachter vue中会在compile解析器中通过 显示调用 (this.xxx) 来触发get进行收集
        vm.valueWatchers.length = 0; 
        vm.valueWatchers.push(watcher); 
        return vm.data.value; 
    }
  })
    <!--直接通过显示调用来触发get进行绑定 vue中是在compile解析器中来进行这一步-->
    vm._data.value 
```
进行到这儿也已经实现了绑定，但是我们平时使用vue ，都是可以直接通过 this.xxx来获取和定义数据。那我们还需要进一步Proxy代理
```
Object.defineProperty(vm, 'value', {
  enumerable: true,
  configurable: true,
  set: function (newValue) {
      this._data.value = newValue; //借助
  },
  get: function () {
      return this._data.value; 
  }
})
这样我们就把vm._data.value 代理到vm.value上了，可以通过其直接操作了。按照官方的写法应该是：
function proxy (target, sourceKey, key) {
  Object.defineProperty(target, key, {
      enumerable: true,
      configurable: true,
      get() {
          return this[sourceKey][key];
      },
      set(val) {
          this[sourceKey][key] = val;
      }
  });
}

proxy(vm, '_data', 'value');
```
完善后的完整代码如下：
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>双向绑定简单实现</title>
</head>
<body>
<input type="text" id="inp" oninput="inputFn(this.value)">
<br>
<input type="text" id="inp2" oninput="inputFn(this.value)">
<div id='div'></div>
<script>
    var inp = document.getElementById('inp');
    var inp2 = document.getElementById('inp2');
    var div = document.getElementById('div');

    
    function inputFn(value) {
        div.innerText = vm.value = value;
    }

    function watcher(params) {
        console.log(1)
        div.innerText = inp.value = params; // 派发watcher
    }

    function watcher2(params) {
        console.log(2)

        div.innerText = inp2.value = params; // 派发watcher
    }

    function proxy (target, sourceKey, key) {
        Object.defineProperty(target, key, {
            enumerable: true,
            configurable: true,
            get() {
                return this[sourceKey][key];
            },
            set(val) {
                this[sourceKey][key] = val;
            }
        });
    }

	let handler = {
        enumerable: true,
        configurable: true,
        set: function (newValue) {
            vm.data.value = newValue; 
            vm.valueWatchers.map(fn => fn(newValue));
        },
        get: function () {
            vm.valueWatchers = []; //防止重复添加, 
            vm.valueWatchers.push(watcher); 
            vm.valueWatchers.push(watcher2); 
            return vm.data.value; 
        }
    }

    var vm = {
        data: {},
        _data: {},
        value: '', 
        valueWatchers: [] 
    }
    
    Object.defineProperty(vm._data, 'value', handler)

    proxy(vm, '_data', 'value');

    vm.value;  //显示调用绑定

</script>
</body>
</html>
```

#### 15. 什么是XSS攻击？如何防范XSS攻击？
- 概念

XSS攻击是指跨站脚本攻击，是一种代码注入攻击。攻击者通过在网站注入恶意脚本，使之在用户的浏览器上运行，从而盗取用户的信息，如cookie等。
XSS的本质是因为网站没有对恶意代码进行过滤，与正常的代码混合在一起了，浏览器没有办法分辨哪些脚本是可信的，从而导致了恶意代码的执行。
XSS一般分为存储型、反射型和DOM型。

（1）存储型

是指恶意代码提交到了网站的数据库中，当用户请求数据的时候，服务器将其拼接为HTML后返回给了用户，从而导致了恶意代码的执行。
（2）反射型

是指攻击者构建了特殊的URL，当服务器接收到请求后，从URL中获取数据，拼接到HTML后返回，从而导致了恶意代码的执行。
（3）DOM型

DOM型指的是攻击者构建了特殊的URL，用户打开网站后，js脚本从URL中获取数据，从而导致了恶意代码的执行。

- XSS攻击预防

可以从2个方面考虑预防，一个是恶意代码提交的时候，一个是浏览器执行恶意代码的时候。<br>
(1) 第一个方面：如果我们对存入数据库的数据都进行转义处理，但是一个数据可能在多个地方使用，有的地方可能不需要转义，由于我们没有办法
判断数据最后的使用场景，所以直接在输入端进行恶意代码的处理，其实是不太可靠的。因此我们可以从浏览器的执行来进行预防一种是使用纯前端
的方式，不用服务器端拼接后返回。<br>
(2) 另一种是对需要插入到HTML中的代码做好充分的转义。对于DOM的攻击，主要是前端脚本的不可靠而造成的，我们对于数据获取渲染和字符串拼
接的时候应该对可能出现的恶意代码情况进行判断。<br>
(3) 还有一些方式，比如使用CSP, csp的本质是建立一个白名单，告诉浏览器那些外部资源可以加载和执行，从而防止恶意代码的注入攻击。<br>
(4) 还可以对一些敏感信息进行保护，比如cookie使用http-only，使得脚本无法获取。也可以使用验证码，避免脚本伪装成用户执行一些操作。

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

#### 18. 原型和原型链有什么特点？

【参考文章】<br>
1. [js原型链和继承，别再被问倒了](https://juejin.cn/post/6844903475021627400)
2. [js中的__proto__和prototype关系](https://www.zhihu.com/question/34183746)

    在js中，每个构造函数(constructor)都有一个原型对象(prototype),原型对象都包含一个指向构造函数的指针,而实例(instance)都包含一个指向原型对象的内部指针.
  当我们使用构造函数新建一个对象后，在这个对象的内部将包含一个指针，这个指针指向构造函数prototype属性对应的值，在ES5中这个指针被称为对象的**原型**。
  
  一般说来我们不应该能够取到这个值得，但是现在浏览器中基本都实现了__proto__属性来让我们访问这个属性，但是我们最好不要使用这个属性，因为它不是规范
  中规定的。ES5新增的Object.getPrototypeOf()方法，使得我们可以通过这个方法来获取对象的原型。
    当我们访问一个对象的属性时，如果这个对象内部不存在这个属性，那么它就会去它的原型对象里找这个属性，这个原型对象又有自己的原型，于是就这样一直找下去，
  也就是原型链的概念。原型链的尽头一般来说都是Object.prototype,所以这就是我们新建的对象为什么能够使用toString()等方法的原因。
  
  JS对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本，当我们修改原型，与之相关的对象也会继承这一改变。
  
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



