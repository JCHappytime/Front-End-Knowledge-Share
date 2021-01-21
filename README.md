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
- [8. Vue3.x和Vu2.x之间有什么区别？](#8-Vue3.x和Vu2.x之间有什么区别)



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
  
#### 8. Vue3.x和Vu2.x之间有什么区别？

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

## CSS
| 题目         | 大概内容                    |
| ------------ | -------------------------- |
| CSS常见面试题 | 垂直居中方式，双栏/三栏布局方式，header+main+footer布局|

## HTML


## Vue框架
