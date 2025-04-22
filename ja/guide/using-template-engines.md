---
layout: page
title: Express でテンプレートエンジンを使用する
description: Pug、Handlebars、EJSなどのテンプレートエンジンをExpress.jsで統合して使用し、動的なHTMLページを効率的にレンダリングする方法をご覧ください。
menu: guide
lang: en
redirect_from: ""
---

# Express でテンプレートエンジンを使用する

_template engine_ を使用すると、アプリケーションで静的なテンプレート ファイルを使用できます。 実行時に、テンプレートエンジンはテンプレートファイルの
変数を実際の値に置き換えます。 をクリックして、テンプレートをクライアントに送信する HTML ファイルに変換します。
このアプローチにより、HTML ページのデザインが容易になります。

Expressで動作する一般的なテンプレートエンジンには、[Pug](https://pugjs.org/api/getting-started.html)、[Mustache](https://www.npmjs.com/package/mustache)、[EJS](https://www.npmjs.com/package/ejs)があります。[Expressアプリケーションジェネレータ](/{{ page.lang }}/starter/generator.html)は[Jade](https://www.npmjs.com/package/jade)をデフォルトとして使用しますが、いくつかの他のものもサポートしています。

テンプレートファイルをレンダリングするには、次の[アプリケーション設定プロパティ](/{{ page.lang }}/4x/api.html#app.set)を設定し、ジェネレータで作成されたデフォルトアプリの`app.js`にセットします。

- `views` テンプレートファイルがあるディレクトリ。 例: `app.set('views', './views')` 。
  デフォルトはアプリケーションのルートディレクトリにある `views` ディレクトリです。
- `viewengine` を使用するテンプレートエンジン。 たとえば、Pugテンプレートエンジンを使用するには、`app.set('view engine', 'pug')`を使います。

次に、対応するテンプレートエンジン npm パッケージをインストールします。例えば、Pug をインストールする場合:

```bash
$ npm install pug --save
```

<div class="doc-box doc-notice" markdown="1">
PugのようなExpressに準拠したテンプレートエンジンは`__express(filePath, options, callback)`,
テンプレートコードをレンダリングするために`res.render()`を呼び出します。

一部のテンプレートエンジンはこの規約に従っていません。 [@ladjs/integrate](https://www.npmjs.com/package/@ladjs/consolidate)
ライブラリは、一般的な Node.js テンプレートエンジンのすべてをマッピングすることによって、この規則に従っており、したがって、Express 内でシームレスに動作します。

</div>

ビューエンジンが設定された後、アプリケーションにエンジンを指定したりテンプレートエンジンモジュールをロードしたりする必要はありません。
Express はモジュールを内部的にロードします。例:

```js
app.set('view engine', 'pug')
```

次に、`views`ディレクトリに`index.pug`という名前のパグテンプレートファイルを作成します。

```pug
html
  head
    title= title
  body
    h1= message
```

`index.pug` ファイルをレンダリングするルートを作成します。 If the `view engine` property is not set,
you must specify the extension of the `view` file. そうでなければ、それを省略することができます。

```js
app.get('/', (req, res) => {
  res.render('index', { title: 'Hey', message: 'Hello there!' })
})
```

ホームページへのリクエストを行うと、 `index.pug` ファイルは HTML としてレンダリングされます。

ビューエンジンキャッシュはテンプレートの出力の内容をキャッシュせず、元のテンプレート自体のみキャッシュします。 キャッシュがオンの場合でも、ビューはリクエストごとに再レンダリングされます。
