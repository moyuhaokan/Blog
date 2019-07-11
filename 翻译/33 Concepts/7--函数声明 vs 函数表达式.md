

######什么是js的函数表达式和函数声明?



函数声明声明了一个函数



一个函数声明是"保存待用".稍后会执行.当这个函数使用的时候.



就行声明一个变量是使用"var",函数声明是使用"function"

```
function bar() {
 return 3;
}
```



函数已经声明了,要使用它,必须使用函数名 bar()



######什么是函数表达?

js 函数同样可以使用**函数表达式**定义

函数表达式可以存储在变量图

*var x = function (a, b) {return a \* b};*

当一个函数存储到一个变量之后,使用这个变量就相当于使用这个函数.存储在变量里面的表达式不需要函数名.这些函数可以直接使用变量名调用.



######函数表达式 VS 函数声明

**例子: 函数表达式**

alert(foo()); // ERROR! foo wasn't loaded yet
var foo = function() { return 5; }

**例子: 函数声明**

alert(foo()); // Alerts 5. Declarations are loaded before any code can run.
function foo() { return 5; }



- **函数声明**可以再任何代码之前执行,函数表达式只能在加载器到达代码之时加载.
- 和var 声明类似,函数声明可以提升到其它代码的顶部.函数表达式没有提升.这允许函数表达式从定义它们的范围中保留局部变量的副本。



下面是几个函数表达式比函数声明更好使的好处

 

- 闭包
- 可以作为别的函数的参数
- 作为立即执行函数(IIFE)



原文地址: https://medium.com/@mandeep1012/function-declarations-vs-function-expressions-b43646042052

