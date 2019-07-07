想要直接看总结的朋友请直接拉到底部



本篇文章翻译成了俄罗斯文



在开始之前



在 js里面,有六种原始数据类型

booleans - true - false

null

undefined

number 

string

symbol (new in es6)

 除了六种原始数据类型,ECMAsript 标准还定义了有一个对象类型,对象是一个键值对的集合

```
const object = {
  key: "value"
}
```



总的来说,在 js中除了原始数据类型,就是一个对象,包括函数和数组.

总的来说,所有的函数都是对象



```
// Primitive types
true instanceof Object; // false
null instanceof Object; // false
undefined instanceof Object; // false
0 instanceof Object; // false
'bar' instanceof Object; // false

// Non-primitive types
const foo = function () {}
foo instanceof Object; // true
```



原始类型

原始类型是没有方法的,所有你从来不会看到 undefined.toString().因此原始类型是固定不变的,因为它没有方法使他变化.

你可以重新给一个原始类型一个变量,但是这会是一个新的值,老的值不会,也不能改变



原始类型是永远不变的



除此之外,原始类型存储时是存他们的值本身,不像对象,存储的是一个引用地址,当要执行检查相等的时候就会出现问题.

```
"dog" === "dog"; // true
14 === 14; // true

{} === {}; // false
[] === []; // false
(function () {}) === (function () {}); // false
```

原始类型是存储为一个值,对象是存储为一个引用



函数



函数是一个特殊类型的对象,有一些特殊的属性,像构造和 call

```
const foo = function (baz) {};
foo.name; // "foo"
foo.length; // 1
```

就像一个普通对象一样,你可以添加新的属性到对象上面

```
foo.bar = "baz";
foo.bar; // "baz"
```

这使得函数像是第一等公民一样,因为可以把函数传到别的函数里面,就像其他对象一样.



方法

函数同时也可以用方法

```
const foo = {};
foo.bar = function () { console.log("baz"); };
foo.bar(); // "baz"
```

构造函数

构造函数和别的函数没啥不同,当一个函数使用了 new 关键字之后,他就当做构造函数来使用了.

任何函数都可以是构造函数



```
const Foo = function () {};
const bar = new Foo();
bar; // {}
bar instanceof Foo; // true
bar instanceof Object; // true
```

一个构造函数会返回 object,你可以使用 this 在函数里面赋值一个新的属性给对象,所以如果我们想要创建许多包含属性 bar 属性伴随着值是 baz的对象.我们可以创建一个新的构造函数 foo 来封装我们的逻辑.

```
const Foo = function() {
this.bar = 'baz';
}
const qux = new Foo()
qux: // {bar :'baz'} 
qux instanceof Foo; //true
qux instanceof Object; //true

```

> 你可以使用构造函数来创建一个新的对象.

使用一个像 Foo()这样子的构造函数,没有使用 new的话,就会像一个普通函数,函数里面的 this 值会应用到执行的上下文.所以,如果我们在所有函数的外面调用 Foo(),就会修改 window 这个对象.

```
Foo();//undefined

window.bar; //'baz'
```

相反的,把一个普通的函数当做一个构造函数来执行的话,会返回一个空对象,就像你早就看过的那样

const pet = new String('dog');

包装类型

这种混淆是由于字符串,数字,布尔值,函数等,当使用 new 的时候,创建一个包装对象给原始类型.

字符串是一个全局的函数,在创建原始字符串是会传入一个参数,他会将该参数转换为字符串.

```
String(1337); // "1337"
String(true); // "true"
String(null); // "null"
String(undefined); // "undefined"
String(); // ""
String("dog") === "dog" // true
typeof String("dog"); // "string"
```



但是你也可以使用 String 函数当做构造函数



const pet  = new String('dog')

typeof pet ; // 'object'

pet === 'dog' ; // false

这个表示会创建一个新的字符串对象"dog" 属性如下



```
{
  0: "d",
  1: "o",
  2: "g",
  length: 3
}
```

> 对象包装器通常也叫包装对象 ,想一想吧



自动包装



有趣的是，原始字符串和对象的构造函数都是字符串函数。更有趣的是，您可以在基元字符串上调用.constructor，当我们已经讨论基元类型不能有方法时！

```
const pet = new String("dog")
pet.constructor === String; // true
String("dog").constructor === String; // true
```

正在发生的是一个叫做自动包装的过程。当您尝试对某些基元类型调用属性或方法时，javascript将首先将其转换为临时包装对象，并访问其上的属性/方法，而不会影响原始对象。

```
const foo = "bar";
foo.length; // 3
foo === "bar"; // true
```



在上面的示例中，为了访问属性长度，javascript将foo自动打包到包装对象中，访问包装对象的长度属性，然后丢弃它。这样做不会影响foo（foo仍然是原始字符串）。



这也解释了为什么当您试图将属性分配给基元类型时，JavaScript不会抱怨，因为分配是在临时包装对象上完成的，而不是基元类型本身。

```
const foo = 42;
foo.bar = "baz"; // Assignment done on temporary wrapper object
foo.bar; // undefined
```

如果您尝试使用没有包装对象的基元类型（如Undefined或null），它将报错。

```
const foo = null;
foo.bar = "baz"; // Uncaught TypeError: Cannot set property 'bar' of null
```

总结

1.在 js中不是万物皆对象

2 在 js 中有六种原始类型

3 在 js 中不是原始类型就是对象

4 函数是一个特殊的对象

5 函数可以用来创建一个新的对象

6 字符串,布尔值,数字,可以看做一个原始类型,但是同时也是一个对象

7 有些原始类型(字符串,数字,布尔值)的行为像一个对象,因为js的特性自动装箱



