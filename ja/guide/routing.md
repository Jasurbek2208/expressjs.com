---
layout: page
title: 高速ルーティング
description: Express.jsアプリケーションでルートを定義して使用する方法を学びます。ルートメソッド、ルートパス、パラメータ、モジュラールーティングにルーターを使用する方法を学びます。
menu: guide
lang: en
redirect_from: ""
---

# ルーティング

_Routing_ とは、アプリケーションのエンドポイント(URI)がクライアントリクエストに対してどのように応答するかを指します。
For an introduction to routing, see [Basic routing](/{{ page.lang }}/starter/basic-routing.html).

HTTPメソッドに対応するExpress `app` オブジェクトのメソッドを使用してルーティングを定義します。
のように、`app。 POST リクエストを処理する GET リクエストと `app.post\` を処理します。 完全なリストについては、
を参照してください。 [app.METHOD](/{{ page.lang }}/5x/api.html#app.METHOD). You can also use [app.all()](/{{ page.lang }}/5x/api.html#app.all) to handle all HTTP methods and [app.use()](/{{ page.lang }}/5x/api.html#app.use) to
specify middleware as the callback function (See [Using middleware](/{{ page.lang }}/guide/using-middleware.html) for details).

これらのルーティングメソッドは、アプリケーションが指定されたルート (エンドポイント) と HTTP メソッドへのリクエストを受け取ったときに呼び出されるコールバック関数 ("handler functions" と呼ばれることもあります) を指定します。 言い換えれば、アプリケーションは指定されたルートとメソッドに一致するリクエストを「リッスン」します。 マッチを検出すると、指定されたコールバック関数を呼び出します。

実際、ルーティングメソッドは引数として複数のコールバック関数を持つことができます。
複数のコールバック関数を使用。 コールバック関数に `next` を引数として渡し、関数の本体内で `next()` を呼び出して、次のコールバックに
を渡すことが重要です。

以下のコードは、非常に基本的なルートの例です。

```js
const express = require('express')
const app = express()

// respond with "hello world" when a GET request is made to the homepage
app.get('/', (req, res) => {
  res.send('hello world')
})
```

<h2 id="route-methods">ルートメソッド</h2>

routeメソッドはHTTPメソッドのいずれかから派生し、`express` クラスのインスタンスに追加されます。

以下のコードは、`GET` と `POST` メソッドを定義したルートの例です。

```js
// GET method route
app.get('/', (req, res) => {
  res.send('GET request to the homepage')
})

// POST method route
app.post('/', (req, res) => {
  res.send('POST request to the homepage')
})
```

Expressは、すべてのHTTPリクエストメソッドに対応するメソッドをサポートしています: `get`、`post`など。
完全なリストについては、 [app.METHOD](/{{ page.lang }}/5x/api.html#app.METHOD) を参照してください。

特別なルーティングメソッド`app.all()`があり、_all_HTTPリクエストメソッドのパスにミドルウェア関数をロードするために使用されます。 例えば、`GET`を使用しているかどうかに関わらず、ルート`"/secret"へのリクエストに対して以下のハンドラが実行されます。 `POST`、`PUT`、`DELETE\`、または[http module](https://nodejs.org/api/http.html#http_http_methods)でサポートされている他のHTTPリクエストメソッド。

```js
app.all('/secret', (req, res, next) => {
  console.log('Accessing the secret section ...')
  next() // pass control to the next handler
})
```

<h2 id="route-paths">ルートパス</h2>

ルートパスはリクエストメソッドと組み合わせて、リクエストを作成できるエンドポイントを定義します。 ルートパスは文字列、文字列パターン、または正規表現であることができます。

{% capture caution-character %} 5では、文字 `? を表現します。 、`+`、`\*`、`[]`、および`()\`はバージョン4とは異なり、format@@0(/{{ page.lang }}/guide/migrating-5を確認してください。 詳細についてはtml#path-syntax){% endcapture %}

{% include admonitions/care.html content=cartion-character %}

{% capture note-dollar-character %}エクスプレッション4では、`$`のような正規表現文字を`\`でエスケープする必要があります。
{% endcapture %}

{% include admonitions/care.html content=note-dollar-character %}

{% capture note-path-to-regexp %}
Express ではルートパスに一致する [path-to-regexp](https://www.npmjs.com/package/path-to-regexp) を使用しています。ルートパスの定義におけるすべての可能性については、path-to-regexp ドキュメントを参照してください。 [Express Playground Router](https://bjohansebas.github.io/playground-router/)は、パターンマッチングをサポートしていませんが、基本的なExpressルートをテストするための便利なツールです。
{% endcapture %}

{% include admonitions/note.html content=note-path-to-regexp %}

{% include admonitions/warning.html content="クエリー文字列はルートパスの一部ではありません。 %}

### 文字列に基づく経路パス

このルートパスはルートルートのリクエストと一致します。

```js
app.get('/', (req, res) => {
  res.send('root')
})
```

このルートパスは `/about` へのリクエストと一致します。

```js
app.get('/about', (req, res) => {
  res.send('about')
})
```

このルートパスは `/random.text` へのリクエストと一致します。

```js
app.get('/random.text', (req, res) => {
  res.send('random.text')
})
```

### 文字列パターンに基づく経路パス

{% capture caution-string-patterns %} Express 5の文字列パターンが動作しなくなりました。 Please refer to the [migration guide](/{{ page.lang }}/guide/migrating-5.html#path-syntax) for more information.{% endcapture %}

{% include admonitions/care.html content=cartion-string-pattern %}

このルートパスは `acd` と `abcd` に一致します。

```js
app.get('/ab?cd', (req, res) => {
  res.send('ab?cd')
})
```

このルートパスは `abcd`、`abbcd`、`abbcd`などにマッチします。

```js
app.get('/ab+cd', (req, res) => {
  res.send('ab+cd')
})
```

このルートパスは `abcd`、`abxcd`、`abrandoMcd`、`ab123cd`などにマッチします。

```js
app.get('/ab*cd', (req, res) => {
  res.send('ab*cd')
})
```

このルートパスは `/abe` と `/abcde` に一致します。

```js
app.get('/ab(cd)?e', (req, res) => {
  res.send('ab(cd)?e')
})
```

### 正規表現に基づく経路パス

このルートパスは "a" と一致します。

```js
app.get(/a/, (req, res) => {
  res.send('/a/')
})
```

このルートは`蝶々`と`トンボ`にマッチしますが、`蝶々`、`トンボフライマン`などにはマッチしません。

```js
app.get(/.*fly$/, (req, res) => {
  res.send('/.*fly$/')
})
```

<h2 id="route-parameters">ルートパラメータ</h2>

ルートパラメータは、URL 内の位置で指定された値をキャプチャするために使用される名前付きの URL セグメントです。 取得した値は `req.params` オブジェクト内に入力され、パス内でそれぞれのキーとして指定されたrouteパラメータの名前が入力されます。

```
Route path: /users/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userId": "34", "bookId": "8989" }
```

ルートパラメータを使用してルートを定義するには、以下のようにルートのパスにルートパラメータを指定します。

```js
app.get('/users/:userId/books/:bookId', (req, res) => {
  res.send(req.params)
})
```

<div class="doc-box doc-notice" markdown="1">
ルートパラメータの名前は「単語文字」([A-Za-z0-9_])で構成されている必要があります。
</div>

ハイフン(`-`)とドット(`.`)は文字通り解釈されるので、ルートパラメータとともに便利な目的で使うことができます。

```
Route path: /flights/:from-:to
Request URL: http://localhost:3000/flights/LAX-SFO
req.params: { "from": "LAX", "to": "SFO" }
```

```
Route path: /plantae/:genus.:species
Request URL: http://localhost:3000/plantae/Prunus.persica
req.params: { "genus": "Prunus", "species": "persica" }
```

{% capture warning-regexp %}
In express 5, Regexp characters are not supported in route paths, for more information please refer to the [migration guide](/{{ page.lang }}/guide/migrating-5.html#path-syntax).{% endcapture %}

{% include admonitions/care.html content=warning-regexp %}

route (ルート)パラメータにマッチする正確な文字列をより詳細に制御するには、括弧(`()`)で正規表現を追加します。

```
Route path: /user/:userId(\d+)
Request URL: http://localhost:3000/user/42
req.params: {"userId": "42"}
```

{% include admonitions/warning. tml content="通常、正規表現はリテラル文字列の一部であるため、 `\\d+`のようにバックスラッシュを追加して`\`文字をエスケープするようにしてください。 %}

Express 4.xでは、<a href="https://github.com/expressjs/express/issues/2495">正規表現の<code>_</code>文字は通常の方法で解釈されません。</a>回避策として、<code>_</code>の代わりに<code>{0,}</code>を使用してください。これは、Express 5で修正される可能性があります。
回避策として、`*` の代わりに `{0,}` を使用します。 これはExpress 5で修正される可能性があります。
{% endcapture %}

{% include admonitions/warning.html content=warning-version %}

<h2 id="route-handlers">Route handlers</h2>

リクエストを処理するために、 [middleware](/{{ page.lang }}/guide/using-middleware.html) のように動作する複数のコールバック関数を提供できます。 唯一の例外は、これらのコールバックが `next('route')` を呼び出して、残りのルートコールバックをバイパスすることです。 このメカニズムを使用して、ルート上に事前条件を設定できます。 次に現在のルートを進める理由がなければ次のルートに制御を渡す。

ルートハンドラは、次の例に示すように、関数、関数の配列、または両方の組み合わせの形式で使用できます。

単一のコールバック関数はルートを処理できます。 例:

```js
app.get('/example/a', (req, res) => {
  res.send('Hello from A!')
})
```

複数のコールバック関数がルートを処理できます (`next` オブジェクトを指定してください)。 例:

```js
app.get('/example/b', (req, res, next) => {
  console.log('the response will be sent by the next function ...')
  next()
}, (req, res) => {
  res.send('Hello from B!')
})
```

コールバック関数の配列はルートを処理できます。 例:

```js
const cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

const cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

const cb2 = function (req, res) {
  res.send('Hello from C!')
}

app.get('/example/c', [cb0, cb1, cb2])
```

独立した関数と関数の配列の組み合わせは、ルートを処理することができます。 例:

```js
const cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

const cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

app.get('/example/d', [cb0, cb1], (req, res, next) => {
  console.log('the response will be sent by the next function ...')
  next()
}, (req, res) => {
  res.send('Hello from D!')
})
```

<h2 id="response-methods">レスポンスメソッド</h2>

次の表のレスポンスオブジェクト (`res`) のメソッドは、クライアントにレスポンスを送信し、リクエスト応答のサイクルを終了することができます。 これらのメソッドのいずれもルートハンドラから呼び出されない場合、クライアントリクエストはハングしたままになります。

| 方法                                                                                                                                                                                                                        | 説明                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| [res.download()](/{{ page.lang }}/5x/api.html#res.download)     | ダウンロードするファイルを指示します。                       |
| [res.end()](/{{ page.lang }}/5x/api.html#res.end)               | 応答プロセスを終了します。                             |
| [res.json()](/{{ page.lang }}/5x/api.html#res.json)             | JSON 応答を送信します。                            |
| [res.jsonp()](/{{ page.lang }}/5x/api.html#res.jsonp)           | JSONP サポートを使用して JSON 応答を送信します。            |
| [res.redirect()](/{{ page.lang }}/5x/api.html#res.redirect)     | リダイレクトします。                                |
| [res.render()](/{{ page.lang }}/5x/api.html#res.render)         | ビューテンプレートをレンダリングします。                      |
| [res.send()](/{{ page.lang }}/5x/api.html#res.send)             | さまざまなタイプの応答を送信します。                        |
| [res.sendFile()](/{{ page.lang }}/5x/api.html#res.sendFile)     | ファイルをオクテットストリームとして送信する。                   |
| [res.sendStatus()](/{{ page.lang }}/5x/api.html#res.sendStatus) | レスポンスステータスコードを設定し、文字列表現をレスポンスボディとして送信します。 |

<h2 id="app-route">app.route()</h2>

`app.route()` を使用すると、ルートパスに対してチェーン可能なルートハンドラを作成できます。
パスは単一の場所で指定されているため、モジュラールートを作成することは、冗長性とタイプミスを削減するのに役立ちます。 ルートの詳細については、以下を参照してください: [Router() documentation](/{{ page.lang }}/5x/api.html#router)。

以下は、`app.route()`を使用して定義されたルートハンドラの例です。

```js
app.route('/book')
  .get((req, res) => {
    res.send('Get a random book')
  })
  .post((req, res) => {
    res.send('Add a book')
  })
  .put((req, res) => {
    res.send('Update the book')
  })
```

<h2 id="express-router">express.Router</h2>

`express.Router` クラスを使用して、モジュール化されたマウント可能なルートハンドラを作成します。 `Router`インスタンスは完全なミドルウェアとルーティングシステムです。そのため、しばしば「ミニアプリ」と呼ばれます。

次の例では、ルータをモジュールとして作成し、ミドルウェア関数をロードします。 いくつかのルートを定義し、メインアプリのパスにルータモジュールをマウントします。

appディレクトリに`birds.js`という名前のルーターファイルを作成します。以下の内容を使用します。

```js
const express = require('express')
const router = express.Router()

// middleware that is specific to this router
const timeLog = (req, res, next) => {
  console.log('Time: ', Date.now())
  next()
}
router.use(timeLog)

// define the home page route
router.get('/', (req, res) => {
  res.send('Birds home page')
})
// define the about route
router.get('/about', (req, res) => {
  res.send('About birds')
})

module.exports = router
```

次に、アプリにルーターモジュールをロードします。

```js
const birds = require('./birds')

// ...

app.use('/birds', birds)
```

アプリは `/birds` と `/birds/about` へのリクエストを処理できるようになりました。 同様に、ルート固有の「timeLog」ミドルウェア関数を呼び出します。

ただし、親ルート `/birds` にパスパラメータがある場合、サブルートからデフォルトではアクセスできません。 アクセス可能にするには、 `mergeParams` オプションを Router コンストラクタ [reference](/{{ page.lang }}/5x/api.html#app.use) に渡す必要があります。

```js
const router = express.Router({ mergeParams: true })
```
