精通 node.js 的文件系统

node 自身提供了几个最小内核，当有些语言内置了完整的 POSIX  API，node 尝试只提供全部功能的最核心api,其他都通过同步，异步，流的 方式来进行引入。

这意味着 OS 上面一下方便的功能，必须要在 node 中重新创建。这个实用的教程就是教你基本的 node 文件系统怎么使用。

### 引入文件 files 文件系统

与文件系统交互的时候，最重要的是指向正确的文件，由于 npm 包也存储在必得库中，因此使用动态链接就要比使用硬编码的关系要好。这里有两种方式来确保包指向正确的文件。



*// 使用 `path.join` 替换 `+` 来使得windows 用户开心*



`const path = require('path')`

`*// 查找相对于调用的文件的位置，对于CLI应用程序很有用*`

`通过用户`

`path.join(process.cwd(), 'my-dynamic-file')`

`*// 或者*`

`path.resolve('my-dynamic-file')`

`*// 查找相对于该文件的文件，对于引用以下文件非常有用，随着包一起分发*`

`path.join(__dirname, 'my-package-file')`

### 读取文件

在 node 中，我们很可以很方便地使用流来读取文件。例子如下：

const path = require('path')

const fs = require('fs')

// 读取文件并传送到 console 里面

fs.createReadStream(path.join(__dirname, 'my-file')).pipe(process.stdout)

### 创建文件

创建文件也不复杂，这里是 shell 命名的 node 实现。

const path = require('path')

const fs = require('fs')

// cat ./my-file > ./my-other-file

fs.createReadStream(path.join(__dirname, 'my-file')).pipe(

  fs.createReadStream(path.join(__dirname, './my-other-file'))

)

### 移除文件

移除文件和目录通过是用用 shell 的 rm  -rf 命令。在 node 中，我们使用 rimaraf 包来实现。



const rimraf = require('rimraf')

const path = require('path')

rimraf(path.join(__dirname, './my-directory'), err => {

  if (err) throw err

})

### 创建目录

创建目录和移除文件的操作非常相似 ，使用的是 mkdirp 包



const mkdirp = require('mkdirp')

const path = require('path')



mkdirp(path.join(__dirname, 'foo/bar'), err => {

  if (err) throw err

})

### 查找文件

在当前目录下查找文件使用 readdirp



const readdirp = require('readdirp')

const json = require('JSONStream')

const path = require('path')

*// recursively print out all files in all subdirectories*

*// to the command line. The object stream must be*

*// stringified before being passed to `stdout`.*

readdirp({ root: path.join(__dirname) })

  .pipe(json.stringify())

  .pipe(process.stdout)

在当前目录的上一级查找文件使用 findup





const findup = require('findup')

const path = require('path')







findup(path.join(__dirname), 'package.json', (err, res) => {

  if (err) throw err

  console.log('dir is: ' + res)

})

### 关于代码鲁棒性的提醒

尽管我没有使用过，不过我知道一个非常好的东西 叫做 graceful-fs ，包含了重试，队列和其它优秀的内置特性。  如果你遇到文件系统问题的话，推荐使用。

### pipes 

当大量的文件一起传输的时候，处理错误就变得非常重要了，相比于在每个单独的流中做.on (‘error’ cb) 的处理，推荐使用 pump 来处理错误并关闭正确的流。

const pump = require('pump')

const fs = require('fs')

fs.createReadStream('./in.file').pipe(fs.createReadStream('./out.file'))



const rs = fs.createReadStream('./in.file')

const ws = fs.createReadStream('./out.file')



pump(rs, ws, err => {

  if (err) throw err

})