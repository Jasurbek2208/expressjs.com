---
layout: page
title: Express "Hello World" 示例
description: 开始使用 Express.js 创建一个简单的“Hello World”应用程序，展示初学者的基本设置和服务器创建。
menu: starter
lang: 中
redirect_from: ""
---

# 您好世界示例

<div class="doc-box doc-info" markdown="1">
内嵌在下面是您可以创建的最简单的快递应用程序。 It is a single file app &mdash; _not_ what you'd get if you use the [Express generator](/{{ page.lang }}/starter/generator.html), which creates the scaffolding for a full app with numerous JavaScript files, Jade templates, and sub-directories for various purposes.
</div>

```js
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```

此应用启动服务器并在端口 3000 上监听连接. 这个应用响应"Hello World!"请求
到 root URL (`/`) 或 _route_. 为了每一条其他道路，它将使用 **404 找不到**。

### 本地运行

首先创建一个名为`myapp`的目录，更改它并运行 `npm init` 。 Then, install `express` as a dependency, as per the [installation guide](/{{ page.lang }}/starter/installing.html).

在 `myapp` 目录中，创建一个名为 `app.js` 的文件并从上面的示例中复制代码。

<div class="doc-box doc-notice" markdown="1">
`req`（请求）和 `res`（响应）与 Node 提供的对象完全相同，所以您可以在不涉及 Express 的情况下调用 `req.pipe()`、`req.on('data', callback)` 和要执行的其他任何函数。
</div>

使用以下命令运行应用程序：

```bash
$ node app.js
```

然后，在浏览器中加载 `http://localhost:3000/` 以查看输出。

### 这基本上是您可以创建的最简单的 Express 应用程序。这是单个文件应用程序 &mdash; 根本_不_需要动用 [Express 生成器](/{{ page.lang }}/starter/generator.html)。Express 生成器的作用就像是为完整的应用程序建立一个“脚手架”，包含各种用途的 JavaScript 文件、Jade 模板和子目录。
