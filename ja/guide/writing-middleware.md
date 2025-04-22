---
layout: page
title: Express アプリで使用するミドルウェアを書く
description: Express.jsアプリケーション用にカスタムミドルウェア関数を作成する方法を学びます。例や、リクエストとレスポンスの処理を強化するためのベストプラクティスなどです。
menu: guide
lang: en
redirect_from: ""
---

# Express アプリで使用するミドルウェアを書く

<h2>概要</h2>

_Middleware_ 関数は、format@@0(/{{ page.lang }}/4x/api) にアクセスできる関数です。 tml#req) (`req`), [response object](/{{ page.lang }}/4x/api.html#res) (`res`), アプリケーションのリクエスト応答サイクルでの `next` 関数. `next` 関数はExpressルータ内の関数で、呼び出されたときに現在のミドルウェアを継承してミドルウェアを実行します。

ミドルウェア機能は以下のタスクを実行できます。

- 任意のコードを実行します。
- リクエストとレスポンスオブジェクトに変更を加えます。
- リクエストレスポンスサイクルを終了します。
- スタック内の次のミドルウェアを呼び出します。

現在のミドルウェア関数がリクエスト応答サイクルを終了しない場合は、次のミドルウェア関数に制御を渡すために `next()` を呼び出す必要があります。 そうでなければ、リクエストはハングアップのままになります。

次の図はミドルウェア関数呼び出しの要素を示しています。

<table id="mw-fig">
<tbody><tr><td id="mw-fig-imgcell">
<img src="/images/express-mw.png" alt="Elements of a middleware function call" id="mw-fig-img" />
</td>
<td class="mw-fig-callouts">
<div class="callout" id="callout1">ミドルウェア関数が適用される HTTP メソッド。</div></tbody>

<div class="callout" id="callout2">ミドルウェア関数が適用されるパス(ルート)。</div>

<div class="callout" id="callout3">ミドルウェア関数。</div>

<div class="callout" id="callout4">規約ごとに「next」と呼ばれるミドルウェア関数へのコールバック引数。</div>

<div class="callout" id="callout5">HTTP <a href="/{{ page.lang }}/4x/api.html#res">レスポンス</a> は、規約によって「res」と呼ばれるミドルウェア関数への引数です。</div>

<div class="callout" id="callout6">HTTP <a href="/{{ page.lang }}/4x/api.html#req">は "req" と呼ばれるミドルウェア関数に</a> 引数を要求します。</div>
</td></tr>
</table>

Express 5以降、Promiseを返すミドルウェア関数はエラーの拒否またはスロー時に「next(value)」を呼び出します。 `next`は、拒否された値またはスローされたエラーで呼び出されます。

<h2>例</h2>

以下は、簡単な「Hello World」エクスプレスアプリケーションの例です。
The remainder of this article will define and add three middleware functions to the application:
one called `myLogger` that prints a simple log message, one called `requestTime` that
displays the timestamp of the HTTP request, and one called `validateCookies` that validates incoming cookies.

```js
const express = require('express')
const app = express()

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(3000)
```

<h3>ミドルウェア関数 myLogger</h3>
以下は、「myLogger」というミドルウェア関数の簡単な例です。 この関数は、アプリへのリクエストがそれを通過したときに "LOGGED" を出力するだけです。 ミドルウェア関数は `myLogger` という名前の変数に割り当てられます。

```js
const myLogger = function (req, res, next) {
  console.log('LOGGED')
  next()
}
```

<div class="doc-box doc-notice" markdown="1">
上記の `next()` の呼び出しに注目してください。 この関数を呼び出すと、アプリケーションで次のミドルウェア関数が呼び出されます。
`next()`関数はNode.jsやExpress APIの一部ではなく、ミドルウェア関数に渡される3番目の引数です。 `next()`関数には何でも名前を付けることができますが、慣習上は常に「next」と名付けられています。
混乱を避けるため、常にこの規約を使用してください。
</div>

ミドルウェア関数をロードするには、ミドルウェア関数を指定して `app.use()` を呼び出します。
例えば、次のコードはルートパス(/)の前に`myLogger`ミドルウェア関数をロードします。

```js
const express = require('express')
const app = express()

const myLogger = function (req, res, next) {
  console.log('LOGGED')
  next()
}

app.use(myLogger)

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(3000)
```

アプリがリクエストを受け取るたびに、「LOGGED」というメッセージが端末に出力されます。

ミドルウェアのロード順序は重要です。最初にロードされるミドルウェア関数も最初に実行されます。

ルートパスの後に`myLogger`がロードされている場合、リクエストは到達せず、アプリは"LOGGED"を出力しません。 なぜなら、ルートパスのルートハンドラは、リクエスト応答サイクルを終了するからです。

ミドルウェア関数 `myLogger` は単にメッセージを出力します。 次に、`next()`関数を呼び出すことで、スタック内の次のミドルウェア関数にリクエストを渡します。

<h3>ミドルウェア関数requestTime</h3>

次に、"requestTime" というミドルウェア関数を作成し、リクエストオブジェクトに `requestTime`
というプロパティを追加します。

```js
const requestTime = function (req, res, next) {
  req.requestTime = Date.now()
  next()
}
```

アプリは `requestTime` ミドルウェア関数を使用します。 また、ルートのコールバック関数はミドルウェア関数が`req`（リクエストオブジェクト）に追加するプロパティを使用します。

```js
const express = require('express')
const app = express()

const requestTime = function (req, res, next) {
  req.requestTime = Date.now()
  next()
}

app.use(requestTime)

app.get('/', (req, res) => {
  let responseText = 'Hello World!<br>'
  responseText += `<small>Requested at: ${req.requestTime}</small>`
  res.send(responseText)
})

app.listen(3000)
```

アプリのルートにリクエストを送信すると、アプリはブラウザにリクエストのタイムスタンプを表示するようになりました。

<h3>ミドルウェア関数 validateCookies</h3>

最後に、入力されたクッキーを検証するミドルウェア機能を作成し、クッキーが無効な場合に400回のレスポンスを送信します。

ここでは、外部非同期サービスで Cookie を検証する機能の例を示します。

```js
async function cookieValidator (cookies) {
  try {
    await externallyValidateCookie(cookies.testCookie)
  } catch {
    throw new Error('Invalid cookies')
  }
}
```

ここでは、[`cookie-parser`](/resources/middleware/cookie-parser.html) ミドルウェアを使用して、`req`オブジェクトから入ってくるCookieを解析し、それを私たちの`cookieValidator`関数に渡します。 `validateCookies`ミドルウェアは、拒否時に自動的にエラーハンドラをトリガーするPromiseを返します。

```js
const express = require('express')
const cookieParser = require('cookie-parser')
const cookieValidator = require('./cookieValidator')

const app = express()

async function validateCookies (req, res, next) {
  await cookieValidator(req.cookies)
  next()
}

app.use(cookieParser())

app.use(validateCookies)

// error handler
app.use((err, req, res, next) => {
  res.status(400).send(err.message)
})

app.listen(3000)
```

<div class="doc-box doc-notice" markdown="1">
`await cookieValidator(req.cookies)`の後に`next()`が呼び出されることに注意してください。 これにより、`cookieValidator` が解決した場合、スタック内の次のミドルウェアが呼ばれます。 `next()` 関数に (ストリング `'route'` を除く) 何らかを渡すと、Express は、現在のリクエストでエラーが発生したと想定して、エラーが発生していない残りのすべての処理のルーティングとミドルウェア関数をスキップします。そのエラーを何らかの方法で渡す場合は、次のセクションで説明するようにエラー処理ルートを作成する必要があります。
</div>

リクエストオブジェクト、レスポンスオブジェクト、スタック内の次のミドルウェア関数、そしてノード全体にアクセスできるためです。 s API、ミドルウェア関数の可能性は無限大です。

Express ミドルウェアについて詳しくは、[Express ミドルウェアの使用](/{{ page.lang }}/guide/using-middleware.html)を参照してください。

<h2>設定可能なミドルウェア</h2>

ミドルウェアの設定が必要な場合は、optionsオブジェクトや他のパラメータを受け付ける関数をエクスポートしてください。 入力パラメータに基づいてミドルウェアの実装を返します。

ファイル: `my-middleware.js`

```js
module.exports = function (options) {
  return function (req, res, next) {
    // Implement the middleware function based on the options object
    next()
  }
}
```

ミドルウェアを以下のように使用できるようになりました。

```js
const mw = require('./my-middleware.js')

app.use(mw({ option1: '1', option2: '2' }))
```

構成可能なミドルウェアの例については、 [cookie-session](https://github.com/expressjs/cookie-session) と [compression](https://github.com/expressjs/compression) を参照してください。
