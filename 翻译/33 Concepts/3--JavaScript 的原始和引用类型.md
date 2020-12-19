> 总结: 在这个教程,你会看到 JavaScript 的原始和引用类型的区别

######使用一个值和引用一个值

在 JavaScript 中,一个变量有可能存储为不同类型的数据: 原始类型和引用类型,JavaScript 有六种原始类型,如:undefined,null,Boolean,unmber,string,和 symbol还有一个引用类型对象.

当你给一个变量赋值的时候,JavaScript 引擎会探测这个值是原始类型还是引用类型.

如果一个变量存储一个原始类型的值,当你操作这个值的时候,你是操作存储这个值的变量,换句话说,这个变量是存储一个原始类型的值是按照值来进行使用

跟原始类型的值不同,当你操作一个对象,是你操作一个对象的引用.相当于一个真实是对象,总之,一个变量要是存储的是一个对象的话,那就是按照引用来使用.



######复制一个原始值

当你把一个原始类型的变量赋值给另一个变量的时候,会创建一个新的变量并把原本的原始类型的值复制给新的变量.

让我们看一下例子吧

首先,定义一个变量并给它一个初始的是 10

| 1    | var a = 10; |
| ---- | ----------- |
|      |             |

![JavaScript-Primitive-Value-Example](https://www.javascripttutorial.net/wp-content/uploads/2016/08/JavaScript-Primitive-Value-Example.png)

其次,定义另一个变量 b,并给它赋值为变量 a ,内部里面 js 会复制 a的值到 b 里面

| 1                                                            | var b = a; |
| ------------------------------------------------------------ | ---------- |
| ![JavaScript-Primitive-Value-Copying](https://www.javascripttutorial.net/wp-content/uploads/2016/08/JavaScript-Primitive-Value-Copying.png) |            |

最后,给变量 b一个新的值 20

| 1    | b = 20; |
| ---- | ------- |
|      |         |

![JavaScript-Primitive-Value-Assigning](https://www.javascripttutorial.net/wp-content/uploads/2016/08/JavaScript-Primitive-Value-Assigning.png)

因为 a 和 b 之间并没有关联,因此,当你改变存储在 b 变量里面的值的时候,变量 a 里面的值还是保持不变.

| 12   | console.log(a); *// 10;*console.log(b); *// 20;* |
| ---- | ------------------------------------------------ |
|      |                                                  |

######复制一个引用值

当你从一个存储引用类型的变量赋值给另一个变量时,存储在变量里面的值同时也会复制到另一个新的变量,不同之处在于两个变量的值都是存储在同一个地址的堆中.结果是,两个变量指向同一个对象.

看一下下面的例子

定义一个变量 x 赋值包含一个对象里面有一个 name 的属性为'John'

| 1                                                            | var x = {name: 'John'}; |
| ------------------------------------------------------------ | ----------------------- |
| ![JavaScript-Reference-Declaration](https://www.javascripttutorial.net/wp-content/uploads/2016/08/JavaScript-Reference-Declaration.png) |                         |

其次,定义另一个变量,并把 x 变量赋值给 y.现在 x和 y 同时指向一个对象在堆中.

| 1    | var y = x;                                                   |
| ---- | ------------------------------------------------------------ |
|      | ![JavaScript-Reference-Assignment](https://www.javascripttutorial.net/wp-content/uploads/2016/08/JavaScript-Reference-Assignment.png) |

第三,使用 y变量来改变存储在对象里面的 name 属性,

| 1                                                            | y.name = 'David' |
| ------------------------------------------------------------ | ---------------- |
| ![JavaScript-Reference-Modifying-Property](https://www.javascripttutorial.net/wp-content/uploads/2016/08/JavaScript-Reference-Modifying-Property.png) |                  |

因为 x和 y 指向同一个对象,因此,这个改变同时体现在 x 变量上.

| 1    | console.log(x.name); *// 'David'* |
| ---- | --------------------------------- |
|      |                                   |

![JavaScript-Reference-Accessing-Property](https://www.javascripttutorial.net/wp-content/uploads/2016/08/JavaScript-Reference-Accessing-Property.png)





在这个教程里面,你已经学习了使用原始值和引用值

文章原文:https://www.javascripttutorial.net/javascript-primitive-vs-reference-values/