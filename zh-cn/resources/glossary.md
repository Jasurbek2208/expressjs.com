---
layout: page
title: 快递术语表
description: 与Express.js, Node.js, midleware, routing, 以及其他关键概念有关的术语的综合词汇，以帮助您有效地理解和使用Express。
menu: resources
lang: 中
redirect_from: ""
---

# Glossary

### 应用程序

一般来说，一个或多个旨在为特定目的开展业务的方案。  在Express背景下，一个使用 Node.js 平台上运行的Express API程序。  Might also refer to an [app object](/{{ page.lang }}/api.html#express).

### API

应用程序编程接口。 首次使用缩写时拼写。

### 快照

为 Node.js 应用程序提供一个快速、无视、最小化的网页框架。 一般来说，“Express.js”比“Express.js”更受欢迎，尽管后者是可以接受的。

### libuv

一个以异步I/O为重点的多平台支持库，主要开发供Node.js使用。

### 中间件

快速路由图层在最后请求处理器之前调用的函数， 并因此处于原始请求与最终预定路线之间的中间位置。 围绕中间层的几个精细术语：

- `var foo = required('middleware)` 称为_requiring_ 或 _using_a Node.js 模块。 然后，语句`var mw = foo()`通常返回中间件。
- `app.use(mw)` 称为_将中间件添加到全局处理堆栈。
- `app.get('/foo', mw, function (req, res) })`被称为_添加中间件到"GET /foo"处理堆栈_。

### Node.js

一个用于构建可扩展网络应用程序的软件平台。 Node.js 使用 JavaScript 作为其脚本语言，并通过非屏蔽I/O 和单线程事件循环实现了高通量。 见 [nodejs.org](https://nodejs.org/en/)。 **用法说明**：最初，"Node.js"之后"Node"。

### 开源、开源

当用作形容词时，连字符串。例如：“这是开源软件。” See [Open-source software on Wikipedia](http://en.wikipedia.org/wiki/Open-source_software).

{% include admonitions/note.html content="虽然不将这个词混合是常见的，但我们正在使用标准的英国规则来混合复合形状。" %}

### 请求

HTTP请求。 客户端向服务器提交一个 HTTP 请求消息，服务器将返回响应。  HTTP 请求。客户机向服务器提交 HTTP 请求消息，然后服务器返回响应。该请求必须使用若干[请求方法](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)之一，例如 GET、POST 等。

### 应答

HTTP响应。 服务器返回客户端的 HTTP 响应消息。 回复包含请求的完成状态信息，并可能包含请求内容在其消息机构。

### 路由

识别资源的 URL 的一部分。 例如，在`http://fo.com/products/id`, "/products/id"是路线。

### 路由器

请参阅“API 参考”中的[路由器](/{{ page.lang }}/4x/api.html#router)。
