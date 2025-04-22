---
layout: page
title: 开发快递模板引擎
description: 学习如何使用 app.engine()，为Express.js 开发自定义的模板引擎，并用实例创建和整合您自己的模板渲染逻辑。
menu: advanced
lang: 中
redirect_from: ""
---

# 开发快递模板引擎

使用 `app.engine(ext, callback)` 方法来创建您自己的模板引擎。 `ext` 是指文件扩展名，而`callback` 是模板引擎函数。 接受以下项目作为参数：文件的位置、选项对象和回调函数。

下面的代码是实现渲染`.ntl`文件的非常简单的模板引擎的例子。

```js
const fs = require('fs') // this engine requires the fs module
app.engine('ntl', (filePath, options, callback) => { // define the template engine
  fs.readFile(filePath, (err, content) => {
    if (err) return callback(err)
    // this is an extremely simple template engine
    const rendered = content.toString()
      .replace('#title#', `<title>${options.title}</title>`)
      .replace('#message#', `<h1>${options.message}</h1>`)
    return callback(null, rendered)
  })
})
app.set('views', './views') // specify the views directory
app.set('view engine', 'ntl') // register the template engine
```

您的应用现在可以渲染`.ntl`文件。 在`views`目录中创建一个具有以下内容的名为 `index.ntl`的文件。

```pug
#title#
#message#
```

然后在您的应用中创建以下路线。

```js
app.get('/', (req, res) => {
  res.render('index', { title: 'Hey', message: 'Hello there!' })
})
```

当您向主页提出请求时，`index.ntl`将以 HTML格式呈现。