





在面向对象的 js中,万物皆对象,因为所有的都是一个对象,我们了解到我们可以设置和访问函数的属性.

给一个函数设置一个属性和给函数添加方法是很棒的,但是我们是怎么做到的?



我们要介绍一下 this 关键字.我们了解到每个函数都会自动获得 this 这个属性.如果我们要为这个函数创建一个模型,(我不是孤例对吧)他会想是这样子的:

![img](https://miro.medium.com/max/1400/1*oGDRHlH5QWXTFTenWvMaBw.png)

我们花了一点时间才熟悉this关键字，但一旦我们了解this用处，我们就开始意识到它是多么有用。这是在函数内部使用的，并且总是引用单个对象——调用（调用）使用“this”的函数的对象



但是事情不是完美的,有时候我们会失去this 的指向.当这个事情发生了,我们最后会迷惑的保存this 的指向,查看具体的例子[例子](https://github.com/Arieg419/ITCCodingBootcamp/blob/master/localStorage/eBay.js)

我为啥要保存 this 的指向,因为deleteBtn.addEventListener的 this 指向的*deleteBtn*对象. 这是不幸的,有个没有解决办法?

call(),apply()和 bind() - 新的希望

到现在我们把函数当做一个有名字的对象(可选择的,同样可以是一个匿名函数),当她被调用的时候被执行.但这不是所有的真相,做完一个有爱的人儿,我有必要让你知道函数实际上看起来是下面这样子的:



![image-20190811170841394](/Users/tongzhirong/Library/Application Support/typora-user-images/image-20190811170841394.png)

这是啥?别担心,我会通过三个相识的方法添加到函数上面,通过例子让你明白.





bid()

官方的说法是: 这bind()方法创建了一个新的函数,当他被调用时,将其 this 关键字设置为提供的值(实际上有很多东西可以谈,但是我们留到下一下)





这是很强大的,让我们在调用的时候明确的定义 this 的值 ,让我们看下代码

var pokemon = {

​	fistname : 'Pika',

​	lastname: 'Chu',

​	getPokeName: function() {

​		var fullname = this.fistname + ''  + this.lastname;

​	return fullname;

}



 var pokemonName = function () {

console.log(this.getPokeName()+ 'i choose you ')

}

var logPokemon = pokemonName.bing(pokemon); }

让我们解释一下,当我们使用 bind()方法



1 js 引擎会创建一个新的 pokemonName 实例,然后绑定 pokemon 作为他的 this 的变量.这是很重要的如何理解复制 pokemonName 函数



2.在创建一个复制的 pokemonName 函数,让他去调用 logPokemon() 尽管它原本不是在 pokemon 对象上面,但现在回自动作为他的属性(Pika 和Chu)和方法



最棒的事情是,在我们绑定了一个值之后,我们可以像使用普通函数一样使用它,我们甚至可以让函数接受参数,然后传递

```
var pokemon = {
    firstname: 'Pika',
    lastname: 'Chu ',
    getPokeName: function() {
        var fullname = this.firstname + ' ' + this.lastname;
        return fullname;
    }
};

var pokemonName = function(snack, hobby) {
    console.log(this.getPokeName() + 'I choose you!');
    console.log(this.getPokeName() + ' loves ' + snack + ' and ' + hobby);
};

var logPokemon = pokemonName.bind(pokemon); // creates new object and binds pokemon. 'this' of pokemon === pokemon now

logPokemon('sushi', 'algorithms'); // Pika Chu  loves sushi and algorithms
```





call(),apply()



call()的官方文档说的是:call 方法调用一个函数,并单独提供this 和arguments给函数



这就是说,我们可以调用任何函数,并指明具体的 this 指向.

有点像 bind()方法.这个可以把我们从垃圾代码中解放出来



bind 和 call 方法主要的区别是:call 方法



1.可以接受别的参数

2立即执行调用它的函数

3call 方法不会复制正在调用它的函数



call 和 apply 服务于一个确定的目标,他们的区别是 call 预期传递的参数都是独立的,apply 预期是一个数组的参数





```
var pokemon = {
    firstname: 'Pika',
    lastname: 'Chu ',
    getPokeName: function() {
        var fullname = this.firstname + ' ' + this.lastname;
        return fullname;
    }
};

var pokemonName = function(snack, hobby) {
    console.log(this.getPokeName() + ' loves ' + snack + ' and ' + hobby);
};

pokemonName.call(pokemon,'sushi', 'algorithms'); // Pika Chu  loves sushi and algorithms
pokemonName.apply(pokemon,['sushi', 'algorithms']); // Pika Chu  loves sushi and algorithms
```



这些内置;的方法,每一个都是非常有用的,即使你不打算在平常写代码中使用,但是当你读别人的代码时候还是有经常运行的.



如果你有任何问题,老地方,来 Instagram找我.





















原文地址:

https://medium.com/@omergoldberg/javascript-call-apply-and-bind-e5c27301f7bb
