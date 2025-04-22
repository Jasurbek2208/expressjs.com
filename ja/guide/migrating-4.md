---
layout: page
title: Express 4に移行
description: Express.jsアプリケーションをバージョン3からバージョン4に移行するためのガイドでは、ミドルウェアの変更、ルーティング、コードベースの効果的な更新方法について説明します。
menu: guide
lang: en
redirect_from: ""
---

# Express 4に移動中

<h2 id="overview">概要</h2>

エクスプレス4はエクスプレス3からの変更です。 つまり、Expressバージョンを依存関係で更新すると、既存のExpress 3アプリは動作しなくなります。

この記事のカバー：

<ul class="doclist">
  <li><a href="#changes">Express 4</a> の変更点。</li>
  <li><a href="#example-migration">Express 3 アプリを Express 4 に移行する例</a></li>
  <li><a href="#app-gen">Express 4 アプリケーション・ジェネレーターへのアップグレード</a></li>
</ul>

<h2 id="changes">Express 4の変更</h2>

Express 4にはいくつかの大きな変更点があります。

<ul class="doclist">
  <li><a href="#core-changes">Express core システムとミドルウェアシステムに変更しました。</a> Connectと組み込みミドルウェアの依存関係は削除されましたので、自分でミドルウェアを追加する必要があります。
  </li>
  <li><a href="#routing">ルーティングシステムへの変更。</a></li>
  <li><a href="#other-changes">その他の様々な変更。</a></li>
</ul>

こちらもご参照ください:

- [新機能 in 4.x] (https://github.com/expressjs/express/wiki/New-features-in-4.x)
- [Migrating from 3.x to 4.x](https://github.com/expressjs/express/wiki/Migrating-from-3.x-to-4.x)

<h3 id="core-changes">
Express コアおよびミドルウェア・システムの変更
</h3>

Express 4はもうConnectに依存せず、組み込みの
ミドルウェアをコアから削除します。ただし、`express.static`関数は除外します。 This means that
Express is now an independent routing and middleware web framework, and
Express versioning and releases are not affected by middleware updates.

組み込みのミドルウェアがなければ、アプリケーションの実行に必要なすべての
ミドルウェアを明示的に追加する必要があります。 以下の手順に従ってください：

1. モジュールをインストール: `npm install --save <module-name>`
2. アプリでは、次のモジュールを必要とします: `require('module-name')`
3. ドキュメントに従ってモジュールを使用します: `app.use( ... )`

以下の表は、Express 4でのExpress 3ミドルウェアとそのミドルウェアを示しています。

<table class="doctable" border="1">
<tbody><tr><th>■急行3</th><th>■急行4</th></tr>
<tr><td><code>express.bodyParser</code></td>
<td><a href="https://github.com/expressjs/body-parser">body-parser</a> +
<a href="https://github.com/expressjs/multer">multer</a></td></tr>
<tr><td><code>express.compress</code></td>
<td><a href="https://github.com/expressjs/compression">圧縮</a></td></tr>
<tr><td><code>express.cookieSession</code></td>
<td><a href="https://github.com/expressjs/cookie-session">クッキーセッション</a></td></tr>
<tr><td><code>express.cookieParser</code></td>
<td><a href="https://github.com/expressjs/cookie-parser">クッキーパーサ</a></td></tr>
<tr><td><code>express.logger</code></td>
<td><a href="https://github.com/expressjs/morgan">モーガン</a></td></tr>
<tr><td><code>express.session</code></td>
<td><a href="https://github.com/expressjs/session">express-session</a></td></tr>
<tr><td><code>express.favicon</code></td>
<td><a href="https://github.com/expressjs/serve-favicon">サービスファビコン</a></td></tr>
<tr><td><code>express.responseTime</code></td>
<td><a href="https://github.com/expressjs/response-time">応答時間</a></td></tr>
<tr><td><code>express.errorHandler</code></td>
<td><a href="https://github.com/expressjs/errorhandler">errorhandler</a></td></tr>
<tr><td><code>express.methodOverride</code></td>
<td><a href="https://github.com/expressjs/method-override">メソッド-オーバーライド</a></td></tr>
<tr><td><code>express.timeout</code></td>
<td><a href="https://github.com/expressjs/timeout">接続タイムアウト</a></td></tr>
<tr><td><code>express.vhost</code></td>
<td><a href="https://github.com/expressjs/vhost">vhost</a></td></tr>
<tr><td><code>express.csrf</code></td>
<td><a href="https://github.com/expressjs/csurf">csurf</a></td></tr>
<tr><td><code>express.directory</code></td>
<td><a href="https://github.com/expressjs/serve-index">サーブインデックス</a></td></tr>
<tr><td><code>express.static</code></td>
<td><a href="https://github.com/expressjs/serve-static">スタティック</a></td></tr>
</tbody></table>

Express 4 のミドルウェアの完全なリストは、[ここ](https://github.com/senchalabs/connect#middleware)を参照してください。

ほとんどの場合、古いバージョン3のミドルウェアを
のExpress 4に置き換えることができます。 詳細については、
GitHub のモジュールドキュメントを参照してください。

<h4 id="app-use"><code>app.use</code> はパラメータを受け付けます</h4>

バージョン 4 では、変数 parameter を使用して、ミドルウェア関数がロードされるパスを定義できます。 次に、ルートハンドラからパラメータの値を読み込みます。
例:

```js
app.use('/book/:id', (req, res, next) => {
  console.log('ID:', req.params.id)
  next()
})
```

<h3 id="routing">
ルーティングシステム
</h3>

アプリケーションがルーティング・ミドルウェアを暗黙的にロードするようになったため、`router` ミドルウェアに関してミドルウェアがロードされる順序を考慮する必要がなくなりました。

ルートの定義方法は変更されていませんが、ルーティングシステムにはルートの整理に役立つ2つの
新機能があります。

{: .doclist }

- 新しいメソッド `app.route()` は、ルートパスに対してチェーン可能なルートハンドラを作成します。
- モジュール式のマウント可能なルートハンドラを作成するための新しいクラス `express.Router` 。

<h4 id="app-route"><code>app.route()</code> メソッド</h4>

新しい`app.route()`メソッドを使用すると、ルートパスのチェーン可能なルートハンドラ
を作成できます。 パスは単一の場所で指定されているため、モジュラールートを作成することは、冗長性とタイプミスを削減するのに役立ちます。 For more
information about routes, see [`Router()` documentation](/{{ page.lang }}/4x/api.html#router).

以下は、`app.route()`関数を使用して定義されたルートハンドラの例です。

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

<h4 id="express-router"><code>express.Router</code> クラス</h4>

ルートを整理するのに役立つもう一つの機能は、新しいクラス
`express.Router` で、モジュラーマウント可能な
ルートハンドラを作成するために使用できます。 `Router`インスタンスは完全なミドルウェアと
ルーティングシステムです。このため、しばしば"mini-app"と呼ばれます。

次の例では、ルーターをモジュールとして作成し、その中にミドルウェアをロードして、いくつかのルートを定義し、それをメインアプリケーションのパスにマウントします。

例えば、アプリケーション・ディレクトリーに次の内容で `birds.js` というルーター・ファイルを作成します。

```js
var express = require('express')
var router = express.Router()

// middleware specific to this router
router.use((req, res, next) => {
  console.log('Time: ', Date.now())
  next()
})
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
var birds = require('./birds')

// ...

app.use('/birds', birds)
```

これで、アプリケーションは、`/birds` および `/birds/about` のパスに対する要求を処理できるようになり、ルートに固有の `timeLog` ミドルウェアを呼び出します。

<h3 id="other-changes">
その他の変更
</h3>

以下の表は、Express 4の他の重要な変更点を示しています。

<table class="doctable" border="1">
<tbody><tr>
<th>オブジェクト</th>
<th>説明</th>
</tr>
<tr>
<td>Node.js</td>
<td>Express 4 では、Node.js 0.10.x 以降が必要で、
Node.js 0.8.x のサポートを廃止しました。</td>
</tr>
<tr>
<td markdown="1">
`http.createServer()`
</td>
<td markdown="1">
`http`モジュールは、直接動作する必要がない限り、もはや必要ありません(socket.io/SPDY/HTTPS)。 アプリは、
`app.listen()`関数を使用して起動できます。
</td>
</tr>
<tr>
<td markdown="1">
`app.configure()`
</td>
<td markdown="1">
`app.configure()`関数が削除されました。  
`process.env.NODE_ENV` または
`app.get('env')` 関数を使用して環境を検出し、それに応じてアプリを構成します。
</td>
</tr>
<tr>
<td markdown="1">
`json spaces`
</td>
<td markdown="1">
Express 4では、`json spaces` アプリケーションプロパティはデフォルトで無効になっています。
</td>
</tr>
<tr>
<td markdown="1">
`req.accepted()`
</td>
<td markdown="1">
`req.accepts()`、`req.acceptsEncodings()`、
`req.acceptsCharsets()`、および `req.acceptsLanguages()`を使用してください。
</td>
</tr>
<tr>
<td markdown="1">
`res.location()`
</td>
<td markdown="1">
相対URLを解決しなくなりました。
</td>
</tr>
<tr>
<td markdown="1">
`req.params`
</td>
<td markdown="1">
配列; オブジェクトになりました。
</td>
</tr>
<tr>
<td markdown="1">
`res.locals`
</td>
<td markdown="1">
関数であり、現在はオブジェクトです。
</td>
</tr>
<tr>
<td markdown="1">
`res.headerSent`
</td>
<td markdown="1">
`res.headersSent` に変更しました。
</td>
</tr>
<tr>
<td markdown="1">
`app.route`
</td>
<td markdown="1">
`app.mountpath` として利用可能です。
</td>
</tr>
<tr>
<td markdown="1">
`res.on('header')`
</td>
<td markdown="1">
削除しました。
</td>
</tr>
<tr>
<td markdown="1">
`res.charset`
</td>
<td markdown="1">
削除しました。
</td>
</tr>
<tr>
<td markdown="1">
`res.setHeader('Set-Cookie', val)`
</td>
<td markdown="1">
機能は基本的なクッキー値の設定に限定されるようになりました。 機能追加には、
`res.cookie()` を使用します。
</td>
</tr>
</tbody></table>

<h2 id="example-migration">アプリの移行例</h2>

Express 3アプリケーションをExpress 4に移行する例を以下に示します。
関心のあるファイルは `app.js` と `package.json` です。

<h3 id="">
バージョン3アプリ
</h3>

<h4 id=""><code>app.js</code></h4>

次の `app.js` ファイルを含む Express v.3 アプリケーションを考えてみましょう。

```js
var express = require('express')
var routes = require('./routes')
var user = require('./routes/user')
var http = require('http')
var path = require('path')

var app = express()

// all environments
app.set('port', process.env.PORT || 3000)
app.set('views', path.join(__dirname, 'views'))
app.set('view engine', 'pug')
app.use(express.favicon())
app.use(express.logger('dev'))
app.use(express.methodOverride())
app.use(express.session({ secret: 'your secret here' }))
app.use(express.bodyParser())
app.use(app.router)
app.use(express.static(path.join(__dirname, 'public')))

// development only
if (app.get('env') === 'development') {
  app.use(express.errorHandler())
}

app.get('/', routes.index)
app.get('/users', user.list)

http.createServer(app).listen(app.get('port'), () => {
  console.log('Express server listening on port ' + app.get('port'))
})
```

<h4 id=""><code>package.json</code></h4>

付随するバージョン 3 の `package.json` ファイルの内容は次のようになります。

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "3.12.0",
    "pug": "*"
  }
}
```

<h3 id="">
プロセス
</h3>

以下のコマンドを使用して、
Express 4アプリに必要なミドルウェアをインストールし、ExpressとPugを最新の
バージョンにアップデートして移行を開始します。

```bash
$ npm install serve-favicon morgan method-override express-session body-parser multer errorhandler express@latest pug@latest --save
```

`app.js`に以下の変更を加えます。

1. 組み込みの Express ミドルウェア関数 `express.favicon` ,
  `express.logger` , `express.methodOverride` ,
  `express.session` , `express.bodyParser` と
  `express.errorHandler` は、
  `express` オブジェクトでは使用できなくなりました。 代わりの
  を手動でインストールし、アプリにロードする必要があります。

2. `app.router`関数をロードする必要がなくなりました。
  有効なExpress 4アプリオブジェクトではないため、
  `app.use(app.router);` コードを削除します。

3. ミドルウェア関数が正しい順序でロードされていることを確認してください - アプリのルートをロードした後に `errorHandler` をロードします。

<h3 id="">バージョン4アプリ</h3>

<h4 id=""><code>package.json</code></h4>

上記の `npm` コマンドを実行すると、 `package.json` が以下のように更新されます。

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "body-parser": "^1.5.2",
    "errorhandler": "^1.1.1",
    "express": "^4.8.0",
    "express-session": "^1.7.2",
    "pug": "^2.0.0",
    "method-override": "^2.1.2",
    "morgan": "^1.2.2",
    "multer": "^0.1.3",
    "serve-favicon": "^2.0.1"
  }
}
```

<h4 id=""><code>app.js</code></h4>

次に、無効なコードを削除し、必要なミドルウェアをロードし、必要に応じて他の
変更を行います。 `app.js`ファイルは次のようになります。

```js
var http = require('http')
var express = require('express')
var routes = require('./routes')
var user = require('./routes/user')
var path = require('path')

var favicon = require('serve-favicon')
var logger = require('morgan')
var methodOverride = require('method-override')
var session = require('express-session')
var bodyParser = require('body-parser')
var multer = require('multer')
var errorHandler = require('errorhandler')

var app = express()

// all environments
app.set('port', process.env.PORT || 3000)
app.set('views', path.join(__dirname, 'views'))
app.set('view engine', 'pug')
app.use(favicon(path.join(__dirname, '/public/favicon.ico')))
app.use(logger('dev'))
app.use(methodOverride())
app.use(session({
  resave: true,
  saveUninitialized: true,
  secret: 'uwotm8'
}))
app.use(bodyParser.json())
app.use(bodyParser.urlencoded({ extended: true }))
app.use(multer())
app.use(express.static(path.join(__dirname, 'public')))

app.get('/', routes.index)
app.get('/users', user.list)

// error handling middleware should be loaded after the loading the routes
if (app.get('env') === 'development') {
  app.use(errorHandler())
}

var server = http.createServer(app)
server.listen(app.get('port'), () => {
  console.log('Express server listening on port ' + app.get('port'))
})
```

<div class="doc-box doc-info" markdown="1">
`http`モジュール(ソケット)で直接作業する必要がない限り。 o/SPDY/HTTPS)、ロードする必要はありません。アプリは次のように簡単に起動できます。

```js
app.listen(app.get('port'), () => {
  console.log('Express server listening on port ' + app.get('port'))
})
```

</div>

<h3 id="">アプリの実行</h3>

移行処理が完了し、アプリは
エクスプレス4アプリになりました。 確認するには、次のコマンドを使用してアプリを起動します。

```bash
$ node .
```

[http://localhost:3000](http://localhost:3000)
を読み込み、Express 4によってレンダリングされるホームページを参照してください。

<h2 id="app-gen">Express 4アプリジェネレーターへのアップグレード</h2>

Express アプリケーションを生成するためのコマンド・ライン・ツールは引き続き `express` ですが、新規バージョンにアップグレードするには、Express 3 アプリケーション・ジェネレーターをアンインストールしてから、新しい `express-generator` をインストールする必要があります。

<h3 id="">インストール中 </h3>

すでにExpress 3アプリジェネレータがシステムにインストールされている場合、
アンインストールする必要があります。

```bash
$ npm uninstall -g express
```

ファイルとディレクトリ権限の設定に応じて、
`sudo` でこのコマンドを実行する必要があります。

新しいジェネレータをインストールします。

```bash
$ npm install -g express-generator
```

ファイルとディレクトリ権限の設定に応じて、
`sudo` でこのコマンドを実行する必要があります。

システムの `express` コマンドが
Express 4ジェネレータに更新されます。

<h3 id="">アプリジェネレーターの変更 </h3>

コマンドオプションと使用方法は、以下の例外を除き、ほとんど同じままです。

{: .doclist }

- `--sessions` オプションを削除しました。
- `--jshtml` オプションを削除しました。
- [Hogan.js](http://twitter.github.io/hogan.js/) をサポートするための `--hogan` オプションを追加しました。

<h3 id="">例</h3>

Express 4 アプリを作成するには、次のコマンドを実行します。

```bash
$ express app4
```

`app4/app.js` ファイルの内容を見ると、アプリケーションに必要な (`express.static` を除く) すべてのミドルウェア関数が独立したモジュールとしてロードされており、`router` ミドルウェアがアプリケーションに明示的にロードされなくなったことが分かります。

`app.js`ファイルがノードになっていることにも気づくでしょう。 sモジュールは、古いジェネレータによって生成されたスタンドアロンアプリとは対照的に。

依存関係をインストールした後、次のコマンドを使用してアプリを起動します。

```bash
$ npm start
```

`package.json` ファイルで npm start スクリプトを見ると、アプリケーションを開始する実際のコマンドは `node ./bin/www` であることが分かります。これは、Express 3 では `node app.js` でした。

Express 4 ジェネレーターによって生成される `app.js` ファイルが Node.js モジュールになったため、(コードを変更しない限り) アプリケーションとして単独では開始できなくなりました。モジュールを Node.js ファイルにロードして、Node.js ファイルから開始する必要があります。この場合、Node.js ファイルは `./bin/www` です。 モジュールは Node.js ファイル
にロードされ、Node.js ファイルを介して開始する必要があります。 Node.js ファイルは `./bin/www`
です。

Expressアプリの作成やアプリの起動には、`bin`ディレクトリも拡張機能のない`www`
ファイルも必須ではありません。 それらは
発電機による提案ですので、
のニーズに合わせて変更してください。

`www` ディレクトリーを削除して、処理を「Express 3 の方法」で実行するには、`app.js` ファイルの最後にある `module.exports = app;` という行を削除して、その場所に以下のコードを貼り付けます。

```js
app.set('port', process.env.PORT || 3000)

var server = app.listen(app.get('port'), () => {
  debug('Express server listening on port ' + server.address().port)
})
```

`app.js`ファイルの先頭にある`debug`モジュールがロードされていることを確認します。

```js
var debug = require('debug')('app4')
```

次に、 `start": `package.json` ファイル中の "node ./bin/www"` を `"start": "node app.js"` に変更します。

これで `./bin/www` の機能を
`app.js` に戻しました。 これで、`./bin/www` の機能を `app.js` に戻しました。この変更は推奨されるものではありませんが、この演習により、`./bin/www` ファイルの仕組みと、`app.js` ファイルが単独で開始されなくなった理由を理解できます。
