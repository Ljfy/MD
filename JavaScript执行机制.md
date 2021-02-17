### JavaScript执行机制

因为`JavaScript`是一门单线程语言，所以得出以下结论：

- `JavaScript`是按照语句出现的顺序执行的，我们以为js都是都是这样的

```js
let a = 1;
console.log(a);

let b = 2;
console.log(b)
```

然而实际上`js`是这样的

```js
setTimeout(function(){
    console.log('定时器开始了')
});
new Promise(function(resolve){
    console.lop('马上执行for循环了');
    for(var i = 0;i < 1000;i++){
        i == 99 && resolve();
    }
}).then(function(){
    console.log('执行then函数');
})
console.log('执行结束')
```

### javascript事件循环

既然js是单线程的，那么就是只有一个窗口的银行，客户需要一个一个排队做业务，js也要按照顺序执行，如果有一个任务耗时过长，那么后一个任务就要等着