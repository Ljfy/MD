## JavaScript 基础

1. `JavaScript` 定义了几种数据类型？哪些是原始类型？哪些是复杂类型？`null` 是对象吗？

- 原始类型
  - `Number`:用于任何类型的数值，整数或浮点数
  - `String`：用于字符串，一个或多个
  - `Boolean`：`true`和`false`
  - `null`:表示为空的对象,`typoof`会返回`Object`
  - `undefined`：未定义
- 复杂类型
  - 普通对象(Object)
  - 数组(Array)
- `null`表示准备用来保存对象,还没有真正保存对象的值，从逻辑角度看null表示一个空对象指针

2. 怎样判断“值”属于哪种类型？`typeof` 是否能正确判断类型？

   typeof 能够正确判断基本的数据类型,对于对象来说，除了null,function不能正确判断类型

   typeof 运算符返回参数的类型

3. `NaN` 是什么？有什么特别之处？

`NaN`不是一个有效数字,但它是一个数字类型,任何值和`NaN`相比都是`NaN`

4. `== `与 `=== ` 有什么区别？

`==`在判断相等的时候会进行隐式的类型转换

`===`先判断类型,在比较.类型不同直接不相等。

5. `console.log(1+"2")` 和 `console.log(1-"2") `的打印结果？'12' -1

6. 为什么 `console.log(0.2+0.1==0.3)` 输出 `false` ？

   计算机在做运算时,所有的运算都要转换成二进制去计算。然而,有些数字转换成二进制之后无法精确表示比如说,`0.1`和`0.2`转换成二进制之后,是无穷的,因此存在浮点数的计算不精确的问题，

7. 列举`Math`对象和`Date`对象的常用方法

  `Math.abs()`:返回绝对值

  `Math.random()`随机数

  `Math.floor`向下取整

  `Math.round`四舍五入

  `Math.ceil();向上取整`

  `Math.max(x,y,z)`返回多个数字中的最大值

  `Math.min(x,y,z)`返回多个数字中的最小值

`date`      

`getFullYear()`获取年份

`getMonth`：获取月份

`getDate()`获取日

`getDay()`获取星期

`getHours`获取小时

`getMinutes()`获取分钟

`getSeconds()`获取秒

8. 请用三元运算符改写以下代码

   ``` js
   if(a > 10){ 
       b = a    
   }else {      
       b = a - 2    
   }
   a > 10 ? b = a : b = a-2
   ```

9. `break` 与 `continue` 有什么区别？

   `break`可以用来退出`switch`语句或者整个循环语句,会立即终止离他最近的那个循环语句,`continue`可以用来跳过当次循环,继续下一次循环,默认只会离它最近的循环起作用

9. `switch...case` 语句中的 `break` 有什么作用？

用来退出`switch`语句或者整个循环语句。

10. 以下代码的输出？为什么？    

   ```js
   console.log(a);//undefined    
   var a = 1;    
   console.log(b);//b is not defined
   // 谈一下js中的提升
   当作用域形成,代码自上而下执行之前,浏览器首先会var/function关键字提前声明或者定义，这种预先处理机制称为变量提升。
   ```

11. 如下代码的输出？为什么？    

   ```js
   var x = 10;    
   bar()     
   function bar() {      
       var x = 30;      
       function foo() {        
           console.log(x);//30       
       }      
       foo();    
   } 
变量取值到创建这个变量的函数的作用域中取值,如果在当前作用域中没有查到值,就会向上级作用域查找，直到查到全局作用域,这样的查找过程叫做作用域链。
   ```

12. 如下代码的输出？为什么？    

   ```js
   var x = 10    
   bar()     
   function foo() {      
       console.log(x);//10    
   }    
   function bar() {      
       var x = 30      
       foo()    
   }
当函数操作一个变量时,它会在自身作用域中查找,如果有就直接使用(就近原则),如果没有就向上一级作用域寻找,直到找到全局作用域,
   ```

13. 如下代码的输出？为什么？    

    ```js
    var a = 1    
    var c = {name: "oli", age: 2}    
    function f1(n) {      
        ++n    
    }    
    function f2(obj) {      
        ++obj.age    
    }    
    f1(a)     
    f2(c)     
    f1(c.age)     
    console.log(a);//1 传入的参数是a的副本,并不会改变a,只是改变副本的值,不会对外部变量产生影响
    console.log(c);//{name: "oli", age: 3}参数为引用类型,并非是引用传递。可以说是按值传递,传入的参数,是对实参地址的复制,是实参地址的副本,指向同一个对象,obj还是会按引用来访问一个对象,改变函数内部的age,外边的C也会受到影响。    
    // 谈一下 复杂数据类型和基本类型的不同之处？
    基本数据类型:参数赋值的时候传数值
    复杂数据类型：参数赋值的时候传地址,基本数据类型的值,直接保存在栈内存中。值与值之间时独立存在的,修改其中一项并不会影响其他的变量。
    引用数据类型保存在堆内存中的,每创建一个对象,就会在堆内存中开辟一个新的内存空间，而变量对象保存在对象的内存地址,如果两个保存了同一个对象的引用,当一个值通过变量修改属性时,另一个也会受到影响
    // 函数参数是对象会发生什么问题？
    相当于在函数内部写了var obj;定义形参就相当于在函数作用域中声明了变量
    ```

14. 写一个函数 `squireArr`，其参数是一个数组，作用是把数组中的每一项变为原值的平方。    

    ```js
    var arr = [3, 4, 6]    
    function squireArr(arr) {      
        // 补全 
     for (var i = 0; i < arr.length; i++) {
      arr[i] = Math.pow(arr[i],2)
    }    
    squireArr(arr)    
    console.log(arr) // [9, 16, 36]
    ```

15. 写一个函数 `squireArr`，其参数是一个数组，返回一个新的数组，新数组中的每一项是原数组对应值的平方，原数组不变。    

    ```js
    var arr = [3, 4, 6];    
    function squireArr(arr) {
        var arr2 = arr.slice(0);
       //var arr2 = JSON.parse(JSON.stringify(arr));
        for(var i = 0;i<arr2.length;i++){
            arr2[i]= Math.pow(arr2[i],2);
        }
        return arr2;
    }    
    var arr2 = squireArr(arr)    
    console.log(arr) // [3, 4, 6]    
    console.log(arr2) // [9, 16, 36]
    ```

15. 封装一个判断质数的函数,要求返回`true`或`false`

```js
function set(n){
    for(var i = 0;i<n.length;i++){
        if(!n%i==0){
           return false;
           }
    }
    return true;
}
console.log(set(6));
```



16. 实现一个方法,于数组中寻找某个值作为分割的界点,使得该值左右两边的数相加相等

   ```js
    [1,2,3,4,3,2,1]===> 返回下标3
    [1,100,50,-51,1,1]===> 返回下标1

	var arr = [1,100,50,-51,1,1];
	function set(arr){
        var sum = 0;
        for(var i = 0;i < arr.length;i++){
            sum += arr[i];
            var sum2 = 0;
            for(var j = i + 2;j<arr.length;j++){
                sum += arr[j];
            }
            if(sum == sum2){
               return i+1;
            }
        }
    }
console.log(set(arr));
   ```

17. 如何正确的判断 `this`

```javascript
   
  function foo() {
   	console.log(this.a);
   }
   var a = 1;
   foo();
   
   var obj = {
   	a: 2,
   	foo: foo,
   };
   obj.foo();
  
   var c = new foo();

当前方法执行的主体，谁执行这个方法,this就执行谁
1、给当前元素的某个事件添加方法,方法中this中的this,就是当前操作元素的本身。
2、函数执行看是否有(.)，有的话(.)前面的this就是谁
3、构造函数执行,方法中的this一般都是当前类的实例
4、箭头函数中没有自己的this,this是上下文中的this
```

18. `JSON` 的两个方法,说明他们的作用

- `JSON.stringify()`可以把括号里面的对象转换为`JSON`字符串
- `JSON.parse()`可以把括号里面的`JSON`字符串转为对象

19. 写一个函数，生成一个随机颜色字符串，合法的颜色为 `#000000 ~ #ffffff`。    

    ```js
    function getRandColor() {      
        // 补全
        return '#'+Math.random().toString(16).substr(2,6).toUpperCase()
    }    
    var color = getRandColor()    
    console.log(color) // #3e2f1b
    ```

20. 怎样用原生 `JS` 将一个多维数组拍平？    

    ```js
     var arr = [1, [2, 8],[3, [4, 5]] ];
       function flat(arr) {
                var text = arr.toString();
                var str = text.split(',');
                var num = [];
                str.forEach(function (data, item) {
                    num.push(+data);
                })
                console.log(num);
            }
        flat(arr);
    ```

21. 以下代码的输出? 为什么?

    ```js
    function getSum(a,b){
        return a+b
    }
    function foo(a,b){
        var temp = a+b;
    }
    console.log(getSum(3,5)); // 8
    console.log(foo(3,5)); //  undefined 没有返回值
    ```

22. 总结一下数组常用的方法(`API`)

`push`：向数组末尾追加新的内容,原有数组改变

`	pop`：删除数组最后一项,原有数组改变

`shift`：删除数组的第一项,第一项被删除后.原有后面的索引都要向前提一位,原有数组改变

`unshift`:向数组开始位置追加新的内容,原有数组改变

`splice`：可以对数组进行很多操作,删除指定位置的内容,向数组指定位置增加新的内容、还可以修改指定位置的信息。删除`arr.splice(n,m)`从索引n开始删除m个元素,把删除的部分以一个新数组返回,原有数组改变

`Slice`：在一个数组中按照条件查找出其中的部分内容，原有数组不改变

`concat`：实现两个数组(或者值的拼接)原有数组不改变

 `toString`:把数组转为字符串

`join`：和`toString`类似,把数组转为字符串,可以设置为字符串后.每一项之间的连接符,原有数组不改变

`reverse`：把数组倒过来排列,原有数组改变

`sort`：给数组排序,在不传递参数的情况下只能处理10以内的数字排序,原有数组改变。

`indexOf/lastIndexOf`：这两个方法不兼容`IE6~8`,检测当前值在数组中第一次或者最后一次出现位置的索引,基于`indexOf`检测如果有返回大于等于零的索引，如果没有返回-1


