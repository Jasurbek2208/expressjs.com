---
layout: page
title: エクスプレス「Hello World」の例
description: Express.jsを始めるには、シンプルな「Hello World」アプリケーションを構築しましょう。初心者向けの基本的なセットアップとサーバー作成を説明します。
menu: starter
lang: en
redirect_from: ""
---

# Hello world example

<div class="doc-box doc-info" markdown="1">
以下に埋め込まれているのは、基本的に作成できる最も簡単なExpressアプリです。 It is a single file app &mdash; _not_ what you'd get if you use the [Express generator](/{{ page.lang }}/starter/generator.html), which creates the scaffolding for a full app with numerous JavaScript files, Jade templates, and sub-directories for various purposes.
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

このアプリはサーバーを起動し、接続のためにポート3000をリッスンします。 アプリはルート URL (`/`) または _route_ にリクエスト
を返します。 他のすべてのパスについては、**404 Not Found**で応答します。

### ローカルで実行中

最初に `myapp` という名前のディレクトリを作成し、変更して `npm init` を実行します。 Then, install `express` as a dependency, as per the [installation guide](/{{ page.lang }}/starter/installing.html).

`myapp` ディレクトリで、`app.js`という名前のファイルを作成し、上の例からコードをコピーします。

<div class="doc-box doc-notice" markdown="1">
`req` (要求) と `res` (応答) は、Node が提供するのとまったく同じオブジェクトであるため、Express が関与しない場合と同じように、`req.pipe()`、`req.on('data', callback)` などを呼び出すことができます。
</div>

次のコマンドでアプリを実行します。

```bash
$ node app.js
```

次に、ブラウザーに `http://localhost:3000/` をロードして出力を確認します。

### [Previous: Installing ](/{{ page.lang }}/starter/installing.html)&nbsp;&nbsp;&nbsp;&nbsp;[Next: Express Generator] (/{{ page.lang }}/starter/generator.html)
