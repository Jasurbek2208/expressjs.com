---
layout: page
title: 迁移到Express 4
description: 一个将您的 Express.js 应用程序从版本 3 迁移到 4 的指南，涵盖中间器的更改、路由以及如何有效更新您的代码库.
menu: guide
lang: 中
redirect_from: ""
---

# 移动到快递4

<h2 id="overview">概览</h2>

Express 4 是对Express 3 的一次突破。 这意味着，如果您在其依赖关系中更新快递版本，那么现有的快递3应用将无法工作。

该条规定：

<ul class="doclist">
  <li><a href="#changes">Express 4</a></li>
  <li><a href="#example-migration">一个将 Express 3 应用程序迁移到 Express 4 的示例</a></li>
  <li><a href="#app-gen">升级到 Express 4 应用生成器</a></li>
</ul>

<h2 id="changes">快递变化4</h2>

Express 4有若干重大变化：

<ul class="doclist">
  <li><a href="#core-changes">Changes to Express core and middleware system.</a> 连接和内置中间件的依赖关系已被删除，所以您必须自己添加中间件本身。
  </li>
  <li><a href="#routing">对路由系统进行了更改。</a></li>
  <li><a href="#other-changes">其他各种更改。</a></li>
</ul>

另见：

- [新功能在 4.x.](https://github.com/expressjs/express/wiki/New-features-in-4.x)
- [从 3.x 迁移到 4.x.](https://github.com/expressjs/express/wiki/Migrating-from-3.x-to-4.x)

<h3 id="core-changes">
对 Express 核心和中间件系统的更改。
</h3>

Express 4 不再依赖连接，除“express.static”函数外，将所有内置的
中间件从其核心删除。 这意味着
Express现在是一个独立的路由和中间件网络框架。 和
快递版本和版本不受中间软件更新的影响。

没有内置的中间件，您必须明确添加运行您的应用程序所需的所有
中间件。 只需遵循这些步骤：

1. 安装模块：`npm install --save <module-name>`
2. 在您的应用中，需要模块：`require('module-name')`
3. 根据文档使用模块：`app.use( ... )`

下表列出Express 3 中间件及其对应的 Express 4。

<table class="doctable" border="1">
<tbody><tr><th>Express 3</th><th>Express 4</th></tr>
<tr><td><code>表示。bodyParser</code></td>
<td><a href="https://github.com/expressjs/body-parser">正文解析器</a> +
<a href="https://github.com/expressjs/multer">multer</a></td></tr>
<tr><td><code>expres.com按</code></td>
<td><a href="https://github.com/expressjs/compression">压缩</a></td></tr>
<tr><td><code>express.cookieSession</code></td>
<td><a href="https://github.com/expressjs/cookie-session">cookie-session</a></td></tr>
<tr><td><code>express.cookieParser</code></td>
<td><a href="https://github.com/expressjs/cookie-parser">cookie解析器</a></td></tr>
<tr><td><code>表示。Logger</code></td>
<td><a href="https://github.com/expressjs/morgan">morgan</a></td></tr>
<tr><td><code>express.session</code></td>
<td><a href="https://github.com/expressjs/session">表示会话</a></td></tr>
<tr><td><code>express.favicon</code></td>
<td><a href="https://github.com/expressjs/serve-favicon">serve-favicon</a></td></tr>
<tr><td><code>表示响应时间</code></td>
<td><a href="https://github.com/expressjs/response-time">响应时间</a></td></tr>
<tr><td><code>表示错误处理器</code></td>
<td><a href="https://github.com/expressjs/errorhandler">errorhandler</a></td></tr>
<tr><td><code>表示方法覆盖</code></td>
<td><a href="https://github.com/expressjs/method-override">方法覆盖</a></td></tr>
<tr><td><code>表示超时</code></td>
<td><a href="https://github.com/expressjs/timeout">连接超时</a></td></tr>
<tr><td><code>expres.vhost</code></td>
<td><a href="https://github.com/expressjs/vhost">vhost</a></td></tr>
<tr><td><code>express.csrf</code></td>
<td><a href="https://github.com/expressjs/csurf">csurf</a></td></tr>
<tr><td><code>表示目录</code></td>
<td><a href="https://github.com/expressjs/serve-index">服务器索引</a></td></tr>
<tr><td><code>表示静态</code></td>
<td><a href="https://github.com/expressjs/serve-static">服务器静态</a></td></tr>
</tbody></table>

这里是 Express 4 中间件的[完整列表](https://github.com/senchalabs/connect#middleware)。

在大多数情况下，您可以简单地将旧版本3的中间件替换为
其快递4对应件。 欲了解详情，请参阅
GitHub 中的模块文档。

<h4 id="app-use"><code>应用程序。使用</code> 接受参数</h4>

在版本 4 中，您可以使用一个变量参数来定义加载中间件函数的路径， 然后从路由处理器中读取参数的值。
例如：

```js
app.use('/book/:id', (req, res, next) => {
  console.log('ID:', req.params.id)
  next()
})
```

<h3 id="routing">
路由系统
</h3>

应用程序现在隐含加载路由中间件， 所以你不再需要
担心中间件加载到
路由器中间件的顺序。

您定义路线的方式没有改变，但路由系统有两个
新功能来帮助您组织路线：

{: .doclist }

- 一个新方法，`app.route()`，为路由路径创建链路处理程序。
- 一个新的类，`express.Router`，用于创建模块化可挂载路由处理器。

<h4 id="app-route"><code>app.route()</code> 方法</h4>

新的 `app.route()` 方法可以让您为路由路径创建链路处理器
。 由于路径是在一个位置指定的，因此创建模块化路线是有帮助的，减少冗余和搭配也是有帮助的。 For more
information about routes, see [`Router()` documentation](/{{ page.lang }}/4x/api.html#router).

这是使用 `app.route()` 函数定义的链路处理器的示例。

```js
app.route('/book')
  .get((req, res) => {
    res.send('Get a random book')
  })
  .post((req, res) => {
    res.send('Add a book')
  })
  .put((req, res) => {
    res.send('Update the book')
  })
```

<h4 id="express-router"><code>express.Router</code> 类</h4>

帮助组织路线的另一个功能是一个新的类，
`express.Router`，你可以用它来创建模块挂载的
路由处理器。 一个 `Router` 实例是一个完整的中间件和
路由系统。为此原因，它通常被称为“微型应用程序”。

下面的示例创建一个路由器作为模块，在
中加载中间件： 定义了一些路线，并将其挂在主应用的路径上。

例如，在应用程序目录中，
创建一个名为“birds.js”的路由器文件，其内容如下：

```js
var express = require('express')
var router = express.Router()

// middleware specific to this router
router.use((req, res, next) => {
  console.log('Time: ', Date.now())
  next()
})
// define the home page route
router.get('/', (req, res) => {
  res.send('Birds home page')
})
// define the about route
router.get('/about', (req, res) => {
  res.send('About birds')
})

module.exports = router
```

然后，在应用程序中加载路由器模块：

```js
var birds = require('./birds')

// ...

app.use('/birds', birds)
```

该应用现在可以处理到 "/birds" 和
"/birds/about" 路径的请求， 并调用 "timeLog"
中间件，这是路径特有的。

<h3 id="other-changes">
其他更改
</h3>

下表列出了Express4中其他小但重要的变化：

<table class="doctable" border="1">
<tbody><tr>
<th>对象</th>
<th>描述</th>
</tr>
<tr>
<td>Node.js</td>
<td>Express 4 需要 Node.js 0.10.x 或更高版本，并且放弃了
Node.js 0.8.x的支持。</td>
</tr>
<tr>
<td markdown="1">
`http.createServer()`
</td>
<td markdown="1">
不再需要`http`模块，除非你需要直接使用 (socket.io/SPDY/HTTPS)。 可以使用
`app.listen()` 函数启动应用程序。
</td>
</tr>
<tr>
<td markdown="1">
`app.configure()`
</td>
<td markdown="1">
`app.configure()` 函数已被删除。  
已移除 `app.configure()` 函数。使用 `process.env.NODE_ENV` 或 `app.get('env')` 功能来检测环境并相应配置该应用程序。

</td>
</tr>
<tr>
<td markdown="1">
"json spaces"
</td>
<td markdown="1">
在 Express 4 中，缺省情况下，已禁用 `json spaces` 应用程序属性。
</td>
</tr>
<tr>
<td markdown="1">
`req.accepted()`
</td>
<td markdown="1">
使用`req.accepts()`, `req.acceptsEncodings()`,
`req.acceptsCharsets()`, 和 `req.acceptsLanguages()`.
</td>
</tr>
<tr>
<td markdown="1">
`res.location()`
</td>
<td markdown="1">
不再解析相对的 URL。。
</td>
</tr>
<tr>
<td markdown="1">
`req.params`
</td>
<td markdown="1">
是一个数组，现在是一个对象。
</td>
</tr>
<tr>
<td markdown="1">
`res.locals`
</td>
<td markdown="1">
是一个函数；现在是一个对象。。
</td>
</tr>
<tr>
<td markdown="1">
`res.headerSent`
</td>
<td markdown="1">
更改为 "res.headersSent"。
</td>
</tr>
<tr>
<td markdown="1">
`app.route`
</td>
<td markdown="1">
现在可用于“app.mountpath”。
</td>
</tr>
<tr>
<td markdown="1">
`res.on('header')`
</td>
<td markdown="1">
已删除。
</td>
</tr>
<tr>
<td markdown="1">
`res.charset`
</td>
<td markdown="1">
已删除。
</td>
</tr>
<tr>
<td markdown="1">
`res.setHeader('Set-Cookie', val)`
</td>
<td markdown="1">
功能现在仅限于设置基本的 cookie 值。 
功能现在已限制为设置基本 cookie 值。将 `res.cookie()` 用于增添的功能。

</td>
</tr>
</tbody></table>

<h2 id="example-migration">示例应用程序迁移</h2>

这是一个将Express 3 应用程序迁移到Express 4的例子。
感兴趣的文件是 `app.js` 和 `package.json` 。

<h3 id="">
版本 3 App
</h3>

<h4 id=""><code>app.js</code></h4>

考虑一个带有以下`app.js`文件的 Express v.3 应用程序：

```js
var express = require('express')
var routes = require('./routes')
var user = require('./routes/user')
var http = require('http')
var path = require('path')

var app = express()

// all environments
app.set('port', process.env.PORT || 3000)
app.set('views', path.join(__dirname, 'views'))
app.set('view engine', 'pug')
app.use(express.favicon())
app.use(express.logger('dev'))
app.use(express.methodOverride())
app.use(express.session({ secret: 'your secret here' }))
app.use(express.bodyParser())
app.use(app.router)
app.use(express.static(path.join(__dirname, 'public')))

// development only
if (app.get('env') === 'development') {
  app.use(express.errorHandler())
}

app.get('/', routes.index)
app.get('/users', user.list)

http.createServer(app).listen(app.get('port'), () => {
  console.log('Express server listening on port ' + app.get('port'))
})
```

<h4 id=""><code>package.json</code></h4>

随附的 V3 `package.json` 文件可能具有类似于以下的内容：

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "3.12.0",
    "pug": "*"
  }
}
```

<h3 id="">
进程
</h3>

通过安装
Express 4 应用所需的中间件并更新Express 和 Pug 到他们各自的最新版本的
命令来开始迁移过程：

```bash
$ npm install serve-favicon morgan method-override express-session body-parser multer errorhandler express@latest pug@latest --save
```

对`app.js`作如下更改：

1. 内置的快递中间件函数`express.favicon`,
  `express.logger`, `express.methodOverride`,
  `express.session`, `express.bodyParser` 和
  `express.errorhandler` 不再可在
  `express` 中使用。 您必须手动安装他们的备选方案
  并在应用程序中加载它们。

2. 你不再需要加载 `app.router` 函数。
  它不是一个有效的 Express 4 应用对象，所以删除
  `app.use(app.router);` 代码。

3. 请确保中间件函数以正确的顺序加载-加载应用路径后的"错误处理器"。

<h3 id="">版本 4 应用程序</h3>

<h4 id=""><code>package.json</code></h4>

运行上述`npm`命令将更新`package.json`：

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "body-parser": "^1.5.2",
    "errorhandler": "^1.1.1",
    "express": "^4.8.0",
    "express-session": "^1.7.2",
    "pug": "^2.0.0",
    "method-override": "^2.1.2",
    "morgan": "^1.2.2",
    "multer": "^0.1.3",
    "serve-favicon": "^2.0.1"
  }
}
```

<h4 id=""><code>app.js</code></h4>

然后删除无效的代码，加载所需的中间件，并根据需要进行其他的
更改。 `app.js`文件看起来像这样：

```js
var http = require('http')
var express = require('express')
var routes = require('./routes')
var user = require('./routes/user')
var path = require('path')

var favicon = require('serve-favicon')
var logger = require('morgan')
var methodOverride = require('method-override')
var session = require('express-session')
var bodyParser = require('body-parser')
var multer = require('multer')
var errorHandler = require('errorhandler')

var app = express()

// all environments
app.set('port', process.env.PORT || 3000)
app.set('views', path.join(__dirname, 'views'))
app.set('view engine', 'pug')
app.use(favicon(path.join(__dirname, '/public/favicon.ico')))
app.use(logger('dev'))
app.use(methodOverride())
app.use(session({
  resave: true,
  saveUninitialized: true,
  secret: 'uwotm8'
}))
app.use(bodyParser.json())
app.use(bodyParser.urlencoded({ extended: true }))
app.use(multer())
app.use(express.static(path.join(__dirname, 'public')))

app.get('/', routes.index)
app.get('/users', user.list)

// error handling middleware should be loaded after the loading the routes
if (app.get('env') === 'development') {
  app.use(errorHandler())
}

var server = http.createServer(app)
server.listen(app.get('port'), () => {
  console.log('Express server listening on port ' + app.get('port'))
})
```

<div class="doc-box doc-info" markdown="1">
除非您需要直接使用 `http` 模块(套接字)。 o/SPDY/HTTPS，加载它是不需要的，应用程序可以简单地以这种方式启动：

```js
app.listen(app.get('port'), () => {
  console.log('Express server listening on port ' + app.get('port'))
})
```

</div>

<h3 id="">运行应用程序</h3>

迁移过程已完成，应用程序现在是一个
Express 4 应用。 要确认，使用以下命令启动应用程序：

```bash
$ node .
```

加载 [http://localhost:3000](http://localhost:3000)
并查看由Express 4渲染的主页。

<h2 id="app-gen">升级到 Express 4 应用生成器</h2>

生成快递应用的命令行工具仍然是
`expres` ，但是要升级到新版本， 您必须卸载
Express 3 应用生成器，然后安装新的
\`express-generator'。

<h3 id="">正在安装 </h3>

如果您已经在系统上安装了 Express 3 应用生成器，
您必须卸载它：

```bash
$ npm uninstall -g express
```

根据如何配置您的文件和目录权限，
您可能需要用 'sudo' 运行此命令。

现在安装新的生成器：

```bash
$ npm install -g express-generator
```

根据如何配置您的文件和目录权限，
您可能需要用 'sudo' 运行此命令。

现在你系统上的 `express` 命令已更新到
Express 4 生成器。

<h3 id="">更改应用生成器 </h3>

命令选项和使用基本保持不变，但以下除外：

{: .doclist }

- 已删除 `--sessions` 选项。
- 已删除 `--jshtml` 选项。
- 添加 `--hogan` 选项以支持 [Hogan.js](http://twitter.github.io/hogan.js/)。

<h3 id="">示例</h3>

执行以下命令来创建一个Express 4应用：

```bash
$ express app4
```

如果你看看`app4/app.js`文件的内容，你会注意到
所有中间件函数(除了`express'以外)。
所需的tatic`)应用程序被加载为独立模块， 和“路由器”中间件
不再在应用程序中被明确加载。

您还会注意到 `app.js`文件现在是一个节点。 s 模块，与旧的生成器生成的独立应用不同。

安装依赖后，使用以下命令启动应用程序：

```bash
$ npm start
```

如果你看到`软件包中的`npm start`脚本。 son`文件,
你会注意到启动应用程序的实际命令是
"节点。 Express 3中的`节点app.js`
bin/www\`。

因为Express 4生成器
生成的 `app.js` 文件现在是一个节点。 s 模块，它不能作为应用
(除非您修改代码)。 模块必须在 Node.js 文件
中加载，并通过 Node.js 文件开始。 Node.js文件是`.bin/www`
。

对于创建 Express 应用程序或启动此应用程序，`bin` 目录或无扩展名的 `www` 文件都不是必需的。它们只是生成器提出的建议，可随意根据自己的需求进行修改。 他们是
只是生成器提出的建议，所以可以随时修改它们以满足您的
需求。

如果不想使用 `www` 目录，而是保持“Express 3 风格”，请删除 `app.js` 文件末尾的 `module.exports = app;` 行，然后将以下代码粘贴在到该位置：

```js
app.set('port', process.env.PORT || 3000)

var server = app.listen(app.get('port'), () => {
  debug('Express server listening on port ' + server.address().port)
})
```

使用以下代码确保你在`app.js`文件顶部加载`debug`模块：

```js
var debug = require('debug')('app4')
```

接着，将`"start"：`package.json`文件中的"node ./bin/www"改为`"start"：\`node app.js"。

You have now moved the functionality of `./bin/www` back to
`app.js`. This change is not recommended, but the exercise helps you
to understand how the `./bin/www` file works, and why the `app.js` file
no longer starts on its own.
