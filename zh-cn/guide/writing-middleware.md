---
layout: page
title: 写中间件用于快递应用
description: 学习如何为 Express.js 应用程序编写自定义中间件功能，包括加强请求和响应处理的实例和最佳做法。
menu: guide
lang: 中
redirect_from: ""
---

# 写中间件用于快递应用

<h2>概览</h2>

_中间件_函数能够访问[请求对象](/{{ page.lang }}/4x/api.html#req) (`req`)、[响应对象](/{{ page.lang }}/4x/api.html#res) (`res`) 以及应用程序的请求/响应循环中的下一个中间件函数。下一个中间件函数通常由名为 `next` 的变量来表示。 “下一个”函数是快速路由器中的一个函数，在调用时执行当前中间件之后的中间件.

中间件函数可以执行以下任务：

- 执行任何代码。
- 更改请求和响应对象。
- 结束请求-响应周期。
- 在堆栈中调用下一个中间件.

如果当前的中间件函数没有结束请求-响应周期，它必须调用 `next ()` 方法才能将控制传递到下一个中间件函数。 否则，请求将被搁置。

下图显示了中间件函数调用的元素：

<table id="mw-fig">
<tbody><tr><td id="mw-fig-imgcell">
<img src="/images/express-mw.png" alt="Elements of a middleware function call" id="mw-fig-img" />
</td>
<td class="mw-fig-callouts">
<div class="callout" id="callout1">适用中间件函数的 HTTP 方法。</div></tbody>

<div class="callout" id="callout2">适用中间件函数的路径 (路径) 。</div>

<div class="callout" id="callout3">中间件功能。</div>

<div class="callout" id="callout4">通过约定调用中间件功能，称为“下一步”。</div>

<div class="callout" id="callout5">HTTP <a href="/{{ page.lang }}/4x/api.html#res">对中间件函数的响应，名为 "res" 的参数为</a>。</div>

<div class="callout" id="callout6">HTTP <a href="/{{ page.lang }}/4x/api.html#req">通过约定向中间件函数请求</a> 参数，称为“req”。</div>
</td></tr>
</table>

从Express 5开始，返回承诺的中间件函数将在拒绝或抛出错误时调用 `next (value)'。 `next \`将被调用被拒绝的值或抛出的错误。

<h2>示例</h2>

这是一个简单的“Hello World”快递应用程序的例子。
这篇文章的其余部分将定义并添加三个中间件函数到应用程序：
一个名为 `myLogger` ，用于打印一个简单的日志消息， 一个叫做
的“requestTime”来显示HTTP请求的时间戳，一个叫做`validateCookies` 来验证传入的 cookie。

```js
const express = require('express')
const app = express()

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(3000)
```

<h3>中间件函数myLogger</h3>
这是一个叫做“myLogger”的中间件函数的简单例子。 此函数只是在请求通过应用程序时打印"LOGUED"。 中间件函数分配给一个变量，名为“myLogger”。

```js
const myLogger = function (req, res, next) {
  console.log('LOGGED')
  next()
}
```

<div class="doc-box doc-notice" markdown="1">
注意上面的呼叫到 `next ()` 。 调用此函数调用应用程序中的下一个中间件函数。
`next ()`函数不是Node.js或Express API的一部分，而是传递给中间件函数的第三个参数。 `next ()`函数可以命名，但根据惯例，它总是被命名为“下一步”。
为了避免混乱，总是使用本公约。
</div>

要加载中间件函数，请调用 `app.use()`，指定中间件函数。
例如，下面的代码会在路径(/)之前加载`myLogger`中间件函数。

```js
const express = require('express')
const app = express()

const myLogger = function (req, res, next) {
  console.log('LOGGED')
  next()
}

app.use(myLogger)

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(3000)
```

每次应用程序收到请求时，它都会将消息“LOGED”打印到终端。

中间件加载的顺序很重要：首先加载的中间件函数也会先执行。

如果在 root 路径后加载 `myLogger` ，请求就永远不会送达，应用程序也不打印"LOGED"， 因为根路径的路由处理程序终止请求-响应周期。

中间件函数 `myLogger` 只是打印一条消息， 然后通过调用 `next ()` 函数将请求传递到堆栈中的下一个中间件函数。

<h3>中间件函数请求时间</h3>

接下来，我们会创建一个叫做“requestTime”的中间件函数，并在请求对象中添加一个名为 `requestTime`
的属性。

```js
const requestTime = function (req, res, next) {
  req.requestTime = Date.now()
  next()
}
```

应用程序现在使用 `requestTime` 中间件功能。 另外，根路径路由的回调函数使用了中间件函数添加到`req`(请求对象)的属性。

```js
const express = require('express')
const app = express()

const requestTime = function (req, res, next) {
  req.requestTime = Date.now()
  next()
}

app.use(requestTime)

app.get('/', (req, res) => {
  let responseText = 'Hello World!<br>'
  responseText += `<small>Requested at: ${req.requestTime}</small>`
  res.send(responseText)
})

app.listen(3000)
```

当您向应用程序的根请求时，应用程序现在在浏览器中显示您请求的时间戳。

<h3>中间件函数验证 Cookie</h3>

最后，我们将创建一个验证传入的 cookie 的中间件功能，并在 cookie 无效时发送400个响应。

下面是验证外部异步服务的 cookie 的示例函数。

```js
async function cookieValidator (cookies) {
  try {
    await externallyValidateCookie(cookies.testCookie)
  } catch {
    throw new Error('Invalid cookies')
  }
}
```

Here, we use the [`cookie-parser`](/resources/middleware/cookie-parser.html) middleware to parse incoming cookies off the `req` object and pass them to our `cookieValidator` function. `validateCookies` 中间件返回一个承诺，在拒绝时会自动触发我们的错误处理器。

```js
const express = require('express')
const cookieParser = require('cookie-parser')
const cookieValidator = require('./cookieValidator')

const app = express()

async function validateCookies (req, res, next) {
  await cookieValidator(req.cookies)
  next()
}

app.use(cookieParser())

app.use(validateCookies)

// error handler
app.use((err, req, res, next) => {
  res.status(400).send(err.message)
})

app.listen(3000)
```

<div class="doc-box doc-notice" markdown="1">
请注意如何在 `reward cookieValidator(req.cookies)` 之后调用 `next ()` 方法。 这将确保如果`cookieValidator`解析，堆栈中的下一个中间件将被召唤。 如果将任何项传递到 `next()` 函数（除了字符串 `'route'`），那么 Express 会将当前请求视为处于错误状态，并跳过所有剩余的非错误处理路由和中间件函数。如果您希望以某种方式处理此错误，必须如下一节中所述创建一个错误处理路由。
</div>

因为您可以访问请求对象，响应对象、堆栈中的下一个中间件功能以及整个节点。 s API，具有中间件功能的可能性是无止境的。

有关 Express 中间件的更多信息，请参阅：[使用 Express 中间件](/{{ page.lang }}/guide/using-middleware.html)。

<h2>可配置的中间件</h2>

如果您需要您的中间件配置，导出一个接受选项对象或其他参数的函数， 然后返回基于输入参数的中间件实现。

文件：`my-middleware.js`

```js
module.exports = function (options) {
  return function (req, res, next) {
    // Implement the middleware function based on the options object
    next()
  }
}
```

中间件现在可以用如下所示。

```js
const mw = require('./my-middleware.js')

app.use(mw({ option1: '1', option2: '2' }))
```

请参阅 [cookie-session](https://github.com/expressjs/cookie-session) 和 [compression](https://github.com/expressjs/compression) 的可配置中间件示例。
