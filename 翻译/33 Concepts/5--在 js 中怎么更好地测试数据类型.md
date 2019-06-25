在 js 中想要测试一个数据类型不是那么容易的,js 语言本身提供了一个 typeof 来直接测试.typeof 会返回一个字符串,这个字符串会说明测试的数据类型.所以一个"object"会返回一个字符串"string".

然而 js的数据类型和 typeof 操作符不是那么精确的,举个例子,对于一个空的数值 typeof 会返回一个 "object"而NaN则会返回一个"number",除了查看元素数据类型之外,如果你想要查看某个值是否是数字,字符串,null,数组或者是一个真正的对象则需要更多的逻辑.

下面包含了以下的内容

- [String](https://webbjocke.com/javascript-check-data-types/#javascript-string)
- [Number](https://webbjocke.com/javascript-check-data-types/#javascript-number)
- [Array](https://webbjocke.com/javascript-check-data-types/#javascript-array)
- [Function](https://webbjocke.com/javascript-check-data-types/#javascript-function)
- [Object](https://webbjocke.com/javascript-check-data-types/#javascript-object)
- [Null & undefined](https://webbjocke.com/javascript-check-data-types/#javascript-null-and-undefined)
- [Boolean](https://webbjocke.com/javascript-check-data-types/#javascript-boolean)
- [RegExp](https://webbjocke.com/javascript-check-data-types/#javascript-regexp)
- [Error](https://webbjocke.com/javascript-check-data-types/#javascript-error)
- [Date](https://webbjocke.com/javascript-check-data-types/#javascript-date)
- [Symbol](https://webbjocke.com/javascript-check-data-types/#javascript-symbol)

string

一个字符串永远是字符串,所有判断字符串是容易的,除了使用 new typeof 调用,会返回"object",因此也可以使用instanceof来包含这些字符串

```js
// Returns if a value is a string
function isString (value) {
    return typeof value === 'string' || value instanceof String;
}
```

number

从类型上看，比普通数字更大的东西会返回“number”，比如NaN和无穷大。想要知道摸个只是否是数字我们还需要用到 isFinite 函数

```js
// Returns if a value is really a number
function isNumber (value) {
    return typeof value === 'number' && isFinite(value);
}
```

array

在 js中 数组并不像 java 或者是其它的语言一样是真的数组,数组实际上是一个对象,所以使用 typeof 会返回"object",为了知道是不是数组可以让它的构造函数与数组进行对比.



```

```

function

函数就是函数所以 typeof 足够了.



```
// Returns if a value is a function
function isFunction (value) {
    return typeof value === 'function';
}
```

object

在 js 中很多东西都是对象,想要知道某个值是否是对象,只需要轮混一下他的properties即可,他的构造函数是一个对象,但是从 clsses 里面继承过来的是不起作用的,这种情况下可以使用instanceof 运算符.

```
// Returns if a value is an object
function isObject (value) {
    return value && typeof value === 'object' && value.constructor === Object;
}
```

null 和 undefined

许多时候你不需要测试精确 null 和 undefined 的值,这是因为他们都是虚值.然而下面的函数还是用技巧做到了.

```
// Returns if a value is undefined
function isUndefined (value) {
    return typeof value === 'undefined';
}
// Returns if a value is null
function isNull (value) {
    return value === null;
}

```

boolean 

对于布尔值来说,typeof 已经足够了.不管这个布尔值是 false 还是 true

```
// Returns if a value is a boolean
function isBoolean (value) {
    return typeof value === 'boolean';
}
```

regexp

正则是一个对象,所有唯一需要知道的就是查看构造函数是否是Regex

```
// Returns if a value is a regexp
function isRegExp (value) {
    return value && typeof value === 'object' && value.constructor === RegExp;
}
```

error 

javascript中的错误与许多其他编程语言中的“异常”相同。它们有两种不同的形式，例如错误、类型错误和范围错误。InstanceOf语句足以满足所有这些要求，但要确保我们还检查了错误所具有的“Message”属性。

```
// Returns if value is an error object
function isError (value) {
    return value instanceof Error && typeof value.message !== 'undefined';
}
```

date

时间不是一个 data 类型,但是想要查看的话可以使用 instanceof

```
// Returns if value is a date object
function isDate (value) {
    return value instanceof Date;
}
```

symbol 



es6 新加的数据类型,不需要过多的逻辑,直接使用 typeof 就可以.

```js
// Returns if a Symbol
function isSymbol (value) {
    return typeof value === 'symbol';
}
```

以上就是目前为止所有的类型了,如果你觉得有错误的地方或者遗漏的地方你可以留下你的评论,想要查看更多关于 js的数据类型的可以查看[developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures).