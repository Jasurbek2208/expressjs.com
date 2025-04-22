---
layout: page
title: 快递基本路由
description: 在 Express.js 应用程序中学习路由的基础，包括如何定义路由，处理 HTTP 方法，并为您的 web 服务器创建路由处理程序。
menu: starter
lang: 中
redirect_from: ""
---

# 基本路由

_Routing_ 指的是确定应用程序如何响应客户端请求到某个端点。 它是一个 URI (或路径) 和特定的 HTTP 请求方法 (GET, POST, 等等)。

每条路可以有一个或多个处理函数，在匹配路线时执行。

航线定义采用以下结构：

```js
app.METHOD(PATH, HANDLER)
```

在哪里：

- `app`是一个`expres`的实例。
- `METHOD` 是 [HTTP 请求方法](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)。
- `PATH`是服务器上的路径。
- `HANDLER` 是指在路由匹配时执行的函数。

<div class="doc-box doc-notice" markdown="1">
本教程假定一个名为 `app` 的实例已创建，服务器正在运行。 
本教程假定创建了名为 `app` 的 `express` 实例且服务器正在运行。如果您对创建和启动应用程序并不熟悉，请参阅 [Hello world 示例](/{{ page.lang }}/starter/hello-world.html)。

</div>

下面的例子说明如何界定简单的路线。

在主页上使用 `Hello World!` 响应：

```js
app.get('/', (req, res) => {
  res.send('Hello World!')
})
```

响应在根路由 (`/`)，应用程序的主页上的 POST 请求：

```js
app.post('/', (req, res) => {
  res.send('Got a POST request')
})
```

对 "/user" 路由响应一个 PUT 请求：

```js
app.put('/user', (req, res) => {
  res.send('Got a PUT request at /user')
})
```

对 "/user" 路由响应请求：

```js
app.delete('/user', (req, res) => {
  res.send('Got a DELETE request at /user')
})
```

有关路由的更多详细信息，请参阅[路由指南](/{{ page.lang }}/guide/routing.html)。

### [Previous: Express application generator ](/{{ page.lang }}/starter/generator.html)&nbsp;&nbsp;&nbsp;&nbsp;[Next: Serving static files in Express ](/{{ page.lang }}/starter/static-files.html)