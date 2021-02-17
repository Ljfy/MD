### Js数据类型之检测

**1、typeof是否能正确判断类型**

对于原始类型来说,除了`null`都可以调用`typeof`显示正确的数据类型。

```js
typeof 1 //number
typoof '1' //string
typeof undefined //undefined
typeof true //boolean
```

但对于引用数据类型,除了函数,都会显示`Object`

```js
typeof []; //object
typeof null //object
```

因此采用`typeof`判断对象的数据类型是不合适的,采用`instanceof`会更好，`instanceof`的原理是基于原型链的查询,只要处于原型链中,判断永远为`true`

```js
const Person = function(){}
const p1 = new Person();
p1 instanceof Person //true

var str1 = 'afa';
str1 instanceof String //false
var str2 = new String('hello world');
str2 instanceof String //true 
```

