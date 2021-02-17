### Ajax 跨域

**同源策略**

同源策略是一种约定，它是浏览器最核心也最基本的`Web`安全功能。如果缺少同源策略，浏览器正常的功能可能都会受到影响。

**浏览器的同源策略，限制了来自不同源的document或脚本,对当前document读取或设置某些属性**

**为什么会出现跨域问题**

出于浏览器的同源策略限制，浏览器会拒绝跨域请求

> 严格来说，浏览器并不是拒绝所有的跨域请求，实际上拒绝的是跨域的读操作，浏览器的同源限制策略是这样执行的

- 通常浏览器允许进行跨域写操作，如链接，重定向
- 通常浏览器允许跨域资源共享嵌入,如`img`、`script`
- 通常浏览器不允许跨域读操作

什么才算跨域？

非同源请求,均为跨域。同源：如果两个页面拥有相同的协议(protocol)，端口(prot)和主机(host)那么这两个页面就属于同一个源(origin)

| URL                                                        | 说明                | 是否通信 |
| ---------------------------------------------------------- | ------------------- | -------- |
| `http://www.a.com/a.js`<br/>`http://www.a.com/b.js`        | 同一域名下          | 允许     |
| `http://www.a.com/a.js`<br/>`http://www.b.com/script/b.js` | 同一域名下不同文件  | 允许     |
| `http://www.a.com/a.js`<br/>`https://www.b.com/b.js`       | 同一域名下,不同协议 | 不允许   |

**为什么会有跨域需求？**

工程服务化后,不同职责的服务分散在不同的工程中，往往这些工程的域名是不同的，但一个需求可能需要对应到多个服务，这时便需要调用不同的接口，因此会出现跨域。

**如何实现跨域**

最常见的跨域方式有以下三种:`JSONP`、`CORS`、`postMessage`

**JSONP**

实现原理

虽然因为同源策略的影响，不能通过`XMLHttpResquest`请求不同域上的数据，但是，在页面上引入不同域上的js脚本文件却是可以的，因此在js文件载入完毕之后，触发回调，可以将需要的data作为参数传入。

```js
<script>
    function dosomething(data){
    //处理获得的数据
}
 </script>
<script src="http://example.com/data.php?callback=dosomething""></script>
```

```php
<?php
    $callback = $_GET['callback'];//得到回调函数名
	$data = array('a','b','c');//要返回的数据
	echo $callback.'('.json_ende($data).')';//输出
?>
```

**JSONP的优缺点**

JSONP很少使用(了解)

优点：兼容性好(兼容低版本IE)

缺点：1、只支持`GET`请求。2、`XMLHttpResquest`相对于`JSONP`有着更好的错误处理机制。

**CORS**

`CORS`是W3c推荐的一种新的官方方案，能是服务器支持`XMLHttpRequest`的跨域请求,`CORS`实现起来更方便一些，只需要增加一些`HTTP`头，让服务器声明允许的访问来源。

通常使用`CORS`时异步请求会被分为简单请求和非简单请求，非简单请求的区别是会先发一次的预检请求。

简单请求

使用下列方法之一且没有人为设置对`CORS`首部字段集合之外的其它首部字段

- GET
- HEAD
- POST

```js
//仅进POST方法的Content-Type值等于下列之一才算简单请求
 text/plain
multipart/form-data
application/x-www-form-urlencode
```

**postMessage**

`postMessage`方法是HTML5新引进的特性，可以使用它来向其它的window对象发送消息,不论这个window对象属于同源还是不同源。