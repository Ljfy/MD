### JavaScript深入之原型到原型链

#### 构造函数创建对象

```js
function Person(){
    
}
var person = new Person();
person.name = 'Ljfy';
console.log(person.name);
```

在这个例子中,`Person`就是一个构造函数，我们使用`new`创建了一个实例对象`person`

**prototype**

只有函数才有`prototype`属性，就是我们经常在各种例子中看到的那个`prototype`

```js
function Person(){
    
}
Person.prototype.name = 'Ljfy';
var person1 = new Person();
var person2 = new Person();
console.log(person1.name);//Ljfy
console.log(person2.name);//Ljfy
```

那么这个函数的`prototype`属性指向的是什么呢?是这个函数的原型吗？

其实,函数的`prototype`属性指向了一个对象，这个对象正是构造函数而创建的实例的原型，也就是这个例子中的`person1`、`person2`的原型

那么什么是原型呢?可以这样理解：每一个`JavaScript`对象(null除外)在创建的时候就会与之关联一个对象，这个对象就是我们说的原型,每一个对象都会从原型继承属性。

![构造函数和实例原型的关系图](https://github.com/mqyqingfeng/Blog/raw/master/Images/prototype1.png)

在这张图中我们用`Object.prototype`表示实例原型。

那么该怎么表示实例与实例原型，也就是`person`和`Person.prototype`之间的关系的呢？

`__proto__`

这是每一个`js`对象(除了null)都具有的一个属性，叫`__proto__`,这个属性会指向该对象的原型

```js
function Person(){
    
}
var person = new Person();
console.log(person.__proto__ === Person.prototype);//true
```

更新一下关系图

![实例与实例原型的关系图](https://github.com/mqyqingfeng/Blog/raw/master/Images/prototype2.png)

既然实例对象和构造函数都可以指向原型，那么原型是否有属性指向构造函数或者实例呢?

`constructor`

指向实例倒是没有，因为一个构造函数可以生成多个实例，但是原型指向构造函数倒是有的，

每一个原型都有一个`constructor`属性指向关联的构造函数

```js
function Person(){
    
}
console.log(Person === Person.prototype.constructor);//true
```

更新一下关系图

![实例原型与构造函数的关系图](https://github.com/mqyqingfeng/Blog/raw/master/Images/prototype3.png)

综上得出

```js
function Person(){
    
}
var person = new Person();
console.log(person.__proto__ == Person.prototype);//true
console.log(Person.prototype.constructor== Person);//true
//获得对象的原型
console.log(Object.getPrototypeOf(person)===Person.prototype);//true
```

**实例与原型**

当读取实例的属性时，如果找不到，就会查找与对象关联的原型中的属性，如果还查不到，就去找原型的原型，一直找到最顶层为止。

```js
function Person(){
    
}
Person.prototype.name = 'Ljfy';
var person = new Person();
person.name = new Person();
console.log(person.name);//Ljfy
delete person.name;
console.log(person.name)
```

在这个例子中，我们给实例对象`person`添加了`name`属性，当我们打印`person.name`的时候，结果自然为ljfy

当我们删除了`person`的name属性时，读取了`person.name`从person对象找不到`name`属性就会从`person`的原型也就是`person.__proto__`,也就是`Person.prototype`中查找，幸运的是我们找到了name属性，结果为ljfy

但是万一没找到呢？原型的原型又是什么呢？

**原型的原型**

原型也是一个对象，既然是对象，我们就可以用原始的方式创建它，那就是;

```js
var obj = new Object();
obj.name = 'ljfy';
console.log(obj.name);//ljfy
```

所以原型对象是通过`Object`构造函数生成的，结合之前所讲，实例的`__proto__`指向构造函数的`prototype`在次更新关系图

![](https://github.com/mqyqingfeng/Blog/raw/master/Images/prototype4.png)

**原型链**

那么`Object.prototype`的原型呢?

null？

```js
console.log(Object.prototype.__proto__===null);//true
```

所以查到属性的时候查到Object.prototype就可以停止查找了。

![原型链示意图](https://github.com/mqyqingfeng/Blog/raw/master/Images/prototype5.png)

```js
function Person(){
    
}
var person = new Person();
console.log(person.constructor === Person);//true
```

当获取`person.constructor`时，其实`person`中并没有`constructor`属性，当不能读取到`constructor`属性时，会从`person`的原型也就是`Person.prototype`中读取，正好原型中有该属性

```js
person.constructor === Person.prototype.constructor
```

**__proto__**

绝大部分浏览器都支持这个非标准的方法访问原型，然而它并不存在于`Person.prototype`中，实际上，它是来自于`Object.prototype`，与其说是一个属性，不如说是一个`getter`、`setter`,当使用`obj.__proto__`时，可以理解成返回了`Object.getPrototype(obj)`

**真的是继承吗**

每一个对象都会从原型中继承属性,实际上，继承是一个十分具有迷惑性的说法，继承意味着复制操作，然而js默认并不会复制对象的属性，相反，javascript只是在两个对象之间创建一个关联，这样，一个对象就可以通过委托访问另一个对象的属性和函数，所以与其叫继承，委托的说法反而更准确。