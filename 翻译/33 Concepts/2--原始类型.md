js 有以下不同的原始类型

Booleans

Strings

Numbers

null

undefined(void 在流动类型里面)

Symbols (es6)

原始类型出现在语言中就是字面意思

```
`true; "hello"; 3.14; null; undefined; `
```

或者或者是构造函数包裹在对象里面 

```
new Boolean(false);
new String("world");
new Number(42);
Symbol("foo");
```

值的类型是小写的

```
// @flow
function method(x: number, y: string, z: boolean) {
  // ...
}

method(3.14, "hello", true);
```

包装对象的类型是大写的(与他们的构造函数相同)

```
// @flow
function method(x: Number, y: String, z: Boolean) {
  // ...
}

method(new Number(42), new String("world"), new Boolean(false));
```

这些包装对象很少使用



Booleans

布尔值在 JavaScript 的值是 true 和 false.Flow中的布尔类型接受这些值。

```
// @flow
function acceptsBoolean(value: boolean) {
  // ...
}

acceptsBoolean(true);  // Works!
acceptsBoolean(false); // Works!
acceptsBoolean("foo"); // Error!
```

js 也可以含蓄地把别的值转成布尔值

```
if (42) {} // 42 => true
if ("") {} // "" => false
```

Flow 了解这些转换,并允许他们中的任何一个作用 if 语句或者别的类型的表达式的一部分.

布尔类型需要通过转换非布尔值来显式化。

```
`// @flow function acceptsBoolean(value: boolean) {   // ... }  acceptsBoolean(0);          // Error! acceptsBoolean(Boolean(0)); // Works! acceptsBoolean(!!0);        // Works! `
```

要知道 Boolean 和 boolean是不同的类型

boolean是一个想 true 或者 false 的文字值,或者是 a===b 表达式的结果.

BooleanBoolean是由全局new Boolean（x）构造函数创建的包装器对象。



Number



不像其它的语言,js 只有一个类型的数字,这些只可能是想 42 或者 3 的值,js 也包括 infinity 和 NaN.数字类型捕获 JavaScript 认为是数字的所有内容.

```
// @flow
function acceptsNumber(value: number) {
  // ...
}

acceptsNumber(42);       // Works!
acceptsNumber(3.14);     // Works!
acceptsNumber(NaN);      // Works!
acceptsNumber(Infinity); // Works!
acceptsNumber("foo");    // Error!
```

要记住 number 和 Number 是不同的类型



一个 number 既有可能是 42 或者 3 的值也有可能是一个 parseFloat(x)的值.

Number 是由全局新的 Number 构造函数创建的包装器对象.









strings

字符串是JavaScript中的“foo”值。 Flow中的字符串类型接受这些值。

```
// @flow
function acceptsString(value: string) {
  // ...
}

acceptsString("foo"); // Works!
acceptsString(false); // Error!
```

JavaScript通过连接将其他类型的值隐式转换为字符串。

```
"foo" + 42; // "foo42"
"foo" + {}; // "foo[object Object]"
```

Flow只会在将它们连接到字符串时接受字符串和数字。





您必须明确并将其他类型转换为字符串。 您可以使用String方法或使用其他方法对字符串化值进行此操作。





null 和 void 

JavaScript具有null和undefined。 Flow将这些视为单独的类型：null和void（对于undefined）。

```
`// @flow function acceptsNull(value: null) {   /* ... */ }  function acceptsUndefined(value: void) {   /* ... */ }  acceptsNull(null);      // Works! acceptsNull(undefined); // Error! acceptsUndefined(null);      // Error! acceptsUndefined(undefined); // Works! `
```

null 和 void 同样出现在别的类型里面.



Maybe types 

也许类型适用于值是可选的地方，您可以通过在类型前添加问号来创建它们，例如？string或？number。

除了？类型之外，类型也可以为null或void。



```
// @flow
function acceptsMaybeString(value: ?string) {
  // ...
}

acceptsMaybeString("bar");     // Works!
acceptsMaybeString(undefined); // Works!
acceptsMaybeString(null);      // Works!
acceptsMaybeString();          // Works!
```

optional boject properies (可选对象属性)

对象类型可以有可选属性，是一个问号？跟在 属性名称后面。

```
{ propertyName?: string }
```

对象可以有可选属性,当有一个?跟在 param名字后面

```
// @flow
function acceptsObject(value: { foo?: string }) {
  // ...
}

acceptsObject({ foo: "bar" });     // Works!
acceptsObject({ foo: undefined }); // Works!
acceptsObject({ foo: null });      // Error!
acceptsObject({});                 // Works!
```

optional function parameters  (函数可选参数)

函数可以有可选参数当有一个?跟在 param名字后面

function method(param?: string) { /* ... */ }

除了他们的集合类型,可选参数可以是无效或者省略,但是不能是 null..



funtion  parameters weith defaults(函数默认参数)



函数的参数也可以有默认值,这是 es6 的新特性

```
function method(value: string = "default") { /* ... */ }
```

除了他们的集合类型,默认参数可以是无效或者省略,但是不能是 null..

```
// @flow
function acceptsOptionalString(value: string = "foo") {
  // ...
}

acceptsOptionalString("bar");     // Works!
acceptsOptionalString(undefined); // Works!
acceptsOptionalString(null);      // Error!
acceptsOptionalString();          // Works!
```

symbols 

symbols 现在还不被 flow 支持,你可以查看关于这些问题在

- [facebook/flow#810](https://github.com/facebook/flow/issues/810)
- [facebook/flow#1015](https://github.com/facebook/flow/issues/1015)

