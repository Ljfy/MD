### Array

对象允许键值对集合,很多时候我们会发现,还需要一种有序集合,里面的元素都是按顺序排列的,可能需要储存一些列表。比如用户、商品以及`HTML`元素等等。这时一位大佬就闪耀登场了。`Array`他能存储有序的集合。

声明的两种方式:

```js
let arr = new Array(); //不常用
let arr = [];//常用
```

数组可以储存任何类型的元素：

```js
//混合值
let arr = ["Apple",{name:"Json"},true,function(){alert('hello');}];
alert(arr[1].name); //Json 取索引为 1的对象
arr[3]();//hello 获取索引为3的函数并执行
```

**pop/push,shift/unshift**

队列是最常见的使用数组的方法之一。在计算机科学中,这表示支持两个操作的一个有序集合

- `push` 在末端添加一个元素
- `pop` 从末端取出一个数据
- `shift`取出队列首端的一个元素,整个队列往前移,原本排在第二的现在排第一
- `unshift`  在数组的首端添加元素

这几个方法都会改变数组自身。

我们试试下面的 5 个数组操作。

1. 创建一个数组 `styles`，里面存储有 “Jazz” 和 “Blues”。
2. 将 “Rock-n-Roll” 从数组末端添加进去。
3. 用 “Classics” 替换掉数组最中间的元素。查找数组最中间的元素的代码应该适用于任何奇数长度的数组。
4. 去掉数组的第一个值并显示它。
5. 在数组前面添加 `Rap` 和 `Reggae`。

```js
let styles = ["Jazz","Blues"];
styles.push("Rock-n-Rol");
styles[Math.floor((styles.length-1)/2)] = "Classics";
styles.shift();
styles.unshift("Rap","Reggae");
```

**循环**

遍历数组最古老的方式就是`for`循环

```js
let arr = ["Apple","Orange","Pear"];
for(let i = 0;i < arr.length;i++){
    alert(arr[i]);
}
```

`for...of`

```js
let arr = ["Apple","Orange","Pear"];
for(let fruit of arr){
    alert(fruit);
}
```

`for...of` 不能获取当前的索引，只是获取元素值，大多数情况下是够用的，这样写更短。

数组也是对象,`for...in`也是可以的

```js
let arr = ["Apple","Orange","Pear"];
for(let key of arr){
    alert(key);
}
```

`for...in`会存在一些潜在的问题：

1、`for...in`循环会遍历所有属性,不仅仅是数字属性。

2、`for...in`循环适用于对象，并且做了相应的优化，但不适用数组，速度要慢。

**数组的瑞士军刀splice**

`splice`可以做的事情添加、删除、插入元素。

语法：

```js
arr.splice(start,[,deleteCount,elem1,...,elemN])
```

从索引`start`开始修改arr:删除`deleteCount`个元素在当前位置插入`elem1`、`elem2`,最后返回已删除的元素。

**删除**

```js
let arr = ["I","study","javaScript"];
arr.splice(1,1);//从索引 1删除一个元素
alert(arr);//["I","JavaScript"];
```

```js
 // 删除三个 元素在添加三个元素
 let arr = ["t","e","s","t"];
 arr.splice(0,3,"a","b","c");
 console.log(arr);//["a","b","c","t"]

//负向索引

let arr = [1,2,5];
arr.splice(-1,0,3,4);//数组末尾前一位 删除0个元素 再添加3和4
console.log(arr);//[1,2,3,4,5]
```

**slice**

`arr.slice`语法`arr.slice([start],[end])`

它会返回一个新的数组,将所有从索引`start-end`不包括`end`的数组复制到一个新的数组`start`和`end`都可以是负数

```js
let arr = ["t","e","s","t"];
arr.slice(1,3);//e,s(赋值位置 1到位置3的元素)
```

**concat**合并数组

```js
var a = [1,2,3];
var b = [4,5,6];
var c = a.concat(b);
console.log(c);//1,2,3,4,5,6
```

**forEach循环**

遍历数组中每一项,没有返回值,对原数组没有影响,不改变原数组。

```js
arr.forEach(item,index,array)=>{
   //执行代码
}
```

参数：数组中有几项,那么就传递进去的匿名函数就执行几次

- value 数组中的当前项
- index 当前项的索引
- array原始数组

**Map循环**

有返回值,可以return出来

map的回调函数中支持return返回值，return的是什么,就相当于把数组中的这一项变为什么(不影响原数组)

```js
arr.map(function(value,index,array){
    // 执行代码
    return xxx;
})
var arr = [1,2,3,4,5];
var res = arr.map(function(item,index,arr){
      return item *10;
 })
console.log(res);//数组中的每一项都会*10
console.log(arr);//1,2,3,4,5 没有改变
```

补充:

```js
var ls = ['1','2','3'].map(parseInt)
console.log(ls);
```

首先要了解一下`parseInt()`函数,`parseInt`要接收两个参数(string,radix)

- string 要转化为字符串
- radix：要转化的进制数(将这个字符串转为多少进制的数)默认为0,即将字符串串转为十进制的数radix的范围为`2-36的整数`,超出这个将返回`NaN`

当`Map`中的函数可以接收参数时,map函数会自动把参数传递进去,所以三次执行顺序,parseInt接收的三次参数分别是

```js
[parseInt('1',0),parseInt('2',1),parseInt('3',2)] => [1,NaN,NaN]
```

可以尝试自定义函数,

```js
function myperseInt(str,radix){
    console.log(str,radix);
}
l= ["1","2","3"].map(myperseInt)
```

**搜索和位置方法**

`indexOf/lastIndexOf(item,pos)`从`pos`找到`item`,则返回索引否则返回-1

`includes(value)`如果数组有`value`,则返回`true`,否则返回`false`



**find和findindex**

```js
let  result = arr.find(function(item,index,array){
    //如果返回true 则返回item并停止迭代
    //
})
```

- item 元素
- index 索引
- array数组本身

如果它返回true,则搜索停止,并返回item,如果没搜索到,则返回`undefined`

找到id ==1

```js
let users = {
    {id:1,name:"John"},
    {id:2,name:"Peter"},
    {id:1,name:"haha"}
}
let user = users.find(item => item.id==1);
user // id:1,name:"John"
```

**sort(fn)**

`arr.sort`方法对数组原位排序,更改元素的顺序,直接使用`sort`结果将是不符合预期的

```js
let arr = [1,2,15];
arr.sort();
arr //1,15,2
```

这些元素被按字符串进行排序,按照字典进行排序`"2" > "15"`的。

写一个函数比较两个任意值并返回

```js
function compare(a,b){
    if(a > b) return 1;//如果第一个值比第二个值大
    if(a == b) return 0;// 如果两个值相等
    if(a < b) return -1;// 如果第一个值比第二个值小
}
let arr = [1,2,15];
arr.sort(compare);
console.log(arr);//现在符合预期了
```

![image-20201202082903549](C:\Users\Sky\AppData\Roaming\Typora\typora-user-images\image-20201202082903549.png)![image-20201202082904229](C:\Users\Sky\AppData\Roaming\Typora\typora-user-images\image-20201202082904229.png)![image-20201202082904483](C:\Users\Sky\AppData\Roaming\Typora\typora-user-images\image-20201202082904483.png)![image-20201202082904656](C:\Users\Sky\AppData\Roaming\Typora\typora-user-images\image-20201202082904656.png)![image-20201202082904890](C:\Users\Sky\AppData\Roaming\Typora\typora-user-images\image-20201202082904890.png)

**可迭代对象**

可迭代对象是数组的泛化

**Symbol.iterator**

```js
//创建一个对象
let range = {
    from:1,
    to:5
}
range.[Symbol.iterator] = function(){
    //返回迭代器的对象
    return{
        current:this.from,
        last:this.to,
        next(){ //next 在of的每一轮循环迭代被调用
            if(this.current <=this.last){
               	return{done:false,value:this.current++}
               }else{
                   return{done:true}
               }
        }
    }
}
//现在可以运行了
for(let num of range){
    alert(num)
}
//希望这样运行 for(let num of range)...num =1,2,3,4,5
```

**Array.from**

可以接受一个可迭代或类数组的值,并从中取得一个真正的数组,然后调用数组方法。

```js
 let arr = {
            0: "hello",
            1: "world",
            length: 2
        };
        let arr1 = Array.from(arr);
        alert(arr1.pop());//world
```

除了使用`Array.from`使类数组能够使用数组方法,还可以使用`call/apply`来改变`this`的执向

```js
let obj = {
    0:1,
    1:2,
    2:3,
    length:3
}
Array.prototype.push.call(obj,"哈哈哈")
```

![image-20201202084912167](C:\Users\Sky\AppData\Roaming\Typora\typora-user-images\image-20201202084912167.png)

字符串	不可修改。字符串`length`属性是只读的,不可修改,所有涉及`length`的属性,都无法生效

![image-20201202085411828](C:\Users\Sky\AppData\Roaming\Typora\typora-user-images\image-20201202085411828.png)



在数组中搜索`indexOf/lastIndexOf/includes`

- `indexOf(item,form)`从索引`from`开始搜索`item`,如果找到则返回索引,否则返回-1

```js
let arr = [1,0,fasle];
console.log(arr.indexOf(2));//-1
console.log(arr.indeOf(1));//0
```

- `arr.lastIndexOf(item,from)`和上面相同，只是从右向左搜

- `includes(item,form)`：从索引`from`开始搜索`item`,如果找到则返回`true` 如果没有找到则返回`false`

```js
let arr = [1,0,false];
arr.includes(1);//true
arr.includes(2);//false
```

`map(callback)` 映射数组(遍历数组),有`return` 返回一个新的数组

`callback`参数：

`value`---当前值的索引

index:----索引

array--原数组

```js
	let user = [{
					name: "小明",
					email: 'ming@.com'
				},
				{
					name: "小红",
					email: 'ming@.com'
				},
				{
					name: "小黑",
					email: 'hei@.com'
				},
			]
let memail = user.map((user)=>user.email);			
let names = user.map((user)=>user.name);	
console.log(names.join(','));
console.log(memail.join(','));
```

字符串中使用`map` 在一个string上使用`map`方法获取字符串中每二个字符所对应的字符串编码

```js
var str = Array.prototype.map;
var a = str.call('Hello World',function(x){
    return x.chartCodeAt(0)
})
console.log(a);//map.html:31 (11) [72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100]
```

下面的语句返回什么呢？

```js
["1","2","3"].map(parseInt);//[1,2,3]? 实际的结果是[1,NaN,NaN]
```

通常使用`parseInt`时,只需要传递一个参数,但实际上,`parseInt`可以有两个参数，第二个参数是进制数，可以通过语句`alert(parsein.length)===2` 来验证，`map`方法在调用`callback`函数时,会给他传递三个参数，当前正在遍历的元素，元素索引,原数组本身。

第三个参数`parseInt`会忽视，第二个参数不会，也就是说,`parseInt`把传	过来的索引值当成进制数来使用,从而返回`NaN`

应该使用如下函数 才能正确返回结果

```js

function init(ele){
    return parseInt(ele,10)
}
["1","2","3"].map(init);//[1,2,3]
```

 https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map

**reduce**

`Array`的`reduce`()把一个函数作用在这个`Array`的`[x1,X2,X3...]`上,这个函数必须接收两个参数，`reduce`()的结果继续和序列的下一个元素做累积计算，如下：

```js
[x1,x2,x3,X4].reduce(f) = f(f(f(x1,x2)，x3),x4)
```

```js
let arr = [0,1,2,3,4];
let arr1 = arr.reduce((preValue,curValue)=>
 preValue + curValue
 )
console.log(arr1);//10
```

