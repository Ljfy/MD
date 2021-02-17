### 一、JavaScript基础

#### 变量和类型

#### 1、JavaScript规定了几种数据类型

`js`目前共定义了8中数据类型，其中包括:`undefined`、`Null`、`Boolean`，`Number`、`String`、`Object`、`Symbol`、`BigInt`

 ####  2、JavaScript对象的底层数据结构是什么?

`JavaScript`基本数据类型数据都是直接存储在栈中(`undefined`、`Null`、不是`new出来的布尔`、数字和字符串)，每种类型的数据占用的内存空间的大小是确定的并由系统自动分配和自定释放。这样带来的好处就是，内存可以及时得到回收，相对于堆来说，更加容易管理内存空间。

`JavaScript`引用数据类型被存储与堆中(如对象、数组、函数等，它们都是通过拷贝和`new`出来的)。其实，说存储与堆中，也不太准确，因为，引用类型的数据指针是储存与栈中的，当我们想要访问引用类型值的时候，需要先从栈中获得对象的地址指针，然后通过地址指针找到堆中所需要的数据。

#### 3.Symbol类型在实际开发中的应用、可手动实现一个简单的Symbol

#### 4.JavaScript中的变量在内存中的具体存储形式

基本类型时保存在栈内存中的简单数据段，他们的值都有固定大小，保存在栈空间，通过按值访问

引用类型时保存在堆内存中的对象，值大小不固定，栈内存中存放的该对象的地址指向堆内存中的对象，`JavaScript`不允许直接访问堆内存中的位置，因此操作对象时，实际操作的是对象的引用

```js
let a1 = 1;//栈内存
let a2 = 'hehe';//栈内存
let a3 = null;//栈内存
let b = {x:10};//变量b存与栈中，{x：10}作为对象存于堆中
let c = {1,2,3};//变量c存与栈中,{1,2,3}作为对象存在于堆中
```

#### 5.基本类型对应的内置对象，以及他们之间的装箱拆箱操作

#### 6.理解值类型和引用类型

#### 7.null和undefined的区别

`null`表示没有对象，即该处不应该有值。典型用法是:

1、作为函数的参数，表示该函数的参数不是对象。

2、作为对象原型链的终点

`undefined`表示缺少值，就是此处应该有一个值，但是还没有定义。典型用法是:

1、变量被声明了，但没有赋值时，就等于`undefined`

2、调用函数时，应该提供的参数没有提供，该参数等于`undefined`

3、对象没有赋值的属性，该属性的值为`undefined`

4、函数没有返回值时，默认返回`undefined`

#### 8.至少可以说出三种判断JavaScript数据类型的方式，以及他们的优缺点，如何准确的判断数组类型

1、typeof(可以对基本类型做出准确的判断，但对于引用类型，用它就力不从心了)

`typeof`返回一个表示数据类型的字符串，返回结果包括`number`、`boolean`、`string`、`object`、

`undefined`、`function`等6中数据类型。

**2、instanceof**

`instanceof`是用来判断A是否为B的实例时，表达式为A instanceof B，如果A是B的实例，则返回true,否则为false，instanceof检测的是原型

**3、Object.prototype.toString **

`toString`是`Object`原型对象上的一个方法，该方法默认返回其调用者的具体类型，更严格的讲，是`toString`运行时`this`指向的对象类型，返回的类型格式为[object,xxx]xxx是具体的数据类型，其中包括`String`、`Number`,`Boolean`,`undefined`、`null`,`function`、`date`、`array`、`Error`、`HTML`基本上所有的对象的类型都可以通过这个方法获取到.

`constructor	`查看对象对应的构造函数`construvtor`在对应对象的原型下面，是自动生成的，当我们写一个构造函数的时候，程序自动添加，构造函数名.prototype.constructor = 构造函数名	

#### 9.可能发生隐式类型转换的场景以及转换原则，应如何避免或巧妙应用

#### 10.出现小数精度丢失的原因，JavaScript可以存储的最大数字、最大安全数字，JavaScript处理大数字的方法、避免精度丢失的方法

### 原型和原型链

1、`instanceof`的底层原理，手动实现一个`instanceof`

2、实现继承的几种方式以及他们的优缺点

3、可以描述new一个对象的详细过程，手动实现一个`new`操作符

4、理解Es6 class构造以及继承的底层实现原理

### 作用域和闭包

1、理解词法作用域和动态词法作用域

2、理解`JavaScript`的作用域和作用域链

### 执行机制

### 语法和API

1、理解`ECMAScript`和`JavaScript`的关系

前者是后者的规格，后者是前者的一种实现

2、`setInterval`需要注意的点使用`settimeout`实现setinterval

```js
function mysetInterval(fn,mil){
    function interval(){
        setTimeout(interval,mil);
        fn();
    }
    setTimeout(interval,mil)
}
mysetInterval(function(){
    console.log(1);
},1000)
```

3、什么是防抖和节流，有什么区别？如何实现

防抖就是n时间内函数只会执行一次，如果n时间内多次触发则会重新计算时间

```js
function debounce(fn){
    let timeout = null;
    return function(){
        clearTimeout(timeout);
        timeout = setTimeout(function(){
            fn.apply(this.arguments)
        },500)
    }
}
function say(){
    conosle.log('防抖')
}

var input = document.querySelector('hello');
input.addEventListener('input',debounce(say));
```

节流n时间内只会执行一次

```js
function throttle(fn){
    let chang = true;
    return function(){
        if(!chang) return;
        chang = false;
        setTimeout(()=>{
            fn.apply(this.arguments);
            chang = true;
        },1000)
    }
}
function say(){
    console.log('节流',new Date())
}
var myinput = document.getElementById('hee');
myinput = addEventListener('input',throttle(say))
```

4、介绍下Set、Map、WeakSet和WeakMap的区别

`WeakSet`结构和`Set`类似，也是不重复的值的集合,但是，它与`set`有两个区别

- `WeakSet`的成员只能是对象，而不能是其他类型的值
- `WeakSet`中的对象都是弱引用，即垃圾回收机制不考虑`WeakSet`对该对象的引用也就是说,,如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在`WeakSet`之中

### HTML和CSS

1、从规范的角度理解HTML,从分类和语义的角度使用标签

2、常用页面标签的默认样式、自带属性、不同浏览器的差异、处理浏览器兼容问题的方式

3、元信息类标签(head,title,meta)的使用目的和配置方法

4、HTML离线缓存原理

5、可以使用`Canvas`API、`SVG`等绘制高性能的动画

### CSS

1、CSS和模型，在不同浏览器的差异

2、CSS所有选择器及其优先级、使用场景,哪些可以继承，如何运用@规则

3、CSS伪类和伪元素有哪些，他们的区别和实际应用

4、4.HTML文档流的排版规则，CSS几种定位的规则、定位参照物、对文档流的影响，如何选择最好的定位方式，雪碧图实现原理

5、水平居中的方案、可以实现6种以上并对比它们的优缺点

6.BFC实现原理，可以解决的问题，如何创建BFC

7.可使用CSS函数复用代码，实现特效效果

8.PostCSS、Sass、Less的异同，以及使用配置，至少掌握一种

9.CSS模块化方案、如何配置按需加载、如何防止CSS阻塞渲染

10.熟练使用CSS实现常见动画，如渐变、移动、旋转、缩放等等

11.CSS浏览器兼容性写法，了解不同API在不同浏览器下的兼容性情况

12.掌握一套完整的响应式布局方案

### 三、计算机基础

**编译原理**

#### 1.理解代码到底是什么，计算机如何将代码转换为可以运行的目标程序

#### 2.正则表达式的匹配原理和性能优化

#### 3.如何将JavaScript代码解析成抽象语法树(AST)

#### 4.base64的编码原理

#### 5.几种进制的相互转换计算方法，在JavaScript中如何表示和转换

### 网络协议

#### 1.理解什么是协议，了解TCP/IP网络协议族的构成，每层协议在应用程序中发挥的作用

#### 2.有哪些协议是可靠，TCP有哪些手段保证可靠交付

#### 3.DNS的作用、DNS解析的详细过程，DNS优化原理

#### 4.CDN的作用和原理

#### 5.HTTP请求报文和响应报文的具体组成，能理解常见请求头的含义，有几种请求方式，区别是什么

#### 6.HTTP所有状态码的具体含义，看到异常状态码能快速定位问题

#### 7.HTTP1.1、HTTP2.0带来的改变

#### 9.理解WebSocket协议的底层原理、与HTTP的区别

## 四、数据结构和算法

### JavaScript编码能力

#### 1.多种方式实现数组去重、扁平化、对比优缺点

#### 2.多种方式实现深拷贝、对比优缺点

#### 3.手写函数柯里化工具函数、并理解其应用场景和优势

#### 4.实现一个sleep函数

### 手动实现前端轮子

#### 1.手动实现call、apply、bind

#### 2.手动实现符合Promise/A+规范的Promise、手动实现async await

#### 3.手写一个EventEmitter实现事件发布、订阅

#### 6.手写一个模版引擎，并能解释其中原理

#### 7 .手写懒加载、下拉刷新、上拉加载、预加载等效果

### 数据结构

#### 1.理解常见数据结构的特点，以及他们在不同场景下使用的优缺点

#### 2.理解数组、字符串的存储原理，并熟练应用他们解决问题

#### 3.理解二叉树、栈、队列、哈希表的基本结构和特点，并可以应用它解决问题

#### 4.了解图、堆的基本结构和使用场景

### 算法

#### 1.可计算一个算法的时间复杂度和空间复杂度，可估计业务逻辑代码的耗时和内存消耗

#### 2.至少理解五种排序算法的实现原理、应用场景、优缺点，可快速说出时间、空间复杂度

#### 3.了解递归和循环的优缺点、应用场景、并可在开发中熟练应用

#### 4.可应用回溯算法、贪心算法、分治算法、动态规划等解决复杂问题

#### 5.前端处理海量数据的算法方案


