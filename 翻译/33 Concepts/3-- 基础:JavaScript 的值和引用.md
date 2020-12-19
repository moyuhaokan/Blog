

让我们看下值和引用这两个概念.通常这是 出现 bug 的原因.同样的也是面试常见问题.

我会尽量通俗易懂的通过这篇短文来说明这两个概念.

不要阅读的太快,你知道这两个例子都会返回什么吗?



```js
console.log([10] === [10]);
```



```js
var oldArray = [];
var object = {};object.newArray = oldArray;
oldArray.push(10);console.log(object.newArray === oldArray);
```



第一个是 false,第二个是 true.你的答案是对的吗?让我们看下为什么吧?

在 js 中有的类型是复制它的值有的是复制引用地址.它们具体是:

**原始类型(复制值)**

- null
- undefined
- Number
- String
- Boolean

**对象(复制引用)**



- Object
- Array
- Function

######原始类型

var a = 5;

var b = a;

a = 10;

console.log(a); //10

console.log(b);//5

//这同样适用于 String,Boolean,null,undefined



当我们给一个变量赋值原始类型,我们是复制**值**



######对象

现在疑惑的地方是

var a = {};

var b = a;

a.a= 1;

console.log(a); // {a:1}

console.log(b); // {a: 1}



这同样适用于**数组**

var a = [];

var b = a;

a.push(1);

sonsole.log(a); //[1]

console.log(b); //[1]

console.log(a === b); //true

当我们给一个变量赋值对象(非原始类型),我们复制的是引用.你可以想象,当我们声明一个变量 a 我们在内存新建了一个地址,然后我们声明一个变量b,但是只是把指向指到 a 的地址.所有当我们更新这个地址的东西时,变量 a 和变量 b 的值是相同的.



```js
var a = [];     # Address #001 -> []
                # Variable a -> #001var b = a;      # Variable b -> #001a.push(1);      # Address #001 -> [1]Variable | Address | Value
a        | #011    | [1]
b        | #011    | [1]
```

######关于 [10] === [10] 的例子

但我们比较对象,相等操作符(===)会查看他们是否指向同一个地址,如果[10]和[10]是两种不同的数组,结果会返回一个 false.就像最后一个例子一样.当你想要对象或者数组的值,有个一个简单但是作用有限的方式.

JSON.stringify(a) === JSON.stringify(b)

虽然如果两个对象/数组的属性的顺序不同，它将返回false。 如果你想要更好的方式,你可以使用lodash _.isEqual（）或者按照[stackoverflow ](https://stackoverflow.com/questions/1068834/object-comparison-in-javascript)



######总结

关于这个主题还有更多内容,我可能会写更多关于纯函数/污染函数,不变性.怎么复制一个object/array 变量但是变量不被改变等等..点赞这篇文章,然我更有动力,不要忘记关注我,以防错过更新.



原文地址: https://medium.com/dailyjs/back-to-roots-javascript-value-vs-reference-8fb69d587a18

