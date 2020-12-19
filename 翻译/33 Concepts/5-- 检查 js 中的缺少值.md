当我第一次学习 js 的时候我总是很迷惑 js 的检查某个值.

```js
console.log(value == null)
console.log(value === null)
console.log(value == undefined)
console.log(value === undefined)
console.log(value === undefined || value === null)
console.log(typeof value === 'undefined')
console.log(typeof value == 'undefined')
console.log(typeof value === 'undefined' || value === null)
console.log(typeof value === 'undefined' || value == null)
console.log(typeof value == 'undefined' || value == null)
console.log(typeof value == 'undefined' || value === null)
console.log(!value)
```

上面哪一个是正确的?

想要理解上面的表达式,我们需要先看下 js 的两种表示缺少值的方式.

###### undefined

undefined 是原始类型的一种,这意味着我们使用 typeof操作符会返回'undefined',

console.log(typeof undefined) // undefined

它是所有已经声明但没有赋值的的默认值

```
var x
console.log(x) // undefined
```

当尝试接受一个没有声明的对象属性也会返回 undefined

```
var obj = {}
console.log(obj.a) // undefined
```

当想要返回一个函数的值,但是函数并没有返回值

```
function f() {}
console.log(f()) // undefined
```

当使用 void 操作符的时候会返回 undefined,一个运算符，它计算表达式然后返回undefined

```
console.log(void 0) // undefined
console.log(void 'hello') // undefined
console.log(void(3 + 2)) // undefined
console.log(void(/* any expression */)) // undefined
```

最后,undefined 不是一个字面意思的变量或者属性,他是全局对象的一个属性,全局对象永远存在于全局的作用域(可以用过浏览器的 window对象来访问)

###### null

