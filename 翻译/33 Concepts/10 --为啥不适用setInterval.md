最近,我遇到了一个需求是我要隔段时间调用一个函数,类似每隔十秒钟发送一个 ajax 请求.当然,setInterval 看起来是不错的方式.但是我遇到了挫折.



想要理解为啥 setInterval 是不好的,我们需要在脑子里面知道一个知识,那就是 JavaScript 是单线程的.也就是一次只能执行一个操作.

```js
    var fakeCallToServer = function() {
        setTimeout(function() {
            console.log('returning from server', new Date().toLocaleTimeString());
        }, 4000);
    }



    setInterval(function(){ 

        let insideSetInterval = new Date().toLocaleTimeString();

        console.log('insideSetInterval', insideSetInterval);

        fakeCallToServer();
    }, 2000);

//insideSetInterval 14:13:47
//insideSetInterval 14:13:49
//insideSetInterval 14:13:51
//returning from server 14:13:51
//insideSetInterval 14:13:53
//returning from server 14:13:53 
//insideSetInterval 14:13:55
//returning from server 14:13:55
```



正如你在打印的console.log语句中所看到的那样，setInterval一直在不停地发送ajax调用而不关心先前的调用是否已经返回。

这个会使得很多请求在排队.



现在让我们看下同步请求在 setInterval:



```js
var counter = 0;

var fakeTimeIntensiveOperation = function() {

  for(var i =0;i<50000000;i++) {

   document.getElementById('random');

}

 let insideTimeTakinngFunction = new Date().toLocaleTimeString()
 


console.log('insideTimeTakingFunction', insideTimeTakingFunction);

}
var timer = setInterval(function(){ 

    let insideSetInterval = new Date().toLocaleTimeString();

    console.log('insideSetInterval', insideSetInterval);

    counter++;
    if(counter == 1){
        fakeTimeIntensiveOperation();
    }

    if (counter >= 5) {
       clearInterval(timer);
    }
}, 1000);

//insideSetInterval 13:50:53
//insideTimeTakingFunction 13:50:55
//insideSetInterval 13:50:55 <---- not called after 1s
//insideSetInterval 13:50:56
//insideSetInterval 13:50:57
//insideSetInterval 13:50:58


```

我们在这里看到当setInterval遇到时间密集型操作时，它会做两件事情中的任何一件，a 尝试进入轨道或b创建新的节奏。 在Chrome上，它创造了一种新的节奏。

同样,在 setInterval 的代码块里面遇到错误,它不会停止执行而是继续执行错误的代码,需要使用 clearInterval 来停止它.

或者，您可以在时间敏感操作的情况下递归使用setTimeout。

总结

在异步的操作里面,setTimeInterval 会创建一个长长的请求,





原文地址:

https://dev.to/akanksha_9560/why-not-to-use-setinterval--2na9

