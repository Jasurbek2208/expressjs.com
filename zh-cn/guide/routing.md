---
layout: page
title: 快递路由
description: 学习如何在 Express.js 应用程序中定义和使用路由，包括路由方法、路由路径、参数以及使用 Router 进行模块路由。
menu: guide
lang: 中
redirect_from: ""
---

# 路由

_Routing_是指应用程序的端点 (URI) 是如何响应客户端请求的。
For an introduction to routing, see [Basic routing](/{{ page.lang }}/starter/basic-routing.html).

您使用快速`app`对象中与 HTTP 方法对应的方法定义路由；
例如“应用”。 et()`以处理GET 请求和`app.post\` 以处理POST 请求。 For a full list,
see [app.METHOD](/{{ page.lang }}/5x/api.html#app.METHOD). You can also use [app.all()](/{{ page.lang }}/5x/api.html#app.all) to handle all HTTP methods and [app.use()](/{{ page.lang }}/5x/api.html#app.use) to
specify middleware as the callback function (See [Using middleware](/{{ page.lang }}/guide/using-middleware.html) for details).

这些路由方法指定了一个调用函数(有时称为“处理器函数”)，当应用程序收到到指定路由(端点)和HTTP方法的请求时被调用。 换言之，与特定路由和方法相符的请求“听众”应用程序。 当它检测到匹配时，它会调用指定的回调函数。

事实上，路由方法可以有一个以上的回调函数作为参数。
具有多个回调函数， 它必须提供 `next ` 作为回调函数的参数，然后调用 `next ()` 作为函数正文中的一部分来关闭对下一个回调的控制
。

下面的代码是一个非常基本的路径的例子。

```js
const express = require('express')
const app = express()

// respond with "hello world" when a GET request is made to the homepage
app.get('/', (req, res) => {
  res.send('hello world')
})
```

<h2 id="route-methods">路由方法</h2>

路由方法来自一个 HTTP 方法并且附加到 一个 `Express ` 类的实例。

下面的代码是为应用程序根目录下的 `GET` 和 `POST` 方法定义的路由示例。

```js
// GET method route
app.get('/', (req, res) => {
  res.send('GET request to the homepage')
})

// POST method route
app.post('/', (req, res) => {
  res.send('POST request to the homepage')
})
```

表示支持与所有 HTTP 请求方法相对应的方法: `get`, `post`, 等等.
For a full list, see [app.METHOD](/{{ page.lang }}/5x/api.html#app.METHOD).

有一种特殊的路由方法，`app.all()`，用于在路径为 _all_ HTTP 请求方法加载中间件函数。 例如，无论使用`GET`，路由`"/secret`"的请求都会执行以下处理程序， `POST`, `PUT`, `DELETE`, 或[http module](https://nodejs.org/api/http.html#http_http_methods)支持的任何其他HTTP请求方法。

```js
app.all('/secret', (req, res, next) => {
  console.log('Accessing the secret section ...')
  next() // pass control to the next handler
})
```

<h2 id="route-paths">路由路径</h2>

路由路径与请求方法相结合，定义请求的端点。 路由路径可以是字符串、字符串模式或正则表达式。

{% capture caution-character %} In express 5, the characters `?`, `+`, `*`, `[]`, and `()` are handled differently than in version 4, please review the [migration guide](/{{ page.lang }}/guide/migrating-5.html#path-syntax) for more information.{% endcapture %}

{% include admonitions/caution.html content=caution-charge %}

{% capture note-dollar-character %}表示4时，像`$`这样的正则表达式字符需要用`\`来逃脱。
{% endcapture %}

{% include admonitions/caution.html content=note-$l-charge %}

{% capture note-path-to-regexp %}
Express 使用 [path-to-regexp](https://www.npmjs.com/package/path-to-regexp) 匹配路线路径；查看路径定义路径中所有可能性的路径至regexp 文档。 [快递游乐场路由](https://bjohansebas.github.io/playground-router/) 是测试基本快递路线的简易工具，尽管它不支持模式匹配。
{% endcapture %}

{% include admonitions/note.html content=note-path-to-regexp %}

{% include admonitions/warning.html content="查询字符串不是路由路径的一部分。" %}

### 基于字符串的路由路径

此路由路径将匹配请求到根路由，`/`。

```js
app.get('/', (req, res) => {
  res.send('root')
})
```

此路由路径将匹配请求到"/about"。

```js
app.get('/about', (req, res) => {
  res.send('about')
})
```

此路由路径将匹配请求到 `/random.text` 。

```js
app.get('/random.text', (req, res) => {
  res.send('random.text')
})
```

### 基于字符串模式的路由路径

{% capture caution-string-patterns %} Express 5中的字符串模式不再起作用。 Please refer to the [migration guide](/{{ page.lang }}/guide/migrating-5.html#path-syntax) for more information.{% endcapture %}

{% include admonitions/caution.html content=caution-string-pattern%}

此路由路径将匹配 `acd` 和 `abcd` 。

```js
app.get('/ab?cd', (req, res) => {
  res.send('ab?cd')
})
```

此路由路径将匹配 `abcd`, `abbcd`, `abbbbcd`等'。

```js
app.get('/ab+cd', (req, res) => {
  res.send('ab+cd')
})
```

此路由路径将匹配`abcd`、`abxcd`、`abRANDOMcd`、`ab123cd`等'。

```js
app.get('/ab*cd', (req, res) => {
  res.send('ab*cd')
})
```

此路由路径将匹配 `/abe` 和 `/abcde` 。

```js
app.get('/ab(cd)?e', (req, res) => {
  res.send('ab(cd)?e')
})
```

### 基于正则表达式的路由路径

此路由路径将匹配其中的"a"。

```js
app.get(/a/, (req, res) => {
  res.send('/a/')
})
```

此路由路径与 `butterfly` 和 `dragonfly` 匹配，但不是 `butterflyman` 、 `dragonflyman` 等。

```js
app.get(/.*fly$/, (req, res) => {
  res.send('/.*fly$/')
})
```

<h2 id="route-parameters">路由参数</h2>

路由参数被命名为URL部分，用于捕获它们在URL中位置指定的值。 捕获的值被填入`req.params`对象，路径中指定的路由参数的名称为其各自的密钥。

```
Route path: /users/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userId": "34", "bookId": "8989" }
```

要定义路由参数，只需在路由路径中指定路由参数如下所示。

```js
app.get('/users/:userId/books/:bookId', (req, res) => {
  res.send(req.params)
})
```

<div class="doc-box doc-notice" markdown="1">
The name of route parameters must be made up of "word characters" ([A-Za-z0-9_]).
</div>

既然连字（`-`）和点（`.`）是按字面解释的，它们可以与路线参数一起用于有用的目的。

```
Route path: /flights/:from-:to
Request URL: http://localhost:3000/flights/LAX-SFO
req.params: { "from": "LAX", "to": "SFO" }
```

```
Route path: /plantae/:genus.:species
Request URL: http://localhost:3000/plantae/Prunus.persica
req.params: { "genus": "Prunus", "species": "persica" }
```

{% capture warning-regexp %}
In express 5, Regexp characters are not supported in route paths, for more information please refer to the [migration guide](/{{ page.lang }}/guide/migrating-5.html#path-syntax).{% endcapture %}

{% include admonitions/caution.html content=warning-regexp %}

要更多地控制可用路由参数匹配的确切字符串，您可以在括号中附加正则表达式(`()`)：

```
Route path: /user/:userId(\d+)
Request URL: http://localhost:3000/user/42
req.params: {"userId": "42"}
```

{% include admontions/warning. tml content="因为正则表达式通常是文字字符串的一部分， 一定要用额外的 backlash 逃脱任何`\` 字符，例如`\\d+`.'。 %}

{% capture warning-version %}
in Express 4.x, <a href="https://github.com/expressjs/express/issues/2495">正则表达式中的`*`字符不是以通常的方式</a> 解释的。 作为一个工作区，使用 "{0,}" 代替"\*"。 这很可能在Express 5中固定下来。
{% endcapture %}

{% include admonitions/warning.html content=warning-version %}

<h2 id="route-handlers">路由处理程序</h2>

您可以提供多个回调函数，以类似于[中间件](/{{ page.lang }}/guide/using-middleware.html)的行为方式来处理请求。唯一例外是这些回调函数可能调用 `next('route')` 来绕过剩余的路由回调。您可以使用此机制对路由施加先决条件，在没有理由继续执行当前路由的情况下，可将控制权传递给后续路由。 唯一的例外是这些回调可能会使用 `next ('route)` 来绕过剩余的路由回调。 您可以使用此机制对路由设置预设条件， 然后将控制权传递给以后的路线，如果没有理由继续沿现有路线走的话。

路由处理程序的形式可以是函数、各种函数或两者的组合，如下面的例子所示。

单个回调函数可以处理路由。 例如：

```js
app.get('/example/a', (req, res) => {
  res.send('Hello from A!')
})
```

多个回调函数可以处理路由线路(请确保您指定 "下一" 对象)。 例如：

```js
app.get('/example/b', (req, res, next) => {
  console.log('the response will be sent by the next function ...')
  next()
}, (req, res) => {
  res.send('Hello from B!')
})
```

一系列回调函数可以处理路由。 例如：

```js
const cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

const cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

const cb2 = function (req, res) {
  res.send('Hello from C!')
}

app.get('/example/c', [cb0, cb1, cb2])
```

将独立的函数和函数组结合在一起可以处理一条路线。 例如：

```js
const cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

const cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

app.get('/example/d', [cb0, cb1], (req, res, next) => {
  console.log('the response will be sent by the next function ...')
  next()
}, (req, res) => {
  res.send('Hello from D!')
})
```

<h2 id="response-methods">响应方法</h2>

下面表格中的响应对象方法(“res”) 可以向客户端发送响应，并终止请求-响应周期。 如果这些方法没有从路由处理器中调用，客户端请求将被搁置。

| 方法                                                                                                                                                                                                                        | 描述                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| [res.download()](/{{ page.lang }}/4x/api.html#res.download)     | 提示要下载一个文件。              |
| [res.end()](/{{ page.lang }}/4x/api.html#res.end)               | 结束响应过程。                 |
| [res.json()](/{{ page.lang }}/4x/api.html#res.json)             | 发送 JSON 响应。             |
| [res.jsonp()](/{{ page.lang }}/5x/api.html#res.jsonp)           | 使用 JSON 支持发送JSON 响应。    |
| [res.redirect()](/{{ page.lang }}/4x/api.html#res.redirect)     | 重定向请求。                  |
| [res.render()](/{{ page.lang }}/4x/api.html#res.render)         | 渲染视图模板。                 |
| [res.send()](/{{ page.lang }}/4x/api.html#res.send)             | 发送不同类型的回复。              |
| [res.sendFile()](/{{ page.lang }}/4x/api.html#res.sendFile)     | 作为八进制流发送文件。             |
| [res.sendStatus()](/{{ page.lang }}/4x/api.html#res.sendStatus) | 设置响应状态代码并将其字符串表示作为响应正文。 |

<h2 id="app-route">app.route()</h2>

您可以使用 `app.route()` 方法为路由路径创建链路处理程序。
因为路径是在一个地点指定的，因此创建模块化路线是有帮助的，减少冗余和搭配也是有帮助的。 For more information about routes, see: [Router() documentation](/{{ page.lang }}/5x/api.html#router).

这是通过 `app.route()` 定义的链路处理器的示例。

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

<h2 id="express-router">路由器</h2>

使用 `expres.Router` 类来创建模块化的、可挂载的路由处理器。 有助于组织路由的另一个功能是新类 `express.Router`，可用于创建可安装的模块化路由处理程序。`Router` 实例是完整的中间件和路由系统；因此，常常将其称为“微型应用程序”。

下面的示例创建一个路由器作为模块，加载其中的中间件功能。 定义了一些路由，并在主应用程序的路径上挂载路由模块。

在应用程序目录中创建一个名为“birds.js”的路由器文件，包含以下内容：

```js
const express = require('express')
const router = express.Router()

// middleware that is specific to this router
const timeLog = (req, res, next) => {
  console.log('Time: ', Date.now())
  next()
}
router.use(timeLog)

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
const birds = require('./birds')

// ...

app.use('/birds', birds)
```

该应用现在可以处理`/birds`和`/birds/about`的请求， 并调用 `timeLog` 中间件函数，这些函数是路径特有的。

但如果父路由`/birds`有路径参数，它将无法从子路由中默认访问。 To make it accessible, you will need to pass the `mergeParams` option to the Router constructor [reference](/{{ page.lang }}/5x/api.html#app.use).

```js
const router = express.Router({ mergeParams: true })
```
