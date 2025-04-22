---
layout: page
title: Express での静的ファイルの提供
description: 組み込みの 'static' ミドルウェアを使用して、Express.js アプリケーションで画像、CSS、JavaScript などの静的ファイルを提供する方法を理解します。
menu: starter
lang: en
redirect_from: ""
---

# Express での静的ファイルの提供

画像、CSSファイル、JavaScriptファイルなどの静的ファイルを提供するには、Express で組み込まれているミドルウェア関数「express.static」を使用します。

関数の署名は次のとおりです:

```js
express.static(root, [options])
```

`root` 引数は、静的アセットを提供するルートディレクトリを指定します。
引数 `options` の詳細については、 [express.static](/{{page.lang}}/4x/api.html#express.static) を参照してください。

例えば、`public`という名前のディレクトリに画像、CSSファイル、JavaScriptファイルを表示するには、次のコードを使用します。

```js
app.use(express.static('public'))
```

`public` ディレクトリにあるファイルを読み込むことができます。

```text
http://localhost:3000/images/kitten.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/images/bg.png
http://localhost:3000/hello.html
```

<div class="doc-box doc-info">
Express は静的ディレクトリからの相対的なファイルを検索するため、静的ディレクトリの名前はURLの一部ではありません。
</div>

複数の静的アセットディレクトリを使用するには、`express.static` ミドルウェア関数を複数回呼び出します。

```js
app.use(express.static('public'))
app.use(express.static('files'))
```

Express は、`express.static` ミドルウェア関数で静的ディレクトリを設定する順序でファイルを検索します。

{% capture alert_content %}
最高の結果を得るために、静的アセットを提供するパフォーマンスを向上させるために、[リバースプロキシを使用](/{{page.lang}}/advanced/best-practice-performance.html#use-a-reverse-proxy) キャッシュを使用します。
{% endcapture %}
{% include admonitions/note.html content=alert_content %}

`express.static` 関数によって提供されるファイルの仮想パスのプレフィックス (パスは実際にはファイル・システムに存在しません) を作成するには、次に示すように、静的ディレクトリーの[マウント・パスを指定](/{{ page.lang }}/4x/api.html#app.use)します。

```js
app.use('/static', express.static('public'))
```

`/static` というプレフィックスから、 `public` ディレクトリにあるファイルをロードできます。

```text
http://localhost:3000/static/images/kitten.jpg
http://localhost:3000/static/css/style.css
http://localhost:3000/static/js/app.js
http://localhost:3000/static/images/bg.png
http://localhost:3000/static/hello.html
```

しかし、`express.static`関数に与えるパスは、`node`プロセスを起動したディレクトリからの相対パスです。 expressアプリを別のディレクトリから実行する場合、提供したいディレクトリの絶対パスを使用する方が安全です:

```js
const path = require('path')
app.use('/static', express.static(path.join(__dirname, 'public')))
```

`serve-static` 関数とそのオプションの詳細については、  [serve-static](/resources/middleware/serve-static.html) を参照してください。

### [Previous: Basic Routing](/{{ page.lang }}/starter/basic-routing.html)&nbsp;&nbsp;&nbsp;&nbsp;[Next: More examples](/{{ page.lang }}/starter/examples.html)
