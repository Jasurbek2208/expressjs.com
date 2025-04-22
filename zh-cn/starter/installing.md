---
layout: page
title: 安装Express
description: 学习如何在您的 Node.js 环境中安装 Express.js，包括设置您的项目目录和使用 npm 管理依赖关系。
menu: starter
lang: 中
redirect_from: ""
---

# 正在安装

假定您已经安装 [Node.js](https://nodejs.org/)，创建一个目录来保存您的应用程序，并使您的工作目录变得正常。

- [Express 4.x](/{{ page.lang }}/4x/api.html) requires Node.js 0.10 or higher.
- [Express 5.x](/{{ page.lang }}/5x/api.html) requires Node.js 18 or higher.

```bash
$ mkdir myapp
$ cd myapp
```

使用 `npm init` 命令为您的应用程序创建 `package.json` 文件。
欲了解更多关于 `package.json` 如何工作的信息，请参阅[Specifics of npm's package.json handling](https://docs.npmjs.com/files/package.json)。

```bash
$ npm init
```

此命令提示您一些东西，例如应用程序的名称和版本。
现在，您只需按下RETURN 即可接受大部分默认值，但以下除外：

```
entry point: (index.js)
```

输入`app.js`, 或你想要的主文件名称. 如果你想要它是 `index.js`，请点击 RETURN 来接受建议的默认文件名称。

现在，在“myapp”目录中安装Express并将其保存在依赖列表中。 例如：

```bash
$ npm install express
```

暂时安装快递，不要将其添加到依赖列表中：

```bash
$ npm install express --no-save
```

<div class="doc-box doc-info" markdown="1">
默认情况下，版本为 npm 5.0+, `npm install` 将模块添加到 `软件包中的`依赖'列表。 son`文件; 使用早期版本的 npm 必须明确指定`--save`选项。 然后在应用目录中运行 `npm install` 将自动安装依赖列表中的模块。
</div>

### [Next: Hello World ](/{{ page.lang }}/starter/hello-world.html)