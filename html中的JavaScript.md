### html中的JavaScript

**`<script>`**元素有下列八个属性。

- `async`：可选。表示应该立即开始下载脚本，但不能阻止其他页面动作,比如下载资源或等待其他脚本加载。只对外部脚本文件有效。
- `charset`：可选。使用`src`属性指定的代码字符集。很少使用。
- `crossorigin`：可选。配置相关请求的`CORS`(款与资源共享)设置。默认不使用`CORS`
- `defer`：可选。表示在文档解析和显示完成后在执行脚本是没有问题的，只对外部脚本有效
- `integrity`：可选。允许比对接收到的资源和指定的加密签名已验证子资源的完整性.如果接收到的资源签名不匹配,则报错。
- `language`：废弃
- `src`：可选。表示可执行的外部文件
- `type`:可选表示代码块中脚本语言的内容类型(也称MIME)类型

`<script>`元素的最为强大,同时也备受争议的特性是它可以包含来自外部域的`javascript`文件,跟`<img>`很像`<script>`元素的`src`属性可以是一个完整的`url`,而且这个`URL`指向的资源可以跟包含它的HTML页面不在同一个域中。比如:

```html
<script src="http://www.aiuiu.cn;"></script>
```

浏览器在解析这个资源时,会像`src`属性指定的路径发送一个`GET`请求,取得相应的资源,假定一个`javascript`文件,这个初始的请求不受浏览器同源策略限制,但返回并被执行的js则受限制

**标签占位符**

`<script>放到<head>`标签内,意味着必须把所有的js代码都下载、解析和解释完成后执行,才开始渲染页面,页面在浏览器解析到`<body>`的起始标签时开始渲染,对于很多Js的页面,会导致渲染明显延迟,在此期间页面完全空白。解决这个问题的方案就是:有js引用的放在`<body>`元素的页面内容后面。

**推迟执行脚本**

`defer`表示脚本执行的时候不会改变页面的结构,可以在整个页面解析完成以后在运行,在`<script>`元素上设置`defer`属性。下载立即开始,但执行应该推迟

```html
<script defer src="a.js"></script>
<script defer src="b.js"></script>
<body></body>
```

`HTML5`规范要求脚本应该按照它们的顺序执行。第一个脚本会在第二个推迟的脚本之前执行。

实际中不一定按照顺序。

**异步执行脚本**

`async`与`defer`类似不同的是,标记为`async`的脚本并不能保证按照它们出现的顺序执行

**<noscript>**元素

针对早期浏览器不支持Javascript的问题,需要一个页面优雅降级的处理方案。`<noscript>`元素出现,被用于不给支持的`javascript`的浏览器提供替代内容,对于禁用javascript浏览器,这个元素还是有用的。

`<noscript>`元素可以包含任何可以出现在`<body>`中的HTML元素,下列情况,浏览器将显示包含在`<noscript>`中的内容:

- 浏览器不支持脚本
- 浏览器对脚本的支持被关闭

任何一个条件满足.都会被渲染

```html
<noscript>
    <p>不可用时出现的内容</p>
</noscript>
```

- 要包含外部`js`文件,必须将`src`属性设置为要包含文件的`URL`,可以在不同的域中。
- 所有`<script>`元素会依照它们在网页中出现的次序被解释。在不使用`defer`和`async`属性的情况下，包含`<script>`元素中的代码必须严格按次序解释。
- 对不推迟执行的脚本,浏览器必须解释完位于`<script>`元素中的代码,然后才能继续渲染页面的剩余部分,通常应该把`<script>`元素放在末尾,介于主内容之后及`</body>`之前
- 可以使用`defer`属性把脚本推迟文档渲染完毕后再执行。推迟的脚本总是按照它们被列出的次序执行。
- 可以使用`async`属性表示脚本不需要等待其它脚本,同时也不阻塞文档渲染,即异步加载。异步加载不能保证按照它们在页面中出现的次序。
- 通过使用`<noscript>`元素,可以指定在浏览器不支持脚本时显示的内容。如果浏览器支持并启用`JavaScript`,则`<noscript>`元素中的任何内容都不会被渲染。

### JavaScript中的严格和非严格模式

### 严格模式

`ECMAScript`增加了严格模式,严格模式是一种不同的`JavaScript`解析和执行模型。

严格模式在`IE`以上版本的浏览器才会被支持,旧版本浏览器中会被忽略。

严格模式对正常的`JavaScript`语义做了一些修改：

1、消除`JavaScript`语法的一些不合理、不严谨之处、减少了一些怪异行为。

2、消除代码运行的一些不安全之处、保证代码运行进行的安全。

3、提高编译效率,增加运行速度。

4、禁用了`JavaScript`的未来版本中可能定义的一些语法,为未来新版本的`JavaScript`做好铺垫。比如一些保留字如:`class`、`import`、`export`不能作为变量名。

### 开启严格模式

`"use strict"`为整个脚本开启严格模式。`IE10`以前的版本会当成字符串

```js
(function(){
    'use strict'
})
//为某个函数开启严格模式
function fn(){
    'use strict'
    //按照严格模式进行
}
function fun(){
    
}
```

**严格模式中的变化**

```js
//非严格模式
num = 10;
console.log(num); //10
//严格模式
"use strict"
num = 10;
console.log(num); //num is not defined
let num = 10;
console.log(num);//10
delete num;
console.log(num);//Delete of an unqualified identifier in strict mode.
"user strict"
function fn(){
    console.log(this);//undefined
}
fn();
//非函数的代码块
'use strict'
if(true){
    function f(){}//语法错误
    f();
    for(var i = 0;i < 5;i++){
        function f2(){}//错误
    }
}
```

严格模式:

- 变量名必须先声明在使用
- 不能随意删除已经声明好的变量
- 严格模式下全局作用域中函数中的this是`undefined`，以前指向的是`window`
- 以前的构造函数不加`new`也可以调用,当普通函数,`this`指向全局对象
- 严格模式下如果构造函数不加`new`调用,`this`会报错
- `new`实例化的构造函数指向创建的对象实例
- 定时器`this`还是指向`window`
- 事件、对象还是调用者
- 函数不允许参数同名
- 函数必须声明在顶层,会引入块级作用域,不允许在非函数的代码块内声明函数。



