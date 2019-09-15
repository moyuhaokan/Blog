原文地址:
this 是 JavaScript 最棘手的概念之一,简而言之,this 指向执行上下文.



全局上下文



当在任何函数或者类(实际上只是函数)时,这指的是全局执行上下文,它是 web 浏览器的窗口.

```
this; // window
this.foo = "bar";
window.foo; // "bar"
```

在 node.js 中.this 在 全局上下文是指出口对象,默认是指一个 空对象.



函数上下文



当 this 在函数里,this 的值是指向函数调用的地方.例如:

```js
const bar = function () { console.log(this) };
const foo = {};
foo.bar = bar;

bar(); // window
foo.bar(); // bar
```



函数

当一个函数在全局里面被调用,this 指向全局的上下文.

const bar = function() { console.log(this)};

bar(); //window



函数不会影响其正文的执行上下文。

const foo = function () { bar();}

foo(); //window



严格模式

在函数内部,this 的值也取决于严格模式是否开启.没有严格模式,this 是全局对象(window),严格模式情况下,它是一个 undefined.

```js
const foo = function () { console.log(this) };
const bar = function () { 'use strict'; console.log(this); };

foo(); // window
bar(); // undefined
```

构造函数

一个函数当使用 new 关键字的时候可以是一个构造函数.构造函数像一个模板一样创建新的对象.并在es6 中加入到类里面.

当一个函数被用作构造函数,函数内部的 this 指向正在构建的对象.

```js
function Car(make) {
  this.make = make;
}

const myCar = new Car("BMW");
myCar.make; // "BMW"
```

自从在 es6 中构造函数被糖化成类.es6 的类构造函数也是如此.



```js
class Car {
  constructor(make) {
    this.make = make;
  }
}

const myCar = new Car("BMW");
myCar.make; // "BMW"
```

prototype

函数也可以在它的prototype对象里面定义方法.this 指向调用此方法的对象实例.

```js
Car.prototype.getMake = function () {
  return this.make;
}

myCar.getMake(); // "BMW"
```



同样，原型对象等同于类的原型方法，因此适用相同的规则。

```
class Car {
  constructor(make) {
    this.make = make;
  }

  getMake() {
    return this.make;
  }
}
const myCar = new Car("BMW");
myCar.getMake(); // "BMW"
```

对象方法/静态方法



如果一个函数是对象的一个方法的话,那么 this 指向这个对象.

```
const foo = {};
foo.bar = function () { console.log(this); };
foo.bar(); // foo
```

自从每一个函数都是一个对象,this 相当于类中的静态方法.

```js
class Car {
  constructor(make) {
    this.make = make;
  }

  static convertKmToMiles(km) {
    return km * this.kmToMilesConversionRate;
  }
}
Car.kmToMilesConversionRate = 0.621371;
Car.convertKmToMiles(42); // 26.097582
```



另一个例子是,当你运行 window.setTimeout时,在 setTimeout 中,this指的是window 对象



```js
const foo = {};
foo.bar = function () {
  window.setTimeout(function () {
    console.log(this);
  }, 0);
};
foo.bar(); // window
```



绑定 this



如果你想让 函数内的 this 确定地指向一个确定的对象,你可以使用函数的 bind 方法.



```js
const foo = function () { console.log(this) };
const boundFoo = foo.bind("always me!");

foo(); // window
boundFoo(); // "always me!"

const a = {
  b: foo,
  boundB: boundFoo
}
a.b(); // a
a.boundB(); // "always me"

bar = function () {};
bar.prototype.x = foo;
bar.prototype.boundX = boundFoo;

const myBar = new bar();

myBar.x(); // myBar
myBar.boundX(); // "always me"
```

call 和 apply



Function.prototype.bind 返回一个新的函数绑定到一个对象上.但不会调用这个函数,Function.prototype.call 和Function.prototype.apply 是立即调用这个函数,并把 this 的值传递过去.



call 和 apply 的不同之处在于,call 希望直接传递一个列表进去.apply 希望传递一个数组

```
const foo = function (x, y) {
  console.log(this);
  console.log(x);
  console.log(y);
};

foo(); // window, undefined, undefined
foo.call(); // window, undefined, undefined
foo.call("Yo!"); // "Yo!", undefined, undefined
foo.call("Yo!", 1, 2); // "Yo!", 1, 2
foo.apply("Yo!", [1, 2]); // "Yo!", 1, 2
```

ES6 / ES7 



在 es6 中,有 两种方式会影响 this 的绑定



- Arrow functions
- `Reflect.apply()`



在 es7 中,有新的::绑定操作符



箭头函数



箭头函数会自动绑定 this 到函数内部

```
function Car (make) {
  window.setTimeout(function () {
    console.log(this); // window
  }, 0);
  window.setTimeout(() => {
    console.log(this); // Car
  }, 2000)
}

new Car();
// window
// Car
```



**Reflect.apply()**

Reflect.apply() 是Function.prototype.apply.的另一种写法.



```
const foo = function (x, y) {
  console.log(this);
  console.log(x);
  console.log(y);
};

foo.apply('a', ['b', 'c']); // 'a', 'b', 'c'
Reflect.apply(foo, 'a', ['b', 'c']) // 'a', 'b', 'c'
```

它们等同于一些警告，其中最相关的是你可以覆盖对象的apply方法，而Reflect.apply将始终等于Function.prototype.apply

##### `::` 操作符合

:: bind运算符是一个建议的运算符，它将对象的方法绑定到对象本身。












http://blog.brew.com.hk/what-is-this-in-javascript/
