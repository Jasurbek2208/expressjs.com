---
layout: page
title: 快递常见问题
description: 查找常见问答关于 Express.js 的问题，包括应用程序结构、模型、认证、模板引擎、错误处理等主题。
menu: starter
lang: 中
redirect_from: ""
---

# 常见问题

## 我应该如何构建我的应用程序？

这个问题没有明确的答案。 这个问题没有固定答案。具体取决于您的应用程序以及参与团队的规模。为了实现尽可能的灵活性，Express 在结构方面不作任何假设。 为了尽可能保持
的灵活性，快递没有对结构作出任何假设。

路由和其他特定应用程序的逻辑可以在你想要的目录结构中尽可能多的文件
中。 查看下面的
示例以获得灵感：

- [航线列表](https://github.com/expressjs/express/blob/4.13.1/examples/route-separation/index.js#L32-L47)
- [路由图](https://github.com/expressjs/express/blob/4.13.1/examples/route-map/index.js#L52-L66)
- [MVC style controllers](https://github.com/expressjs/express/tree/master/examples/mvc)

此外，还有第三方扩展的Express，这简化了其中一些模式：

- [资源路径](https://github.com/expressjs/express-resource)

## 如何定义模型？

明示没有数据库概念。 此概念是
由第三方节点模块决定，允许您与几乎任何数据库接口
接口。

请参阅 [LoopBack](http://loopback.io) 的基于Express的以模型为中心的框架。

## 如何认证用户？

身份验证是另一个消息区域，快递不会进入
冒险。 您可以使用您想要的任何身份验证方案。
认证是 Express 没有涉足的另一严格领域。您可使用所希望的任何认证方案。
要了解简单的“用户名/密码”方案，请参阅[此示例](https://github.com/expressjs/express/tree/master/examples/auth)。

## Express 支持哪个模板引擎？

快递支持符合`(路径、局部、回调)`签名的任何模板引擎。
要正常化模板引擎接口和缓存，请参阅
[consolidate.js](https://github.com/visionmedia/consolidate.js)
支持项目。 未列出的模板引擎可能仍然支持快速签名。

For more information, see [Using template engines with Express](/{{page.lang}}/guide/using-template-engines.html).

## 如何处理404个响应？

在 Express, 404 个响应不是错误的结果，所以
错误处理程序中间件不会捕获它们。 This behavior is
because a 404 response simply indicates the absence of additional work to do;
in other words, Express has executed all middleware functions and routes,
and found that none of them responded. 您只需要
在堆栈的最底端添加一个中间件函数(低于所有其他函数)
来处理404个响应：

```js
app.use((req, res, next) => {
  res.status(404).send("Sorry can't find that!")
})
```

在 `expres.Router()`
的实例上动态地添加路线，所以路径不会被中间件功能所取代。

## 如何设置错误处理程序？

您定义了错误处理中间件的方式和其他中间件，
除非有四个参数而不是三个； 具体而言，签字`err, req, res, next)`：

```js
app.use((err, req, res, next) => {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```

有关更多信息，请参阅[错误处理](/{{ page.lang }}/guide/error-handling.html)。

## 如何渲染纯HTML？

你不是！ 无需使用 `res.render()` 函数渲染“HTML”。
如果你有特定的文件，请使用 `res.sendFile()` 函数。
如果您正在从目录服务许多资产，请使用 `expres.static()`
中间件功能。

## Express 需要什么版本的 Node.js ？

- [Express 4.x](/{{ page.lang }}/4x/api.html) requires Node.js 0.10 or higher.
- [Express 5.x](/{{ page.lang }}/5x/api.html) requires Node.js 18 or higher.

### [Previous: More examples ](/{{ page.lang }}/starter/examples.html)
