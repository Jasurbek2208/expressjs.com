---
layout: page
title: 在快递中服务静态文件
description: 了解如何在 Express.js 中使用内置的 'static' 中间件来为静态文件服务，例如图像、 CSS 和 JavaScript 服务。
menu: starter
lang: 中
redirect_from: ""
---

# 在快递中服务静态文件

若要用于静态文件，如图像，CSS 文件和 JavaScript 文件，请使用 `express.static` 内置的中间件函数。

函数签名是：

```js
express.static(root, [options])
```

`root`参数指定了用于静态资产的根目录。
更多关于 "options" 参数的信息，见 [express.static](/{{page.lang}}/4x/api.html#express.static)。

例如，在一个名为“公开”的目录中使用以下代码来为图像、CSS 文件和 JavaScript 文件服务：

```js
app.use(express.static('public'))
```

现在，你可以加载在 `public` 目录中的文件：

```text
http://localhost:3000/images/kitten.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/images/bg.png
http://localhost:3000/hello.html
```

<div class="doc-box doc-info">
Express 相对于静态目录查找文件，因此静态目录的名称不是此 URL 的一部分。
</div>

要使用多个静态资源目录，多次调用 `expres.static` 中间件函数：

```js
app.use(express.static('public'))
app.use(express.static('files'))
```

快速以`express.static`中间件函数设置静态目录的顺序查找文件。

{% capture alert_content %}
为了取得最佳结果，[使用反向代理](/{{page.lang}}/advanced/best-practice-performance.html#use-a-reverse-proxy) 缓存来提高静态资产的性能。
{% endcapture %}
{% include admonitions/note.html content=alert_content %}

要为 `express.static` 函数提供的文件创建虚拟路径前缀（路径并不实际存在于文件系统中），请为静态目录[指定安装路径](/{{ page.lang }}/4x/api.html#app.use)，如下所示：

```js
app.use('/static', express.static('public'))
```

现在，你可以从`/static`前缀加载`public`目录中的文件。

```text
http://localhost:3000/static/images/kitten.jpg
http://localhost:3000/static/css/style.css
http://localhost:3000/static/js/app.js
http://localhost:3000/static/images/bg.png
http://localhost:3000/static/hello.html
```

然而，你提供的 `express.static` 函数的路径是相对于你启动你的 `node` 进程的目录。 如果您从另一个目录运行表达式应用程序，使用您想要服务的目录的绝对路径将更安全：

```js
const path = require('path')
app.use('/static', express.static(path.join(__dirname, 'public')))
```

关于 `serve-static` 函数及其选项的更多详情，请见  [serve-static](/resources/middleware/serve-static.html)。

### [Previous: Basic Routing ](/{{ page.lang }}/starter/basic-routing.html)&nbsp;&nbsp;&nbsp;&nbsp;[Next: More examples ](/{{ page.lang }}/starter/examples.html)
