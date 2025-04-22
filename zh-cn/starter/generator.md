---
layout: page
title: 快递应用程序生成器
description: 学习如何使用快递应用程序生成器工具来快速为您的 Express.js 应用程序创建骨架，简化设置和配置。
menu: starter
lang: 中
redirect_from: ""
---

# 快递应用程序生成器

使用应用程序生成器工具“express-generator”来快速创建应用程序骨架。

您可以用 `npx` 命令运行应用程序生成器(可在 Node.js 8.2.0中查找)。

```bash
$ npx express-generator
```

对于早期的节点版本，安装应用程序生成器作为全局npm 包，然后启动：

```bash
$ npm install -g express-generator
$ express
```

使用"-h"选项显示命令选项：

```bash
$ express -h

  Usage: express [options] [dir]

  Options:

    -h, --help          output usage information
        --version       output the version number
    -e, --ejs           add ejs engine support
        --hbs           add handlebars engine support
        --pug           add pug engine support
    -H, --hogan         add hogan.js engine support
        --no-view       generate without view engine
    -v, --view <engine> add view <engine> support (ejs|hbs|hjs|jade|pug|twig|vash) (defaults to jade)
    -c, --css <engine>  add stylesheet <engine> support (less|stylus|compass|sass) (defaults to plain css)
        --git           add .gitignore
    -f, --force         force on non-empty directory
```

例如，以下创建了一个名为_myapp_的快递应用程序。 该应用将被创建在当前工作目录中名为_myapp_的文件夹中，视图引擎将被设置为 <a href="https://pugjs.org/" target="_blank" title="Pug documentation">Pug</a>：

```bash
$ express --view=pug myapp

   create : myapp
   create : myapp/package.json
   create : myapp/app.js
   create : myapp/public
   create : myapp/public/javascripts
   create : myapp/public/images
   create : myapp/routes
   create : myapp/routes/index.js
   create : myapp/routes/users.js
   create : myapp/public/stylesheets
   create : myapp/public/stylesheets/style.css
   create : myapp/views
   create : myapp/views/index.pug
   create : myapp/views/layout.pug
   create : myapp/views/error.pug
   create : myapp/bin
   create : myapp/bin/www
```

然后安装依赖：

```bash
$ cd myapp
$ npm install
```

在 MacOS 或 Linux 上，使用此命令运行应用程序：

```bash
$ DEBUG=myapp:* npm start
```

在 Windows 命令提示符上，使用此命令：

```bash
> set DEBUG=myapp:* & npm start
```

在 Windows PowerShell 上，使用此命令：

```bash
PS> $env:DEBUG='myapp:*'; npm start
```

然后，在您的浏览器中加载 `http://localhost:3000/` 以访问应用程序。

生成的应用具有以下目录结构：

```bash
.
├── app.js
├── bin
│   └── www
├── package.json
├── public
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
├── routes
│   ├── index.js
│   └── users.js
└── views
    ├── error.pug
    ├── index.pug
    └── layout.pug

7 directories, 9 files
```

<div class="doc-box doc-info" markdown="1">
生成器创建的应用结构只是构建快递应用的多种方式之一。 请随时使用此结构或修改它以最适合您的需要。
</div>

### [Previous: Hello World ](/{{ page.lang }}/starter/hello-world.html)&nbsp;&nbsp;&nbsp;&nbsp;[Next: Basic routing](/{{ page.lang }}/starter/basic-routing.html)
