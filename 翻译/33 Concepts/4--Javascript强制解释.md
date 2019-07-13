在我们开始学习强制转换之前,之所以写这篇文章,是因为 js 是一个无类型的语言(根据你的定义可能是弱类型)



语言类型



> 强类型编程语言是指每种类型的数据(例如,证书,字符,十六进制,压缩十进制)被预定义为语言的一部分.所有的常量和变量都必须用其中的一种数据类型.
>
> *—* [source yo](http://whatis.techtarget.com/definition/strongly-typed)





这对于我们 js使用者来说,意味着在编译的过程中强制地基于某种规则来进行类型转换.这篇文章我们会提到两个不同类型强制.明确(explicit) 和 隐含(implicit)

明确强制是使用者想要转换某个类型的值成另一个类型的值.隐含强制是非主观的操作.看一下下面的例子.

![1*stdZQImftgMzyMur_5qXcg](https://miro.medium.com/max/2000/1*stdZQImftgMzyMur_5qXcg.png)

注意例子里面的两个方法,明确(explicit)和(implicit).返回了同样的结果.这是有意思的但是也会引起一点争议.换句话说,可读性是争论的焦点.除了你之外还有人读你的代码.上面的两个方法那个更具有可读性?

从来来说,让我们看下 js 怎么处理使用==和===对比数据类型,当我们使用 null 和 undefined



######null vs. undefind

这里是一些代码例子,下面有更详细的解释(要点):

![1*Ku-MoMX5u2yyvqf4EoA0gw](https://miro.medium.com/max/2000/1*Ku-MoMX5u2yyvqf4EoA0gw.png)



以上代码主要的要点是:

null 是一个对象

undefined是它自己的不同类型undefined



#####比较

我们看一下对比不同类型的值使用相等(==)和严格相等(===)的区别





让我们强制使用JS解释器来对我们的意图做出一些猜测：

![1*abGotxTnQsToqbBC74Ez4Q](https://miro.medium.com/max/2000/1*abGotxTnQsToqbBC74Ez4Q.png)



注意 ,undefined 和 null 使用相等比较的是相等的,但是使用严格相等就是不相等.



让我们看下 String,Number 和 Boolean 的比较:

![1*IF-Usxxw9SvoLbyA_GCPpw](https://miro.medium.com/max/2000/1*IF-Usxxw9SvoLbyA_GCPpw.png)



到现在为止你可能注意到一种模式,但是使用相等比较不同类型的值的时候,js 可能会强制转换值,精准的比较要使用严格相等来达到.

######最后

强制是无类型语言之恶



我的建议是:

当你写代码是**总是**使用严格相等除非你有不这么做的理由.


一如既往,我们知道你的想法和问题,请关注我们的twitterhttps://twitter.com/_bengarrison


如果这个文章对你是有用的,点个赞让我们看到你的支持.




原文地址: https://hackernoon.com/javascript-coercion-explained-545c895213d3

