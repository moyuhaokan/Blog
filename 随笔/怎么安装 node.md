怎么安装 node.js





node.js 有多种安装方式，这篇文章介绍一下常用且最方便的。



包含主要平台的官方包：https://nodejs.org/en/download/.



有一种最简单的方式是通过包管理器来安装 node.每个都有属于自己的包管理器。



在 macOS ，homebrew 是事实上的标准，安装 homebrew 后，运行你通过 homebrew 很方便的安装 node.js。只需要在命令行运行 ：

brew install node





Linux 和 Window 的包管理列表在：https://nodejs.org/en/download/package-manager/





nvm 是一个很受欢迎的运行 node.js 的方式。比如：它很方便切换 node的版本，安装新版本来尝试新功能并且在遇到错误的情况下很方便的回滚。





它也是一种非常有用的帮助测试使用 ndoe.js 老版本的代码。



可以在 https://github.com/nvm-sh/nvm 上面查看更多帮助



如果你是刚刚开始学习并且没有使用过 Homebrew，我的建议是使用使用官方的方式安装。虽然 Homebrew 是我的最爱。



不管怎么样，当你安装了 node之后，你都可以在命令行里面运行 node 的项目。





如果你要用 node,你需要知道多少 JavaScript 的





作为新手，你很难达到一个点说你对自己的编程能力足够自信了





当你开始学习编程时，你可能会疑惑什么时候结束 JavaScript，什么时候开始 node,反之亦然。



在你学习 nod之前我推荐你去学习这些 JavaScript 的主要概念：



词法结构

表达式

类型

变量

函数

this

箭头函数

循环

作用域

数组

模板文字

分号

严格模式

ES 6 ，7，8





当这些概念在你脑中都比较清晰的时候，不管是在浏览器还是 node 中，你都准备成为一个优秀的 JavaScript 开发者了。



下面的概念是理解异步编程的关键，也是 node 的基础部分：



异步编程和回调

定时器

Promises

Async and Await

闭包

事件循环



