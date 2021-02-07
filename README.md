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
- [8. Vue3和Vu2之间有什么区别？](#8-Vue3和Vu2之间有什么区别)
- [9. this的指向问题](#9-thisthis的指向问题)
- [10. 作用域和作用域链](#10-作用域和作用域链)
- [11. 浏览器预解析变量提升](#11-浏览器预解析变量提升)
- [12. js中的深浅拷贝实现？](#12-js中的深浅拷贝实现) 
- [13. 手写call, apply以及bind函数](#13-手写call-apply以及bind函数)
- [14. Vue3相比Vue2新增了哪些功能？](#14-Vue3相比Vue2新增了哪些功能)
- [15. 什么是XSS攻击？如何防范XSS攻击？](#15-什么是XSS攻击如何防范XSS攻击)
- [16. 什么是CSP？](#16-什么是CSP)
- [17. 什么是CSRF攻击？如何防范CSRF攻击？](#17-什么是CSRF攻击如何防范CSRF攻击)
- [18. 原型和原型链有什么特点？](#18-原型和原型链有什么特点)


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

这是几乎每场面试时面试官都会问到的问题，所以重要性可以毫无疑问的说排第一。

- 栈：基本数据类型（Undefined, Null, Boolean, Number, String, Symbol, BigInt）
- 堆：引用数据类型（Object, Array，Function）
以上两种类型的区别是：存储位置不同。
1. 基本数据类型直接存储在栈（Stack）中的简单数据段，占据空间小，大小固定且是频繁使用的数据。
2. 引用数据类型存储在堆（Heap）中的对象，占据空间大，大小不固定。但是如果存储在栈中，将会影响程序运行的性能；引用数据
  类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器找到引用值时，首先检索其在栈中的地址，取得内存地址后
  从堆中获得实体。

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
#### 6. 什么是闭包，为什么要用它？

**【参考文章】**<br>
1. [如何更好的理解Javascript闭包](https://www.zhihu.com/question/31383111)
2. [我从来不理解 JavaScript 闭包，直到有人这样向我解释它...](https://blog.fundebug.com/2019/02/12/understand-javascript-closure/)

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
  
  instanceof 是用来判断 A 是否为 B 的实例，表达式为：A instanceof B，如果 A 是 B 的实例，则返回 true,否则返回 false。 在
  这里需要特别注意的是：instanceof 检测的是原型。
  instanceof (A, B) {
    let a = A.__proto__;
    let b = B.prototype;
    if (a === b) {  // A的内部属性 __proto__ 指向 B 的原型对象
    return true;
    }
  return false;
  }
  例子：
  [] instanceof Array; // true
  [] instanceof Object; // true
  newDate() instanceof Date;// true
  newDate() instanceof Object;// true
  虽然 instanceof 能够判断出 [ ] 是Array的实例，但它认为 [ ] 也是Object的实例，为什么呢？
  
  从 instanceof 能够判断出 [ ].__proto__  指向 Array.prototype，而 Array.prototype.__proto__ 又指向了Object.prototype，
  最终 Object.prototype.__proto__ 指向了null，标志着原型链的结束。因此，[]、Array、Object 就在内部形成了一条原型链：
  从原型链可以得出结论，[] 的 __proto__  直接指向Array.prototype，间接指向 Object.prototype，所以按照 instanceof 的判断规则，[]
  就是Object的实例。依次类推，类似的 new Date()也会形成一条对应的原型链 。因此，instanceof 只能用来判断两个对象是否属于实例关系， 
  而不能判断一个对象实例具体属于哪种类型。
  **问题**
  instanceof 操作符的问题在于，它假定只有一个全局执行环境。如果网页中包含多个框架，那实际上就存在两个以上不同的全局执行环境，从而存
  在两个以上不同版本的构造函数。如果你从一个框架向另一个框架传入一个数组，那么传入的数组与在第二个框架中原生创建的数组分别具有各自不
  同的构造函数。
  
  variframe = document.createElement('iframe');
  document.body.appendChild(iframe);
  xArray = window.frames[0].Array;
  vararr = newxArray(1,2,3); // [1,2,3]
  arr instanceof Array; // false
  针对数组的这个问题，ES5 提供了 Array.isArray() 方法 。该方法用以确认某个对象本身是否为 Array 类型，而不区分该对象在哪个环境中创建。
  Array.isArray() 本质上检测的是对象的内部属性 [[Class]] 值，里面包含了对象的类型信息，其格式为 [object Xxx]，Xxx 就是对应的具体类
  型。对于数组而言，[[Class]] 的值就是 [object Array] 。
 
（3）constructor

  当一个函数Func被定义时，JS引擎会为Func添加 prototype 原型，然后再在 prototype 上添加一个 constructor 属性，并让其指向 Func 的引用。如下所示：
  
  ![捕获](https://user-images.githubusercontent.com/10249805/104984352-82e39f00-5a49-11eb-9fc0-252aa5105a4d.PNG)
  
  <br>当我们执行let f = new Func()时，Func被当成了构造函数，f是Func的实例对象，此时Func原型上的constructor传递到了f上，因此f.constructor === Func.
  
  ![捕获](https://user-images.githubusercontent.com/10249805/104984691-3187df80-5a4a-11eb-948a-d57bed6a4c9e.PNG)
  
  <br>可以看出的是：Func利用对象上的constructor引用了自身，当Func作为构造函数来创建对象时，原型上的constructor就被遗传到新创建的对象上了，从原型链角
  度来讲，构造函数Func就是新对象的类型。这样做的意义是，让新对象在诞生以后，就具有可追溯的数据类型。
  
  **注意：**
  
  - null 和 undefined 是无效的对象，因此是不会有 constructor 存在的，这两种类型的数据需要通过其他方式来判断。

  - 函数的 constructor 是不稳定的，这个主要体现在自定义对象上，当开发者重写 prototype 后，原有的 constructor 引用会丢失，constructor 会默认为 Object,
  为什么会变成Object呢？
  
  因为 prototype 被重新赋值的是一个 { }， { } 是 new Object() 的字面量，因此 new Object() 会将 Object 原型上的 constructor 传递给 { }，也就是 Object
  本身。因此，为了规范开发，在重写对象原型时一般都需要重新给 constructor 赋值，以保证对象实例的类型不被篡改。
  
  ```
  ''.constructor == String
  new Number(5).constructor == Number
  true.constructor == Boolean
  ```

（4）Object.prototype.toString.call()
  
#### 8. Vue3和Vu2之间有什么区别？

我们首先关注一下Vue3.0与Vue2.x的一些最主要的区别。

- 双向绑定实现的区别
【参考文章】<br>
1. [Vue2和Vue3双向数据绑定的区别](https://juejin.cn/post/6844904045237272583)

【Vue2.x】<br>
```
Vue2.x采用es5中的Object.defineproperity()来实现双向绑定。
```

【Vue3.0】<br>
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
```
  var name    // 声明变量
  name = 'John Doe' // 赋值操作
```
只有声明操作var name会被提升，而赋值这个操作并不会被提升，但是为什么变量name的值会是undefined呢?
原因是当JavaScript在编译阶段会找到var关键字声明的变量会添加到词法环境中，并初始化一个值undefined，在之后执行代码到赋值语句时，会把值赋值到这个变量。
而let和const声明的变量，是存放在一个暂时性死区（dead zone）中，不会进行undefined的初始化，所以就会导致提前访问该变量时出现typeError，看起来像没有
变量提升一样。

#### 12. js中的深浅拷贝实现？

参考文章：<br>
1. [js的深拷贝和浅拷贝](https://www.cnblogs.com/Renyi-Fan/p/12677015.html)
2. [js深拷贝 VS 浅拷贝](https://juejin.cn/post/6844903493925371917)

深拷贝和浅拷贝本质上来说都是针对引用型数据来说的。因为浅拷贝拷贝对象的一层，深拷贝是拷贝对象的所有层。
JavaScript存储对象都是存地址的，所以浅拷贝会导致 obj1 和obj2 指向同一块内存地址。改变了其中一方的内容，都是在原来的内存上做修改会导致拷贝对象和源对象都发生改变，
而深拷贝则是开辟一块新的内存地址，将原对象的各个属性逐个复制进去。对拷贝对象和源对象各自的操作互不影响。

- 浅拷贝实现
指的是将一个对象的属性值复制到另外一个对象，如果有的属性的值为引用类型的话，那么会将这个引用的地址复制给对象，因此两个对象会有同一个引用类型的引用。浅
拷贝可以使用Object.assign()和展开运算符来实现(如：const {a, b, c} = {1, 2, {3, 4}}; 所以c = {3, 4})。

如何实现一个对象或者数组的浅拷贝。
想一想，好像很简单，遍历对象，然后把属性和属性值都放在一个新的对象不就好了~

```
function shallowCopy(object) {
  // 只拷贝对象
  if (!object || typeof object !== "object") {
    return;
  }
  // 根据object的类型判断是新建一个数组还是对象
  let newObject = Array.isArray(object) ? [] : {};
  
  // 遍历object，并且判断是object的属性才拷贝
  for (let key in object) {
    if (object.hasOwnProperty(key)) {
      newObject[key] = object[key];
    }
  }
  return newObject;
}
```
- 深拷贝实现
相对于浅拷贝而言，如果遇到属性值为引用类型的时候，它新建一个引用类型并将对应的值复制给它，因此对象获得的一个新的引用类型而不是一个原有类型的引用。深拷贝
对于一些对象可以使用JSON的两个函数来实现，但是由于JSON的对象格式化比js的对象格式化更加严格，所以如果属性值里面出现函数或者Symbol类型的值时，会转换失败。

那如何实现一个深拷贝呢？说起来也简单，我们在拷贝的时候判断一下属性值的类型，如果是对象，我们递归调用深拷贝函数不就好了~

```
function deepCopy(object) {
  if (!object || typeof object !== "object")  return;
    let newObject = Array.isArray(object) ? [] : {};
    
    for (let key in object) {
      if (object.hasOwnProperty(key)) {
        newObject[key] = typeof object[key] === "object" ? deepCopy(object[key]) : object[key];
    }
  }
  
  return newObject;
}
```
**【思考：性能问题】**<br>
  尽管使用深拷贝会完全克隆一个新对象，不会产生副作用，但是深拷贝使用了递归，性能会不如浅拷贝，在开发中，还是要根据实际情况选择。

**【JSON对象的parse和stringify】**<br> 
  JSON对象是ES5中引入的新的类型（支持的浏览器为IE8+），JSON对象parse方法可以将JSON字符串反序列化成JS对象，stringify方法可以将JS对象序列化成JSON字符串，
  借助这两个方法，也可以实现对象的深拷贝。
  ```
  //例1
  var source = { name:"source", child:{ name:"child" } } 
  var target = JSON.parse(JSON.stringify(source));
  target.name = "target";  //改变target的name属性
  console.log(source.name); //source 
  console.log(target.name); //target
  target.child.name = "target child"; //改变target的child 
  console.log(source.child.name); //child 
  console.log(target.child.name); //target child
  //例2
  var source = { name:function(){console.log(1);}, child:{ name:"child" } } 
  var target = JSON.parse(JSON.stringify(source));
  console.log(target.name); //undefined
  //例3
  var source = { name:function(){console.log(1);}, child:new RegExp("e") }
  var target = JSON.parse(JSON.stringify(source));
  console.log(target.name); //undefined
  console.log(target.child); //Object {}
  ```
  这种方法使用较为简单，可以满足基本的深拷贝需求，而且能够处理JSON格式能表示的所有数据类型，但是对于正则表达式类型、函数类型等无法进行深拷贝(而且会直接丢失相应的值)。
还有一点不好的地方是它会抛弃对象的constructor。也就是深拷贝之后，不管这个对象原来的构造函数是什么，在深拷贝之后都会变成Object。同时如果对象中存在循环引用的情况也无法
正确处理。
  
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

**作用**<br>call和apply都是为了改变某个函数运行时的上下文（context）而存在的，换句话说，就是为了改变函数体内部this的指向。<br>
**实现步骤**<br>
1.判断调用对象是否为函数，即使我们是定义在函数原型上的，但是可能出现使用call等方式调用的情况。
2.判断传入上下文对象是否存在，如果不存在，则设置为window;
3.处理传入的参数，截取第一个参数后的所有参数；
4.将函数作为上下文对象的一个属性；
5.使用上下文对象来调用这个方法，并保存返回结果；
6.删除刚才新增的属性。
7.返回结果。
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
  










## CSS
| 题目         | 大概内容                    |
| ------------ | -------------------------- |
| CSS常见面试题 | 垂直居中方式，双栏/三栏布局方式，header+main+footer布局|

## HTML


## Vue框架



## Webpack性能优化

### 目录

- [1. 前端性能优化](#1-前端性能优化)


#### 1. 前端性能优化
参考文章[前端性能优化-webpack](https://juejin.cn/post/6911472693405548557)



