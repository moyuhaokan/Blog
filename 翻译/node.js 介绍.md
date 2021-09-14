node.js 是一个开源且跨平台的 JavaScript 运行环境。在几乎所有的的项目都很受欢迎。





node.js 是运行在浏览器外的谷歌 Chrome JavaScript V8引擎。这使得 node.js 变得很高效。



node的应用是单线程运行的，不会每一个请求都创建一个线程。node.js的标准库 提供了一套异步的 I/O 操作，预防 JavaScript 的代码阻塞流程。



node.js 是用非阻塞的范例来编写的，使阻塞行为会成为例外。



当 node.js 执行一个 I/O 程序，比如从请求从读取数据，进入数据库或者是文件系统。相对于阻塞线程和CPU 等待，node 会在回调返回的时候重新启动应用，继续执行。



这使得 node 可以使用单线程处理几千的并发连接而不用引起并发管理的负担。并发管理是 bug 的重要引入来源。





node.js 有一个独特的优势就是有几百万在浏览器写 JavaScript 的前端现在不需要再学习另一门语言，直接可以写服务端的代码。

在 node.js 中， 新的 ECMAScrip 可以直接使用。你不需要等所有的浏览器用户都更新他们的浏览器。可以通过控制 ndoe.js 的版本来控制ECMAScript。你还可以通过运行特定的标志来尝试特殊的特性。



数量庞大的库





npm 这个简单结构帮助 node 的生态疯狂扩展。你现在使用的 开源包以及操作的 1百万个。



最常见的 hello world 示例是 web 服务：



const http = require('http')

const hostname = '127.0.0.1'
const port = process.env.PORT

const server = http.createServer((req, res) => {
  res.statusCode = 200
  res.setHeader('Content-Type', 'text/plain')
  res.end('Hello World!\n')
})

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`)
})

第一行代码宝行了 node.js 的 http 模块



node.js 有出色的标准库，包含了一流的网络支持。



http模块的 createServer 方法创建一个新的 http 服务并返回





这个服务会监听特殊的端口和服务名，当服务已经准备完毕，回调函数会被执行，并通知我们服务已经启动。

当接受到一个新的请求， request 事件被调用，会提供两个对象，一个 request (一个 [`http.IncomingMessage`](https://nodejs.org/api/http.html#http_class_http_incomingmessage) 对象)和一个 response (一个 [`http.ServerResponse`](https://nodejs.org/api/http.html#http_class_http_serverresponse) 对象).



这个两个对象是处理 http 调用必要的。



第一个 request 提供了请求的详情参数，在这个例子中没有使用到，但是你可以接受请求的 headers 或请求的参数。



第二个是返回数据给调用者的。



在这例子中：



res.statusCode = 200



我们设置 statusCode 为 200，来表明这是一成功的请求。



我们设置一个 context-Type header:

```javascript
res.setHeader('Content-Type', 'text/plain')
```





最后我们关闭这个 response ，然后添加一些内容在 end 方方法的参数上。



```javascript
res.end('Hello World\n')
```

node.js 的框架和工具



node.js 是一个低代码平台，为了让开发者更容易和愉快的进行开发，社区简历的上千个库在 node.js 里。



很多库经过时间的考验变得相当受欢迎，这里是比较全面的值得学习的礼拜



adonisJs一个全栈框架，高度关注开发人员的人机工程学，稳定性和信心。 Adonis是最快的Node.js Web框架之一。



Egg.js使用Node.js和Koa构建更好的企业框架和应用程序的框架。



Express：它提供了创建Web服务器的最简单但功能最强大的方法之一。其极简主义的方法不受限制，专注于服务器的核心功能，是其成功的关键。





Fastify Web框架高度专注于以最少的开销和强大的插件体系结构提供最佳的开发人员体验。 Fastify是最快的Node.js Web框架之一。

Gatsby 基于GraphQL的基于React的静态站点生成器，具有非常丰富的插件和启动器生态系统。



hapi 用于构建应用程序和服务的丰富框架，使开发人员能够专注于编写可重用的应用程序逻辑，而不必花费时间来构建基础结构。

koa

它是由Express背后的同一个团队构建的，旨在基于多年的知识，变得更小，更小。新项目的产生是出于创建不兼容的更改而又不破坏现有社区的需要。

loopback.io

使构建需要复杂集成的现代应用程序变得容易。

meteor

一个功能强大的全栈框架，采用同构方法为您提供支持，以JavaScript构建应用，在客户端和服务器上共享代码。曾经提供所有功能的现成工具，现在可以与前端库React，Vue和Angular集成。也可以用于创建移动应用。

micor

它提供了一个非常轻量级的服务器来创建异步HTTP微服务。

nestJS 基于TypeScript的渐进式Node.js框架，用于构建企业级高效，可靠和可扩展的服务器端应用程序。



next.js React框架可为您提供最佳的开发人员体验，包括生产所需的所有功能：静态和服务器混合渲染，TypeScript支持，智能捆绑，路由预取等。



Nx 使用NestJS，Express，React，Angular等进行全栈Monorepo开发的工具包！ Nx可帮助您将开发工作从一个团队构建一个应用程序扩展到多个团队在多个应用程序上进行协作！



Sapper 使用NestJS，Express，React，Angular等进行全栈Monorepo开发的工具包！ Nx可帮助您将开发工作从一个团队构建一个应用程序扩展到多个团队在多个应用程序上进行协作！



Socket.io 用于构建网络应用程序的实时通信引擎。



strapi

Strapi是一种灵活的开源Headless CMS，它使开发人员可以自由选择自己喜欢的工具和框架，同时还允许编辑者轻松管理和分发其内容。通过使管理面板和API可以通过插件系统进行扩展，Strapi使全球最大的公司可以加速内容交付，同时构建优美的数字体验。

