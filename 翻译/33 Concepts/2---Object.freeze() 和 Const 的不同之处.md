es6 发布带来了不少新的特性和方法.这些特性和提高我们的前端开发者的工作效率.其中就有Object.freeze() 方法和 const

对于这两个特性工作的方式是否一样有很多争议,特别是是新手来说,但他们并不是一样的,让我来告诉你吧.



######概要

const 和 Object.freeze() 是完全不一样的.

const 的更像是let,他定义一个变量之后不能再重新赋值.使用 const定义变量是有一个块作用域,不像是 var 有一个函数作用域.

Object.freeze（）接受一个对象作为参数，并返回与不可变对象相同的对象。 这意味着不能添加，删除或更改对象的任何属性。

> 可变对象的属性是可以改变的,不可变对象当被创建的时候属性就不可以变了

######例子

const

```
const user = 'Bolaji Ayodeji'
user = 'Joe Nash'
```

这会抛出一个 `Uncaught TypeError` ,因为我们尝试重新给 user 赋值.但是 user 已经使用 const 定义过了.这是没有效果的.

![img](https://miro.medium.com/max/60/1*fkm8tv7a1jdhQSWa1Hl5tg.png?q=20)

![img](https://miro.medium.com/max/846/1*fkm8tv7a1jdhQSWa1Hl5tg.png)

最初的时候,适用于 var 和 let 但不适用于 const



const 的问题

当我们使用 Objects,使用 const 能够预防重新赋值,但不是不可变(不能阻止更改其属性)

看一下下面的代码,我们使用 const 定义了一个user变量,并给变量赋值一个对象

```
const user = {
  first_name: 'bolaji',
  last_name: 'ayodeji',
  email: 'hi@bolajiayodeji.com',
  net_worth: 2000
}
user.last_name = 'Samson';
// this would work, user is still mutable!
user.net_worth = 983265975975950;
// this would work too, user is still mutable and getting rich :)!
console.log(user);  // user is mutated
```

#####![1*fXjTs7lGxDXd3bFv2rF1Vg](https://miro.medium.com/max/1400/1*fXjTs7lGxDXd3bFv2rF1Vg.png)



尽管我们不能够重新赋值,但是我们可以改变这个对象本身.



```
const user = {
  user_name: 'bolajiayodeji'
}
// won't work
```

![1*hxSHWKuB8nopFHif_ETW9g](https://miro.medium.com/max/1184/1*hxSHWKuB8nopFHif_ETW9g.png)



我们想要对象不能被修改或是删除属性,const 不能做到这一点,但是Object.freeze()可以做到



######Object.freeze()

想要在对象禁止任何操作我们需要Object.freeze()

```
const user = {
  first_name: 'bolaji',
  last_name: 'ayodeji',
  email: 'hi@bolajiayodeji.com',
  net_worth: 2000
}
Object.freeze(user);user.last_name = 'Samson';
// this won't work, user is still immutable!
user.net_worth = 983265975975950;
// this won't work too, user is still immutable and still broke :(!
console.log(user);  // user is immutated
```

![1*uiv64RdHsencUe9ZKptrbw](https://miro.medium.com/max/1322/1*uiv64RdHsencUe9ZKptrbw.png)

######对象的嵌套属性对象并不是完全不能修改

好吧,Object.freeze()是浅层次的不可改变,好吧，Object.freeze（）有点浅，您需要将它应用于嵌套对象以递归地保护它们。

```
const user = {
  first_name: 'bolaji',
  last_name: 'ayodeji',
  contact: {
    email: 'hi@bolajiayodeji.com',
    telephone: 08109445504,
  }
}
Object.freeze(user);user.last_name = 'Samson';
// this won't work, user is still immutable!
user.contact.telephone = 07054394926;
// this will work because the nested object is not frozen
console.log(user);
```

![1*xL0vmY5YC7n3hq5SfIT-Vg](https://miro.medium.com/max/1286/1*xL0vmY5YC7n3hq5SfIT-Vg.png)





所以Object.freeze()不是完全冻结的当他的属性嵌套的时候

想要完全不能修改的对象和不能修改的嵌套属性,你可以写一个自己的库,或者是使用[Deepfreeze](https://github.com/substack/deep-freeze) or [immutable-js](https://github.com/immutable-js/immutable-js)



#####结论

const 和 Object.freeze() 是不一样的,const 是预防重新赋值,Object.freeze() 是预防改变属性.

PS 这个文章首发于我的[博客](https://bolajiayodeji.com/object.freeze-vs-const/)

感谢你的阅读,撒花!

原文地址: https://medium.com/@bolajiayodeji/the-differences-between-object-freeze-vs-const-in-javascript-4eacea534d7c