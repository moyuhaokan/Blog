在 js 中函数被认为是第一等公民,而且对于创建函数来说这个概念是非常重要的.

![1*dAwQkc-E0j1AcpdPeGznzg](https://miro.medium.com/max/1400/1*dAwQkc-E0j1AcpdPeGznzg.png)

不像别的语言,在 js 中,我们有三种不同的创建函数的方式.

1.函数声明

2. 函数表达式

3. 命名函数表达式

   

######函数声明

```js
function [name](param1, param2, ...param3) {
    // Function Body & Logic
}
```



在这个例子里,我们把function 关键字放在函数名字前面.

一个主要的好处是这个函数会 **提升**

> 因为这个,我们可以先执行这个函数,再声明它.

当你想要将某些抽象的逻辑放到函数内部,但是实际上实现是在以后完成.

> 最佳实践: 定义好了函数之后立即执行它,比依赖js 的提升要好



######函数表达式

任何给某个变量赋值的语句都可以叫做表达式



var a= 100;

var b=  'hello worl'



在某些情况下,会创建没有名字的函数并赋值给某个变量

```js
var [name] = function(param1, param2, ...param3) {
    // Function Body & Logic
}
foo(1,3,4);
```



**限制:**函数不能在被定义之前执行

```js
var num1 = 10;
var num2 = 20;
var result = add(num1, num2);  
// 
Uncaught TypeError: add is not a functionvar add = function(param1, param2) {
    return param1 + param2 ;
} 
```

下面的方式会执行

```js
var num1 = 10;
var num2 = 20;
var add = function(param1, param2) {
    return param1 + param2 ;
}
var result = add(num1, num2); // ==> 30
```

######命名函数表达式 - 包含两种方法

现在你已经知道函数表达式和函数声明之间的区别了,现在我们看下两者的混合吧

```js
var num1 = 10;

var num2 = 20;

 var addVariale = function addFunction(param1,param2) {

return param1+ param2

}


```

注意,上面的代码已经不是匿名的而是有一个**addFunction** 的名字,同时,它赋值给了一个变量 - **addVariale .**

现在你虽然加了一个名字到function 关键字后面,但是这不意味着你可以直接执行这个函数名.

```js
var result = addFunction(num1, num2); 
// ==> Uncaught ReferenceError: addFunction is not defined
```

相反,只有赋值变量 **addVariable** 可以引用和执行

```js
var result = **addVariable**(num1, num2); 
// ==> 30
```



#####重点

1.addFunction掩盖了调试工具调用堆栈中的addVariable。

![1*CPUa1X3-O55XPPMz7MBVkA](https://miro.medium.com/max/1400/1*CPUa1X3-O55XPPMz7MBVkA.png)



命名函数表达式

![1*QsAXJNRrrI49ZkDo3WCrnA](https://miro.medium.com/max/1400/1*QsAXJNRrrI49ZkDo3WCrnA.png)

函数表达式





2.在命名函数表达式的情况下，调用外部抛出的addFunction（）错误



> 未捕获错误: addFunction 没找到



但是你可以在函数内部调用,这样子会执行

```js
var num1 = 10;
var num2 = 20;
var addVariable = function addFunction(param1, param2) {
   var res = param1 + param2;
   if (res === 30) {
        res = 
addFunction(res, 10);
   }
   return res;
}
var result = addVariable(num1, num2); // ==> 40
```

在这个场景上,查看 res 是 30 的话,调用同样的函数,并把赋值 30 和 10,作为参数,最后会返回一个 40 作为输出结果.

3.在IE8及以下版本中使用命名函数表达式的一个严重警告是，它错误地在两个完全不同的时间创建了两个完全独立的函数对象（Double take）。



如果你需要支持 IE8,最好使用函数表达式和函数声明,避免使用命名函数表达式.

希望这个文章会给你一个的关于函数声明,函数表达式,命名函数表达式的清晰的概念



希望你可以在下面留言写下你的想法,反馈和疑虑,我们可以更深的讨论一下.



原文地址: https://medium.com/@raviroshan.talk/javascript-function-declaration-vs-expression-f5873b8c7b38

