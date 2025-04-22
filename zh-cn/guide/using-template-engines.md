---
layout: page
title: 使用快递模板引擎
description: 探索如何整合和使用模板引擎，例如Pug、Handlebar和 EJS 与 Express.js 一起高效率地渲染动态的 HTML 页面。
menu: guide
lang: 中
redirect_from: ""
---

# 使用快递模板引擎

一个 _template 引擎允许您在应用程序中使用静态模板文件。 运行时，模板引擎替换了一个具有实际值的模板文件中的
变量。 并将模板转换为发送到客户端的 HTML 文件。
这种方法使设计一个 HTML 页面变得更加容易。

The [Express application generator](/{{ page.lang }}/starter/generator.html) uses [Pug](https://pugjs.org/api/getting-started.html) as its default, but it also supports [Handlebars](https://www.npmjs.com/package/handlebars), and [EJS](https://www.npmjs.com/package/ejs), among others.

To render template files, set the following [application setting properties](/{{ page.lang }}/4x/api.html#app.set), in the default `app.js` created by the generator:

- `views`, 模板文件所在的目录。 Eg: `app.set('views', './views')`
  默认在应用程序根目录中的 "views" 目录。
- “查看引擎”，即要使用的模板引擎。 例如，使用 Pug 模板引擎：`app.set('view 引擎、'pug')` 。

然后安装相应的模板引擎 npm 包；例如安装Pug：

```bash
$ npm install pug --save
```

<div class="doc-box doc-notice" markdown="1">
与 Express 兼容的模板引擎（例如 Pug）导出名为 `__express(filePath, options, callback)` 的函数，该函数由 `res.render()` 函数调用以呈现模板代码。
某些模板引擎并不遵循此约定。[Consolidate.js](https://www.npmjs.org/package/consolidate) 库通过映射所有流行的 Node.js 模板引擎来遵循此约定，因此可以在 Express 内无缝工作。


某些模板引擎没有遵循此约定。 [@ladjs/consolidate](https://www.npmjs.com/package/@ladjs/consolidate)
库通过映射所有流行的 Node.js 模板引擎来遵循此公约，因此在Express内无缝工作。

</div>

设置视图引擎后，您无需在应用中指定引擎或加载模板引擎模块；
表达式内部加载模块，例如：

```js
app.set('view engine', 'pug')
```

然后，在 `views` 目录中创建一个名为 `index.pug` 的 Pug 模板文件，其内容如下：

```pug
html
  head
    title= title
  body
    h1= message
```

创建一个路由来渲染`index.pug`文件。 如果未设置 `view 引擎` 属性，
您必须指定 `view` 文件的扩展名。 否则，你可以省略它。

```js
app.get('/', (req, res) => {
  res.render('index', { title: 'Hey', message: 'Hello there!' })
})
```

当您向主页提出请求时，`index.pug`文件将以 HTML格式呈现。

视图引擎缓存不缓存模板输出的内容，只有底层模板本身。 即使缓存已开启，视图仍然与每个请求重渲。
