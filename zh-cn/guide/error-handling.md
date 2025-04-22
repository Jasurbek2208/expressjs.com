---
layout: page
title: 快速处理错误
description: 了解Express.js 如何处理同步和异步代码中的错误，并学会执行自定义错误，处理您应用程序的中间件时出错。
menu: guide
lang: 中
redirect_from: ""
---

# 错误处理

_Error Handling_ 指的是快递如何捕获和处理错误，
同时同步和异步发生。 快递带有默认错误
处理程序，所以您不需要写自己就开始了。

## 抓取错误

重要的是要确保快递能够发现
运行路由处理程序和中间行程时出现的所有错误。

Errors that occur in synchronous code inside route handlers and middleware
require no extra work. If synchronous code throws an error, then Express will
catch and process it. 例如：

```js
app.get('/', (req, res) => {
  throw new Error('BROKEN') // Express will catch this on its own.
})
```

For errors returned from asynchronous functions invoked by route handlers
and middleware, you must pass them to the `next()` function, where Express will
catch and process them.  例如：

```js
app.get('/', (req, res, next) => {
  fs.readFile('/file-does-not-exist', (err, data) => {
    if (err) {
      next(err) // Pass errors to Express.
    } else {
      res.send(data)
    }
  })
})
```

从Express 5开始，返回Promise
的路由处理程序和中间件将在他们拒绝或抛出错误时自动调用 `next (value)` 。
例如：

```js
app.get('/user/:id', async (req, res, next) => {
  const user = await getUserById(req.params.id)
  res.send(user)
})
```

如果`getUserById`出现错误或拒绝错误，`next`将被调用
或被拒绝的值。 如果没有提供被拒绝的值, "下一"
将被调用一个默认的错误对象, 由快递路由器提供。

如果您将任何东西传递到 `next ()` 函数(字符串`'route`)，，
表示认为当前请求是一个错误，将跳过
仍然没有错误地处理路由和中间件函数。

如果一个序列中的回调没有提供数据，只有错误，您可以简化
以下代码：

```js
app.get('/', [
  function (req, res, next) {
    fs.writeFile('/inaccessible-path', 'data', next)
  },
  function (req, res) {
    res.send('OK')
  }
])
```

在上面的示例中，`fs.writeFile`,
被调用或没有错误的回调提供了`next `。 如果没有错误，执行第二个
处理程序，否则快递捕获并处理错误。

您必须在路由处理程序或
的异步代码中找到错误，并将它们传递给快递处理。 例如：

```js
app.get('/', (req, res, next) => {
  setTimeout(() => {
    try {
      throw new Error('BROKEN')
    } catch (err) {
      next(err)
    }
  }, 100)
})
```

上面的示例使用 "试...catch" 块来抓取
异步代码中的错误并传递到快递。 如果删除 "试...catch"
块，快递将不会抓到错误，因为它不是同步的
处理代码的一部分。

使用许诺来避免"试...catch"块的间接费用，或使用返回许诺的函数
时使用。  例如：

```js
app.get('/', (req, res, next) => {
  Promise.resolve().then(() => {
    throw new Error('BROKEN')
  }).catch(next) // Errors will be passed to Express.
})
```

因为许诺会自动产生同步错误和被拒绝的许诺，
你可以简单地提供 "下一" 作为最终捕获处理器和快递将会发现错误，
因为捕获处理程序被指定为第一个参数。

您还可以使用一个处理程序链来依赖同步错误
捕获，将异步代码减少到微不足道的程度。 例如：

```js
app.get('/', [
  function (req, res, next) {
    fs.readFile('/maybe-valid-file', 'utf-8', (err, data) => {
      res.locals.data = data
      next(err)
    })
  },
  function (req, res) {
    res.locals.data = res.locals.data.split(',')[1]
    res.send(res.locals.data)
  }
])
```

上面的示例在 "readFile"
调用中有一些微不足道的语句。 如果`readFile`导致错误，则将错误传递给Express， 否则您的
会很快返回到一个同步错误的世界，在链中的下一个处理程序的
。 然后，上面的例子试图处理数据。 如果失败，那么
同步错误处理程序将会捕获它。 如果你在
中完成了这个处理 `readFile` 回调，那么应用程序可能会退出，快递错误的
处理程序将不会运行。

无论您使用何种方法。如果您想要调用快递错误处理程序和
应用程序来生存， 您必须确保快递接收错误。

## 默认错误处理程序

快递带有一个内置的错误处理器来处理应用程序中可能遇到的任何错误。 这个默认错误处理中间件功能是在中间件功能堆栈的末尾添加的。

如果你将一个错误传递给`next()`并且你没有在一个自定义错误
处理器中处理它， 它将由内置的错误处理器处理； 错误将写入带有堆栈跟踪的客户端为
堆栈跟踪在生产环境中不包含
。

<div class="doc-box doc-info" markdown="1">
将环境变量`NODE_ENV` 设置为`production`, 以便在生产模式下运行应用。。
</div>

当一个错误被写入时，以下信息被添加到
响应中：

- `res.statusCode` 是从`err.status` (或`err.statusCode`)设置的。 如果
  此值不在 4xx 或 5xx 范围内，它将被设置为 500。
- `res.statusMessage` 是根据状态代码设置的。
- 在生成
  环境中，本机构将是状态代码消息的 HTML ，否则将是 \`err.stack'。
- 在 `err.headers` 对象中指定的任何标题。

如果您在开始写入
响应后调用 `next ()` 方法时出现错误 (例如) 如果您在串流到
客户端响应时遇到错误， 快速默认错误处理程序关闭
连接并使请求失败。

所以当您添加一个自定义错误处理器时，您必须将默认的快递错误处理器委托给
当headers
已经发送到客户端时：

```js
function errorHandler (err, req, res, next) {
  if (res.headersSent) {
    return next(err)
  }
  res.status(500)
  res.render('error', { error: err })
}
```

Note that the default error handler can get triggered if you call `next()` with an error
in your code more than once, even if custom error handling middleware is in place.

Other error handling middleware can be found at [Express middleware](/{{ page.lang }}/resources/middleware.html).

## 写错误处理程序

定义错误以与其他中间件函数相同的方式处理中间件函数；
除了错误处理函数外，有四个参数而不是三个参数：
`(err, req, res, next)` 。 例如：

```js
app.use((err, req, res, next) => {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```

您定义了在其它`app.use()`和路由调用之后处理中间件的错误；例如：

```js
const bodyParser = require('body-parser')
const methodOverride = require('method-override')

app.use(bodyParser.urlencoded({
  extended: true
}))
app.use(bodyParser.json())
app.use(methodOverride())
app.use((err, req, res, next) => {
  // logic
})
```

来自中间件函数的响应可以是任何格式的，例如HTML错误页、简单消息或JSON字符串。

为了组织(和更高层次的框架)，您可以定义
几个错误处理中间件功能，就像您使用
常规中间件功能。 For example, to define an error-handler
for requests made by using `XHR` and those without:

```js
const bodyParser = require('body-parser')
const methodOverride = require('method-override')

app.use(bodyParser.urlencoded({
  extended: true
}))
app.use(bodyParser.json())
app.use(methodOverride())
app.use(logErrors)
app.use(clientErrorHandler)
app.use(errorHandler)
```

在此示例中，通用的 `logErrors` 可能会写请求和
错误信息到 `stderr` ，例如：

```js
function logErrors (err, req, res, next) {
  console.error(err.stack)
  next(err)
}
```

在这个示例中，`clientErrorHandler`被定义为如下。在这种情况下，错误被明确传递到下一个错误。

请注意，当_not_调用错误处理函数中的“下一步”时，您有责任写入(和结束)。 否则，这些请求就会“存货”，不符合收集垃圾的条件。

```js
function clientErrorHandler (err, req, res, next) {
  if (req.xhr) {
    res.status(500).send({ error: 'Something failed!' })
  } else {
    next(err)
  }
}
```

实现以下“包罗一切”`errorHandler`函数（例如）：

```js
function errorHandler (err, req, res, next) {
  res.status(500)
  res.render('error', { error: err })
}
```

如果你有一个带有多个回调函数的路由处理器，你可以使用 `route` 参数跳到下一个路由处理器。 例如：

```js
app.get('/a_route_behind_paywall',
  (req, res, next) => {
    if (!req.user.hasPaid) {
      // continue handling this request
      next('route')
    } else {
      next()
    }
  }, (req, res, next) => {
    PaidContent.find((err, doc) => {
      if (err) return next(err)
      res.json(doc)
    })
  })
```

在此示例中，`getPaidContent`处理程序将被跳过，但`/a_route_back_paywall`中的任何剩余处理程序将继续执行。

<div class="doc-box doc-info" markdown="1">
调用`next ()` 和 `next (err)` 表示当前处理程序是完整的，并处于何种状态。  `next (err)` 将跳过所有余下的处理器，但为处理上述错误而设置的处理器除外。
</div>
