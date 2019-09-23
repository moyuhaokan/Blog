我最后一篇文章是Typescript关于“class 对比 继承”，我很开心有很多反馈，在反馈当中，我看到有些人对于clsses的迷惑。

所以今天文章的主题会围绕下面这句话来写：

> 自从ES2015标准发布以来，纯JavaScript就具有合适的class



我会告诉你为什么...



这里是不久前一个我们实例化“classes”的例子。第一个函数会是一个构造函数，所以我们有了一个Cat 的class和在class中有一个meow的函数：

![1*y4PkgnYJmLPur2MVzIJZ4A](https://miro.medium.com/max/1614/1*y4PkgnYJmLPur2MVzIJZ4A.jpeg)



要点： 如果你忘记了new关键字会咋样？答案是不会抛出任何错误.. 只是会绑定到window上面

![1*gdfxdrn_ErN5dfyYpQx77g](https://miro.medium.com/max/1258/1*gdfxdrn_ErN5dfyYpQx77g.jpeg)

prototype在哪里？

在console里面你可以看到prototype链 

![1*PYBw1HG7zT_vQAF6-JohxQ](https://miro.medium.com/max/1302/1*PYBw1HG7zT_vQAF6-JohxQ.jpeg)

你的cat是一个对象，里面有一个name的键值对，它有 一个-proto-对象，里面有一个meow函数和和Cat构造函数，这个Object或是prototype也包含一个对象（这是基本对象，类似java，那就是所以JavaScript对象的基本的prototype），你现在可以理解为什么这个叫做原型链了。

现在唯一不同于经典的class的地方是prototypes是一个引用，这意味着，如果你创建了很多cats,并且在其中的一个cat上做了这个操作

delete cat.__proto__.meow



你就删除了所有的cat上面meow方法。因为cat的引用都指向Cat prototype。



现在让我们创建一个Dog 类。别的东西都一样，但是meow方法换成了barking方法。



现在你的得到了一个狗和一个猫，让我们来做一点狗屎的，被禁止，严肃的时候永远不做的操作。

cat.__proto__ = dog.__proto__;

现在来看下我们cat里面是什么？



![1*f-priWwshYd0cRowUl_tRQ](https://miro.medium.com/max/1268/1*f-priWwshYd0cRowUl_tRQ.jpeg)

天啊，现在猫也可以汪汪叫！但是仍然是一个猫，但他其中一个prototype是狗。如果我告诉你

cat instanceof Dog === true

你可以理解为什么所有的东西都可以通过js的prototype链接。



看到没有？这就是JavaScript疯狂的地方。你可以做任何你想做的事情，即使是让你的猫汪汪叫，只需要转换他的prototype。这个问题是明显的是太自由了，由此带来了很多问题。



**我们现在有了class**

让我们重新看下MDN上面关于class的定义：

> ECMAScript 2015中引入的JavaScript类主要是语法上的糖，而不是JavaScript现有的基于原型的继承。类语法不会向JavaScript引入新的面向对象的继承模型。



如果还不够清晰，让我给你看下它在JS中没有引入新的OO模型的程度。



让我们继续我们猫狗的例子，并且使用class语法。



![1*9ropehPTGw99dAUNXYFnUQ](https://miro.medium.com/max/1854/1*9ropehPTGw99dAUNXYFnUQ.jpeg)

我们可以像任何OOP语言一样编写所有内容：类，构造函数，super，extends，甚至还添加了一个静态函数来尝试。但是我们的超级猫是什么样子？

![1*ADWWzjPuNvoHQlmpMlnIrQ](https://miro.medium.com/max/1678/1*ADWWzjPuNvoHQlmpMlnIrQ.jpeg)

我们使用extend意味着我们在原型链中增加了深度。现在我们有了一个具有名称和超能力的对象，它具有带有SuperCat构造函数的对象 **__proto__**__和您的SuperCat函数喵，其中带有__proto__等。

这意味着像以前一样，您可以删除原型的属性或方法，并且它将为您创建的每个实例销毁它。一切都没有改变……某些改变了：

![1*PPguR4GvnI61LVgRSNeMow](https://miro.medium.com/max/2066/1*PPguR4GvnI61LVgRSNeMow.jpeg)

您可以尝试像以前一样更改原型，并拥有仍然具有汪汪叫的超级猫并且还可以有厉害的MEOW，或进行其他疯狂的事情，（原型）世界现在是你的了。



现在您看到，在class关键字后面，它仍然是与以前相同的原型方法。我希望您在代码中使用它时考虑一下。

我要感谢FlorianOrpelière（@florpeliere），在我撰写本文之前不久，他就此主题发表了演讲，内容如此清晰，指导性很好，这给我带来了很多启发。



原文地址:

https://medium.com/@parsyval/javascript-prototype-vs-class-a7015d5473b

