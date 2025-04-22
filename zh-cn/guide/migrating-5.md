---
layout: page
title: 迁移到Express 5
description: 一个将您的 Express.js 应用程序从版本 4 迁移到 5 的全面指南，详细说明了打破性的更改、废弃的方法和新的改进。
menu: guide
lang: 中
redirect_from: ""
---

# 移动到 Express 5

<h2 id="overview">概览</h2>

Express 5 与Express 4没有太大差异； 虽然它保持相同的基本API，但仍然有一些更改与以前版本不兼容。 因此，使用Express 4构建的应用程序可能无法运行，如果您更新它以使用Express 5。

要安装此版本，您需要有 Node.js 版本18或更高版本。 然后，在您的应用程序目录中执行以下命令：

```sh
npm install "express@5"
```

然后您可以运行您的自动化测试来查看什么失败，并根据下面列出的更新来修复问题。 处理测试失败后，运行您的应用以查看发生了哪些错误。 您会立即找到应用是否使用了不支持的任何方法或属性。

## Express 5 codemods

为了帮助您迁移您的快递服务器， 我们已经创建了一组代码集，它将帮助您自动更新代码到最新版本的Express。

运行以下命令来运行所有可用的代码表：

```sh
npx @expressjs/codemod upgrade
```

如果你想要运行一个特定的编解码器，你可以运行以下命令：

```sh
npx @expressjs/codemod name-of-the-codemod
```

您可以找到可用的编解码器 [here](https://github.com/expressjs/codemod?tab=readme-ov-file#available-codemods)。

<h2 id="changes">快递变化5</h2>

**删除方法和属性**

<ul class="doclist">
  <li><a href="#app.del">app.del()</a></li>
  <li><a href="#app.param">app.param(fn)</a></li>
  <li><a href="#plural">多化方法名称</a></li>
  <li><a href="#leading">以名字参数的顶端冒号到app.param(name, fn)</a></li>
  <li><a href="#req.param">req.param(name)</a></li>
  <li><a href="#res.json">res.json(obj, status)</a></li>
  <li><a href="#res.jsonp">res.jsonp(obj, status)</a></li>
  <li><a href="#magic-redirect">res.redirect('back') and res.location('back')</a></li>  
  <li><a href="#res.redirect">res.redirect(url, status)</a></li>
  <li><a href="#res.send.body">res.send(身体，状态)</a></li>
  <li><a href="#res.send.status">res.send(status)</a></li>
  <li><a href="#res.sendfile">res.sendfile()</a></li>
  <li><a href="#express.static.mime">表示.static.mime</a></li>
  <li><a href="#express:router-debug-logs">express:router debug logs</a></li>
</ul>

**变更**

<ul class="doclist">
  <li><a href="#path-syntax">路径路由匹配语法</a></li>
  <li><a href="#rejected-promises">Rejected promises handled from middleware and handlers</a></li>
  <li><a href="#express.urlencoded">express.urlencoded</a></li>
  <li><a href="#app.listen">app.listen</a></li>
  <li><a href="#app.router">app.router</a></li>
  <li><a href="#req.body">req.body</a></li>
  <li><a href="#req.host">req.host</a></li>
  <li><a href="#req.query">req.query</a></li>
  <li><a href="#res.clearCookie">res.clearcookie</a></li>
  <li><a href="#res.status">res.status</a></li>
  <li><a href="#res.vary">res.vide</a></li>
</ul>

**改进**

<ul class="doclist">
  <li><a href="#res.render">res.render()</a></li>
  <li><a href="#brotli-support">Brotli编码支持</a></li>
</ul>

### 移除方法和属性

如果您在应用中使用任何这些方法或属性，它将崩溃。 所以，您需要在更新到第5版后更改您的应用。

<h4 id="app.del">app.del()</h4>

Express 5 不再支持 `app.del()` 函数。 如果您使用此函数，将会出现错误。 要注册 HTTP DELETE 路由，请使用 `app.delete()` 函数。

最初使用 `del` 代替`del` ，因为`delete` 是JavaScript中的保留关键字。 然而，从ECMAScrip6开始，`delete`和其他保留关键词可以合法地用作财产名称。

{% capture codemod-deprecated-signatures %}
您可以用以下命令替换废弃的签名：

```plain-text
npx @expressjs/codemod v4-deprecated-signatures
```

{% endcapture %}

{% include admonitions/note.html content=codemod-废弃签名%}

```js
// v4
app.del('/user/:id', (req, res) => {
  res.send(`DELETE /user/${req.params.id}`)
})

// v5
app.delete('/user/:id', (req, res) => {
  res.send(`DELETE /user/${req.params.id}`)
})
```

<h4 id="app.param">app.param(fn)</h4>

`app.param(fn)`签名被用于修改`app.param(name, fn)`函数的行为。 自v4.11.0以来它已被废弃，Express 5完全不再支持它。

<h4 id="plural">多化方法名称</h4>

以下方法名称已复数。 在Express 4中，使用旧方法导致废弃警告。 Expression 5 根本不再支持他们：

`req.acceptsCharset()` 代之以`req.acceptsets()`。

`req.acceptsEncoding()` 代之以`req.acceptsEncodings()` 。

`req.acceptsLanguage()` 代之以`req.acceptsLanguages()` 。

{% capture codemod-pluralized-methods %}
您可以用以下命令替换废弃的签名：

```plain-text
npx @expressjs/codemod pluralized-methods
```

{% endcapture %}

{% include admonitions/note.html content=codemod-plened-methods %}

```js
// v4
app.all('/', (req, res) => {
  req.acceptsCharset('utf-8')
  req.acceptsEncoding('br')
  req.acceptsLanguage('en')

  // ...
})

// v5
app.all('/', (req, res) => {
  req.acceptsCharsets('utf-8')
  req.acceptsEncodings('br')
  req.acceptsLanguages('en')

  // ...
})
```

<h4 id="leading">顶部冒号 (:) 在 app.param(名称, fn)</h4>

"应用"名称中的前沿冒号字符 (:)。 aram(name, fn)\`函数是Express 3的残余函数。为了向后兼容，Express 4支持它，并且不建议通知。 Express 5 将静默忽略它，使用名称参数，而不会用冒号前缀。

如果您遵循 [app.param](/{{ page.lang }}/4x/api.html#app.param) 的 Express 4 文档进行开发，那么不会影响代码，因为文档中没有提及前置冒号。

<h4 id="req.param">req.param(名称)</h4>

这种潜在的混乱和危险的检索形式数据方法已被删除。 您现在需要在`req.params`, `req.body`, 或 `req.query`对象中具体寻找提交的参数名称。

{% capture codemod-req-param %}
您可以用以下命令替换废弃的签名：

```plain-text
npx @expressjs/codemod req-param
```

{% endcapture %}

{% include admonitions/note.html content=codemod-req-param %}

```js
// v4
app.post('/user', (req, res) => {
  const id = req.param('id')
  const body = req.param('body')
  const query = req.param('query')

  // ...
})

// v5
app.post('/user', (req, res) => {
  const id = req.params.id
  const body = req.body
  const query = req.query

  // ...
})
```

<h4 id="res.json">res.json(obj, status)</h4>

Express 5 不再支持签名 `res.json(obj, status)` 。 相反，设置状态然后将它链到`res.json()` 方法：`res.status(status).json(obj)` 。

{% include admonitions/note.html content=codemod-废弃签名%}

```js
// v4
app.post('/user', (req, res) => {
  res.json({ name: 'Ruben' }, 201)
})

// v5
app.post('/user', (req, res) => {
  res.status(201).json({ name: 'Ruben' })
})
```

<h4 id="res.jsonp">res.jsonp(obj, status)</h4>

Express 5 不再支持签名 `res.jsonp(obj, status)` 。 相反，设置状态然后将它链到`res.jsonp()` 方法：`res.status(status).jsonp(obj)` 。

{% include admonitions/note.html content=codemod-废弃签名%}

```js
// v4
app.post('/user', (req, res) => {
  res.jsonp({ name: 'Ruben' }, 201)
})

// v5
app.post('/user', (req, res) => {
  res.status(201).jsonp({ name: 'Ruben' })
})
```

<h4 id="res.redirect">重定向(url, status)</h4>

Express 5 不再支持特征符 `res.redirect(url, status)`。而是设置状态，然后将其链接到 `res.json()` 方法，如下所示：`res.status(status).json(obj)`。 相反，使用下列签名：`res.redirect(status, url)`。

{% include admonitions/note.html content=codemod-废弃签名%}

```js
// v4
app.get('/user', (req, res) => {
  res.redirect('/users', 301)
})

// v5
app.get('/user', (req, res) => {
  res.redirect(301, '/users')
})
```

<h4 id="magic-redirect">重定向('back') 和 res.location('back')</h4>

Express 5 不再支持`res.redirect()` 和 `res.location()` 方法中的魔法字符串`back`。 相反，使用 `req.get('Refererer') || '/'` 值重定向到上一页。 在Express 4中，res.`redirect('back')`和`res.location('back')`的方法被弃用。

{% capture codemod-magic-redirect %}
您可以用以下命令替换废弃的签名：

```plain-text
npx @expressjs/codemod magic-redirect
```

{% endcapture %}

{% include admonitions/note.html content=codemod-magic-redirect%}

```js
// v4
app.get('/user', (req, res) => {
  res.redirect('back')
})

// v5
app.get('/user', (req, res) => {
  res.redirect(req.get('Referrer') || '/')
})
```

<h4 id="res.send.body">发送(身体，状态)</h4>

Express 5 不再支持签名 `res.send(obj, status)` 。 相反，设置状态然后将其连接到 `res.send()` 方法：`res.status(status).send(obj)` 。

{% include admonitions/note.html content=codemod-废弃签名%}

```js
// v4
app.get('/user', (req, res) => {
  res.send({ name: 'Ruben' }, 200)
})

// v5
app.get('/user', (req, res) => {
  res.status(200).send({ name: 'Ruben' })
})
```

<h4 id="res.send.status">发送(状态)</h4>

Express 5 不再支持签名 `res.send(status)` 是一个数字。 相反，使用“restrictions”。 endStatus(status) `函数设置HTTP响应头状态代码并发送代码的文本版本：“找不到”， "Internal Server Error"，等等。
如果您需要使用 'res' 发送一个数字。 end()`函数，引用数字转换为字符串， 这样Express不会将其解释为试图使用不受支持的旧签名。

{% include admonitions/note.html content=codemod-废弃签名%}

```js
// v4
app.get('/user', (req, res) => {
  res.send(200)
})

// v5
app.get('/user', (req, res) => {
  res.sendStatus(200)
})
```

<h4 id="res.sendfile">发送文件 ()</h4>

`res.sendfile()` 函数已被快递中的迷彩版本`res.sendFile()` 替换。

{% include admonitions/note.html content=codemod-废弃签名%}

```js
// v4
app.get('/user', (req, res) => {
  res.sendfile('/path/to/file')
})

// v5
app.get('/user', (req, res) => {
  res.sendFile('/path/to/file')
})
```

<h4 id="express.static.mime">表示.static.mime</h4>

在Express 5中，`mime`不再是`static`字段的导出属性。
Use the [`mime-types` package](https://github.com/jshttp/mime-types) to work with MIME type values.

```js
// v4
express.static.mime.lookup('json')

// v5
const mime = require('mime-types')
mime.lookup('json')
```

<h4 id="express:router-debug-logs">express:router 调试日志</h4>

在Express 5中，路由器处理逻辑由依赖执行。 因此，在`express:`命名空间下，路由器的
调试日志不再可用。
在v4中，日志可在命名空间`aug:router`, `express:router:layer`,
和`express:router:route`下获取。 所有这些都包括在命名空间`express:*`中。
在 v5.1+中，日志可在命名空间`router`、`routter:layer`和`routter:route`下获取。
来自`router:layer` 和 `router:route` 的日志包含在命名空间`router:*` 中。
若要在v4中使用 "express:_" 实现相同的调试记录详情，请使用
"express:_", "router", 和 "router:\*"。

```sh
# v4
DEBUG=express:* node index.js

# v5
DEBUG=express:*,router,router:* node index.js
```

<h3>已更改</h3>

<h4 id="path-syntax">匹配语法的路径路径</h4>

匹配语法的路径路由是提供一个字符串作为`app.all()`, `app.use()`, `app.METHOD()`, `routter.all()`, `router.METHOD()`, 和`router.use()`API的第一个参数。 对路径字符串与传入请求匹配的方式作了以下更改：

- 通配符`*`必须有一个名称，匹配参数`:`，使用`/*splat`而不是`/*`

```js
// v4
app.get('/*', async (req, res) => {
  res.send('ok')
})

// v5
app.get('/*splat', async (req, res) => {
  res.send('ok')
})
```

{% capture note_wildcard %}
`*splat` 匹配没有根路径的任何路径。 如果你需要同时匹配根路径，你可以使用 "/{\*splat}" 来包装括号中的通配符。

```js
// v5
app.get('/{*splat}', async (req, res) => {
  res.send('ok')
})
```

{% endcapture %}
{% include admonitions/note.html content=note_wildcard %}

- 不再支持可选字符 `?` ，而是使用括号。

```js
// v4
app.get('/:file.:ext?', async (req, res) => {
  res.send('ok')
})

// v5
app.get('/:file{.:ext}', async (req, res) => {
  res.send('ok')
})
```

- 不支持正则表达式字符。 例如：

```js
app.get('/[discussion|page]/:slug', async (req, res) => {
  res.status(200).send('ok')
})
```

应该更改为:

```js
app.get(['/discussion/:slug', '/page/:slug'], async (req, res) => {
  res.status(200).send('ok')
})
```

- 为了避免升级过程中出现混乱，已经保留了一些字符(`()[]?+!`)，使用`\`来逃避它们。
- 参数名称现在支持有效的 JavaScript 标识符，或引用的 `:'this `。

<h4 id="rejected-promises">被拒绝的许诺来自中间件和处理程序</h4>

请求退回被拒绝承诺的中间件和处理程序现在通过转发被拒绝的值作为处理中间件的错误而处理。 这意味着使用“async”函数作为中间件和处理程序比以往任何时候都更容易。 当在一个 "async" 函数中出现错误或拒绝的允诺是"等待"在异步函数内"时, 这些错误将会传递到错误处理程序中，仿佛调用 `next(err)` 。

快速处理错误是如何在 [错误处理文档](/en/guide/error-handling.html) 中涵盖的。

<h4 id="express.urlencoded">urlencoded</h4>

`expres.urlencoded`方法默认将`extended`选项`false`变得无效。

<h4 id="app.listen">监听应用程序...</h4>

在Express 5中，当服务器接收到错误事件时，`app.listen` 方法会调用用户提供的回调函数(如果提供的话)。 在Express4中，这种错误将被扔掉。 此更改将错误处理责任移至Express 5中的回调函数。 如果出现错误，它将会传递给回调作为参数。
例如：

```js
const server = app.listen(8080, '0.0.0.0', (error) => {
  if (error) {
    throw error // e.g. EADDRINUSE
  }
  console.log(`Listening on ${JSON.stringify(server.address())}`)
})
```

<h4 id="app.router">路由器</h4>

在 Express 4 中移除的 `app.router` 对象已经在Express 5 中产生了一个堆栈。 在新版本中，这个对象只是对基础快递路由器的一个引用。 与Express 3不同的是，应用程序必须明确加载它。

<h4 id="req.body">正文。</h4> 

`req.body`返回未定义的物体，当该物体未被解析时。 在Express 4中，默认情况下返回 `{}` 。

<h4 id="req.host">主机</h4>

在Express 4中，如果存在`req.host`函数，它会不正确地删除端口号。 Express 5中保留端口号。

<h4 id="req.query">查询</h4>

`req.query`属性不再是一个可写的属性，而是一个getter。 默认查询解析器已从“extended”改为“simple”。

<h4 id="res.clearCookie">clearcookie</h4>

`res.clearcookie` 方法忽略了用户提供的 `maxAge` 和 `expires` 两个选项。

<h4 id="res.status">状态</h4>

`res.status` 方法只接受在 `100` 到 `999`范围内的整数，并且跟随节点定义的行为。 s , 并且返回状态代码不是整数时的错误。

<h4 id="res.query">更改</h4>

`res.vary` 在缺少`field`参数时出现错误。 在Express 4中，如果省略了这个论点，它会在控制台上发出警告

### 改进

<h4 id="res.render">render()</h4>

这个方法现在强制执行所有视图引擎的异步行为。 避免视图引擎引起的故障，这些引擎具有同步实现并违反了建议的接口。

<h4 id="brotli-support">Brotli编码支持</h4>

Express 5 支持 Brotli 编码，用于从客户端收到支持它的请求。
