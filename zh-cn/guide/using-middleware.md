---
layout: page
title: 使用快递中间件
description: 学习如何在 Express.js 应用程序中使用中间件，包括应用程序级别和路由级别的中间件、 错误处理、 以及整合第三方中间件。
menu: guide
lang: 中
redirect_from: ""
---

# 使用中间件

快递是一个路由和中间件网络框架，其自身功能最小：快递应用程序基本上是一系列中间件函数调用。

_中间件_函数能够访问[请求对象](/{{ page.lang }}/4x/api.html#req) (`req`)、[响应对象](/{{ page.lang }}/4x/api.html#res) (`res`) 以及应用程序的请求/响应循环中的下一个中间件函数。下一个中间件函数通常由名为 `next` 的变量来表示。 下一个中间件函数通常由一个名为`下一件`的变量表示。

中间件函数可以执行以下任务：

- 执行任何代码。
- 更改请求和响应对象。
- 结束请求-响应周期。
- 在堆栈中调用下一个中间件功能。

如果当前的中间件函数没有结束请求-响应周期，它必须调用 `next ()` 方法才能将控制传递到下一个中间件函数。 否则，请求将被搁置。

快递应用程序可以使用以下类型的中间体：

- [应用程序的中间层](#middleware.application)
- [路由中层](#middleware.router)
- [错误处理中间件](#middleware.error-handling)
- [内置中间层](#middleware.built-in)
- [第三方中间层](#middleware.third-party)

您可以加载应用程序级别和路由级别的中间件与可选挂载路径。
您还可以加载一系列中间件功能，在挂载点创建一个中间件系统。

<h2 id='middleware.application'>应用程序的中间件</h2>

使用 `app.use()` 和 `app.METHOD()` 函数将应用层中间件绑定到[应用程序对象](/{{ page.lang }}/4x/api.html#app)的实例，其中 `METHOD` 是中间件函数处理的请求的小写 HTTP 方法（例如 GET、PUT 或 POST）。

此示例显示无挂载路径的中间件函数。 每次应用程序收到请求时都执行该函数。

```js
const express = require('express')
const app = express()

app.use((req, res, next) => {
  console.log('Time:', Date.now())
  next()
})
```

此示例显示挂载在"/user/:id"路径上的中间件函数。 在`/user/:id`路径上执行任何类型的
HTTP 请求。

```js
app.use('/user/:id', (req, res, next) => {
  console.log('Request Type:', req.method)
  next()
})
```

此示例显示路由及其处理器功能(中间件系统)。 函数处理GET 请求到 "/user/:id" 路径。

```js
app.get('/user/:id', (req, res, next) => {
  res.send('USER')
})
```

这是一个在挂载点加载一系列中间件函数的示例，并带有挂载路径。
它展示了一个中间件子堆栈，它将任何类型的 HTTP 请求信息打印到 "/user/:id" 路径。

```js
app.use('/user/:id', (req, res, next) => {
  console.log('Request URL:', req.originalUrl)
  next()
}, (req, res, next) => {
  console.log('Request Type:', req.method)
  next()
})
```

路由处理程序使您能够为路径定义多个路由。 下面的示例定义了两个路径的 GET 请求到 `/user/:id` 路径。 第二条路线不会造成任何问题，但它永远不会被调用，因为第一条路线结束了请求-响应周期。

此示例显示了一个中间件子堆栈，它可以处理 GET 请求到 "/user/:id" 路径。

```js
app.get('/user/:id', (req, res, next) => {
  console.log('ID:', req.params.id)
  next()
}, (req, res, next) => {
  res.send('User Info')
})

// handler for the /user/:id path, which prints the user ID
app.get('/user/:id', (req, res, next) => {
  res.send(req.params.id)
})
```

若要从路由器中间件堆栈中跳过其余的中间件功能，请调用 `nett('route)` 以将控制权传递到下一条路由。

{% include admonitions/note.html content="`next('route)` 只能在使用`app.METHOD()` 或 `router.METHOD()`函数加载的中间件函数中工作。" %}

此示例显示了一个中间件子堆栈，它可以处理 GET 请求到 "/user/:id" 路径。

```js
app.get('/user/:id', (req, res, next) => {
  // if the user ID is 0, skip to the next route
  if (req.params.id === '0') next('route')
  // otherwise pass the control to the next middleware function in this stack
  else next()
}, (req, res, next) => {
  // send a regular response
  res.send('regular')
})

// handler for the /user/:id path, which sends a special response
app.get('/user/:id', (req, res, next) => {
  res.send('special')
})
```

中间件也可以在数组中声明可重新使用。

此示例显示一个包含一个中间件子堆栈的数组，这个数组将处理 GET 请求到 `/user/:id` 路径

```js
function logOriginalUrl (req, res, next) {
  console.log('Request URL:', req.originalUrl)
  next()
}

function logMethod (req, res, next) {
  console.log('Request Type:', req.method)
  next()
}

const logStuff = [logOriginalUrl, logMethod]
app.get('/user/:id', logStuff, (req, res, next) => {
  res.send('User Info')
})
```

<h2 id='middleware.router'>路由中间件</h2>

路由中间件的工作方式与应用程序中间件的工作方式相同，只是它与`express.Router()`的实例联系在一起。

```js
const router = express.Router()
```

使用 `router.use()` 和 `router.METHOD()` 两个函数加载路由级中间件.

下面的示例代码通过路由中间程序复制上面显示的中件系统：

```js
const express = require('express')
const app = express()
const router = express.Router()

// a middleware function with no mount path. This code is executed for every request to the router
router.use((req, res, next) => {
  console.log('Time:', Date.now())
  next()
})

// a middleware sub-stack shows request info for any type of HTTP request to the /user/:id path
router.use('/user/:id', (req, res, next) => {
  console.log('Request URL:', req.originalUrl)
  next()
}, (req, res, next) => {
  console.log('Request Type:', req.method)
  next()
})

// a middleware sub-stack that handles GET requests to the /user/:id path
router.get('/user/:id', (req, res, next) => {
  // if the user ID is 0, skip to the next router
  if (req.params.id === '0') next('route')
  // otherwise pass control to the next middleware function in this stack
  else next()
}, (req, res, next) => {
  // render a regular page
  res.render('regular')
})

// handler for the /user/:id path, which renders a special page
router.get('/user/:id', (req, res, next) => {
  console.log(req.params.id)
  res.render('special')
})

// mount the router on the app
app.use('/', router)
```

若要跳过路由器剩余的中间件功能，请调用 `next ('routter)`
将控制传回路由器实例。

此示例显示了一个中间件子堆栈，它可以处理 GET 请求到 "/user/:id" 路径。

```js
const express = require('express')
const app = express()
const router = express.Router()

// predicate the router with a check and bail out when needed
router.use((req, res, next) => {
  if (!req.headers['x-auth']) return next('router')
  next()
})

router.get('/user/:id', (req, res) => {
  res.send('hello, user!')
})

// use the router and 401 anything falling through
app.use('/admin', router, (req, res) => {
  res.sendStatus(401)
})
```

<h2 id='middleware.error-handling'>错误处理中间件</h2>

<div class="doc-box doc-notice" markdown="1">
错误处理中间件总是需要 _four_参数. 您必须提供四个参数来识别它是错误的处理中间件函数。 即使您不需要使用 "下一" 对象，您也必须指定它来维护签名。 否则，“下一个”对象将被解释为普通中间件，并且将无法处理错误。
</div>

定义错误以与其他中间件函数相同的方式处理中间件函数； 除非有四个参数而不是三个参数，特别是签名`(err, req, res, next)`：

```js
app.use((err, req, res, next) => {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```

有关错误处理中间件的详细信息，请参阅：[错误处理](/{{ page.lang }}/guide/error-handling.html)。

<h2 id='middleware.built-in'>内置中间件</h2>

从版本4.x开始，快递不再依赖 [Connect](https://github.com/senchalabs/connect)。 以前包含在快递中的中间件
功能现在是单独的模块中；查看[中件函数列表](https://github.com/senchalabs/connect#middleware)。

快递具有以下内置的中间件功能：

- [express.static](/en/4x/api.html#express.static) 用于诸如HTML文件、图像等静态资产。
- [express.json](/en/4x/api.html#express.json) 使用 JSON 有效载荷解析收到的请求。 **注意：可用快递4.16.0+**
- [express.urlencoded](/en/4x/api.html#express.urlencoded) 解析传入请求与 URL 编码的有效载荷。  **注意：可用快递4.16.0+**

<h2 id='middleware.third-party'>第三方中间件</h2>

使用第三方中间件添加功能到快递应用程序。

安装Node.js模块，然后在应用程序级别或路由器级别加载它。

下面的示例说明如何安装和加载 cookie解析中间件函数 cookie-parser。

```bash
$ npm install cookie-parser
```

```js
const express = require('express')
const app = express()
const cookieParser = require('cookie-parser')

// load the cookie-parsing middleware
app.use(cookieParser())
```

有关 Express 常用的第三方中间件函数的部分列表，请参阅：[第三方中间件](../resources/middleware.html)。
