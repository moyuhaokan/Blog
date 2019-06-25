我们都知道在 js 中有两种不同的相等比较运算符;==和===运算符,或者叫做非严格相等和严格相等,你看见它们两个都可以用,但是不知道应该选择哪一个用到你的代码上面,你想知道一个可靠的方法来决定使用这个或者另一个.

事实上,这里有一个直接的方法来决定使用哪一个,同样的逻辑适用于不相等运算 !== 和 != .



##### 比较相同的类型使用 ===

```
1 x === y
```



严格相等会返回 true,如果两个操作数类型相等并且他们的值是一样的,如果对比不同的类型,返回的是 false.

这个相等的定义对大多数情况下都已经都用了,当比较字符串"0"和数字0 ,如我们的预期的一样,返回 false.

很多文档类似  [D. Crockford](https://bytearcher.com/articles/douglas-crockford-javascript-good-parts-book-review/) and [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness#Loose_equality_using) 都建议在程序中使用严格相等,忽略不严格相等.

##### 复合型类型转换 ==

```
1 x == y
```

两个等号的操作(==) 遇到不同的 类型比较时会尝试转换类型,如果类型不同,其中的一个或者两个都会转换成公共类型,转换的规则比较复杂而且取决于参数的类型,想要看全部的转换规则,参考 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness#Loose_equality_using) or the [ECMAScript specification](http://ecma-international.org/ecma-262/5.1/#sec-11.9.3).

举个例子,当比较字符串'0'和数字 0,第一个参数会转换成数字 0

```
1 "0" == 0 // becomes
2 ToNumber("0") === 0
```

字符串和数字的比较还是可理解的,其他类型的转换规则就是不易理解的了,举子例子,当在 null,undefined和 false 比较时:

```
1 false == undefined // false
2 false == null      // false
3 null == undefined  // true
```

##### 现在你知道了吧 - 只使用 ===

使用严格相等对比两个操作数,当尝试用严格相等对比两个不同的类型的时候,返回的永远是 false,你将得到你想要的结果,而不用去记忆哪些复杂的转换规则,就像对比苹果和橘子永远返回 false.



注意,这些对比的相等符号只是对比原始类型,想要对比对象或者数组的深度相等性,需要一种不同的方法来对比它们的数据结构.