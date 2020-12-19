原文地址: https://codeburst.io/javascript-functions-understanding-the-basics-207dbf42ed99
什么是函数?

一个函数是一个子程序用来执行某个小的具体的任务.

函数会再被调用的时候执行.这是调用函数

函数可以传递到另个函数并使用.

函数总是返回一个值.在 JavaScript,如果没有返回具体的值,那函数就会返回一个 undefined.

函数是一个对象



定义一个函数

在 JavaScript 中有几种方式定义函数.

函数声明是给一个函数一个 名字.要创建一个函数声明是使用 Function 关键字,并在关键字后面加上名字.当使用函数声明的时候.函数声明会提升.所以允许函数在定义之前使用它.

function name(parameters){
  *statements*}

函数表达式是定义 命名函数或者匿名函数,匿名函数是指一个没有名字的函数.函数表达式是每天提升.因此,不能在定义之前使用它.在下面的例子中.我们设置一个匿名函数赋值给一个变量.

```
let name = function(parameters){
  statements
}
```



箭头函数表达式是一种更简洁写函数表达式的语法.箭头函数不会创建他们的 this 值.

let name = (parameters) => {
  *statements*
}

Parameters vs. Arguments.

如果你是 JavaScript 新手,你可能听说过,*parameters* 和*arguments*可以互换使用.他们相似的同时,他们之间有一个很重要的差别.



Parameters是在定义函数的时候使用的,它们是在函数定义中创建的名称。实际上,在定义函数的时候,我们最多可以传递 255 个参数,Parameters是在()使用逗号隔开.下面是有两个参数的例子-`param1` 和 `param2

```js
const param1 = true;
const param2 = false;function twoParams(param1, param2){
  console.log(param1, param2);
}
```

**Arguments**,从另一方面,是函数在执行的时候从Parameters收到的传递过来的参数.在上面的例子.两个Arguments是`true和 `false`.



调用函数

函数会在被调用的时候执行.这个过程叫做调用函数,你可以使用函数名字来调用.名字跟着圆括号:()



看一个例子

> 如果你是用谷歌浏览器,打开开发者工具,你可以试下这些例子 : **[WINDOWS]***:* **Ctrl + Shift + J [MAC]***:* **Cmd + Opt + J**

首先,我们会定义一个函数命名为 logIt,这个函数有一个参数 name.当被执行时,函数会打印name到 console 上面



要执行函数,我们调用它,同时传递一个参数,这里我传递的是 Joe

```
logIt('Joe');
// Joe
```

如果你的函数没有参数,可以使用一组空括号来调用它:

```
function logIt2(){
  console.log('The second one');
}logIt2();
// The second one
```










函数返回
每个函数在JS中都会返回undefined除非定义，让我们试一下定义一个空函数并调用它
function test(){};
test();
// undefined
真棒，跟预期一样，返回一个undefined
现在让我们修改一下，使用return关键字来返回一个值，看一下下面的代码
function test(){
  return true;
};
test();
// true

在这个例子里面，我们明确告诉函数返回一个true  当我们调用函数，果然返回了一个true


但为啥这是重要的？这是因为函数返回的值，是返回给函数的调用方。看一下代码
let double = function(num) {
   return num * 2;
}


这是一个函数表达式创建了一个返回传递进去的参数的两倍的函数。我们可以调用这个函数然后把返回的值保存到一个变量里面。
let test = double(3);
当我们打印的时候，我们得到6
console.log(test);
// 6
太棒了。返回变量不仅从函数中返回值，而且将它们赋给所谓的函数！

另一个关于return的规则是 到了return之后会停止执行


在下面的例子里面我可没return两个声明
function test(){
  return true;
  return false;
};
test();
// true
第一个return会立即停止执行函数，然后返回一个true 第三行代码 返回false，永远不会被执行

函数是一个函数对象，在JavaScript中，非原始类型都是对象



对象在JavaScript中是非常有用的，因为我们可以传递一个函数当成参数給另一个函数或者返回一个函数，这叫做高阶函数


你可能早已经用过很多高几函数，但是丙不知道：Array.prototype.mapand Array.prototype.filter are higher order functions (Just to name a couple). You can check out some of my previous articles to learn more about objects and higher order functions in JavaScript…
数组、原型、映射和数组、原型、过滤器都是高阶函数(仅举几个例子)。您可以查看我以前的一些文章，了解更多关于JavaScript中的对象和高阶函数的信息…
这有很多知识需要慢慢消化下面是一些重要的东西：
函数是一个子程序用来执行具体的任务

函数声明是有提示的  -函数表达式没有

函数会在调用的时候执行，这叫做函数调用

函数可以传值并使用，这个值的名字叫做参数 这个值本事叫做实参

函数总是返回一个值。在JavaScript如果没有指定，会默认返回一个undefined

函数是一个对象
结束语:
谢谢你的阅读！如果你准备好最终学习网络开发，看看:2018年网络开发路线图。
如果你正在努力成为一名更好的Javascript开发人员，那就去看看:挑战你的JavaScript面试——学习算法+数据结构。
我每周发表4篇关于网络开发的文章。如果你想加入我每周一次的电子邮件列表，请考虑在这里输入你的电子邮件，或者在推特上跟我来。
如果这篇文章有帮助，请点击下面的拍手按钮几次以示支持！⬇⬇
