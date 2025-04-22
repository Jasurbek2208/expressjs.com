---
layout: page
title: Express 5に移行
description: Express.jsアプリケーションをバージョン4からバージョン5に移行するための包括的なガイドで、破壊的な変更、非推奨のメソッド、および新たな改善が詳しく説明されています。
menu: guide
lang: en
redirect_from: ""
---

# Express 5に移動中

<h2 id="overview">概要</h2>

エクスプレス5はエクスプレス4と大きく異なりません。 同じ基本APIを維持していますが、以前のバージョンとの互換性を破る変更はまだあります。 したがって、Express 5を使用するように更新すると、Express 4で構築されたアプリケーションが動作しない可能性があります。

このバージョンをインストールするには、Node.js バージョン 18 以上が必要です。 次に、アプリケーションディレクトリで次のコマンドを実行します。

```sh
npm install "express@5"
```

その後、自動テストを実行して何が失敗するかを確認し、以下に示すアップデートに従って問題を解決することができます。 テストに失敗した後、どのエラーが発生したかを確認するためにアプリケーションを実行します。 サポートされていないメソッドやプロパティを使用している場合は、すぐに確認できます。

## Express 5 Codemods

エクスプレスサーバーを移行するのに役立ちます。 コードを自動的に最新バージョンの Express に更新するコードを作成しました。

使用可能なすべてのコードを実行するには、次のコマンドを実行します。

```sh
npx @expressjs/codemod upgrade
```

特定のコードを実行したい場合は、次のコマンドを実行できます。

```sh
npx @expressjs/codemod name-of-the-codemod
```

利用可能なコードリスト [here](https://github.com/expressjs/codemod?tab=readme-ov-file#available-codemods) があります。

<h2 id="changes">Express 5の変更</h2>

**メソッドとプロパティを削除**

<ul class="doclist">
  <li><a href="#app.del">app.del()</a></li>
  <li><a href="#app.param">app.param(fn)</a></li>
  <li><a href="#plural">複数化メソッド名</a></li>
  <li><a href="#leading">名前引数でコロンを先頭に付けるapp.param(name, fn)</a></li>
  <li><a href="#req.param">req.param(name)</a></li>
  <li><a href="#res.json">res.json(obj, status)</a></li>
  <li><a href="#res.jsonp">res.jsonp(obj, status)</a></li>
  <li><a href="#magic-redirect">res.redirect('back') and res.location('back')</a></li>  
  <li><a href="#res.redirect">res.redirect(url, status)</a></li>
  <li><a href="#res.send.body">res.send(body, status)</a></li>
  <li><a href="#res.send.status">res.send(status)</a></li>
  <li><a href="#res.sendfile">res.sendfile()</a></li>
  <li><a href="#express.static.mime">express.static.mime</a></li>
  <li><a href="#express:router-debug-logs">express:routerデバッグログ</a></li>
</ul>

**変更**

<ul class="doclist">
  <li><a href="#path-syntax">パスルート一致シンタックス</a></li>
  <li><a href="#rejected-promises">ミドルウェアとハンドラーから取り扱われる拒否された約束</a></li>
  <li><a href="#express.urlencoded">express.urlencoded</a></li>
  <li><a href="#app.listen">app.listen</a></li>
  <li><a href="#app.router">app.router</a></li>
  <li><a href="#req.body">req.body</a></li>
  <li><a href="#req.host">req.host</a></li>
  <li><a href="#req.query">req.query</a></li>
  <li><a href="#res.clearCookie">res.clearCookie</a></li>
  <li><a href="#res.status">res.status</a></li>
  <li><a href="#res.vary">res.variety</a></li>
</ul>

**改善**

<ul class="doclist">
  <li><a href="#res.render">res.render()</a></li>
  <li><a href="#brotli-support">Brotliエンコーディングサポート</a></li>
</ul>

### 削除されたメソッドとプロパティ

これらのメソッドやプロパティをアプリケーションで使用すると、クラッシュします。 したがって、バージョン5にアップデートした後、アプリを変更する必要があります。

<h4 id="app.del">app.del()</h4>

Express 5では、`app.del()`関数がサポートされなくなりました。 この関数を使うと、エラーがスローされます。 HTTP DELETEルートを登録するには、代わりに`app.delete()`関数を使用します。

`delete`はJavaScriptで予約されているキーワードであるため、最初は`delete`の代わりに`del`が使用されていました。 しかし、ECMAScript 6 では、 `delete` などの予約キーワードをプロパティ名として使用することができます。

{% capture codemod-deprecated-signatures %}
非推奨の署名を以下のコマンドで置き換えることができます:

```plain-text
npx @expressjs/codemod v4-deprecated-signatures
```

{% endcapture %}

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.del('/user/:id', (req, res) => {
  res.send(`DELETE /user/${req.params.id}`)
})

// v5
app.delete('/user/:id', (req, res) => {
  res.send(`DELETE /user/${req.params.id}`)
})
```

<h4 id="app.param">app.param(fn)</h4>

`app.param(fn)`署名は、`app.param(name, fn)`関数の動作を変更するために使用されました。 v4.11.0以降非推奨となり、Express 5では全くサポートされなくなりました。

<h4 id="plural">複数化されたメソッド名</h4>

以下のメソッド名が複数化されています。 Express 4 では、古いメソッドを使用すると非推奨になりました。 Express 5ではサポートされていません：

`req.acceptsCharset()`は`req.acceptsCharsets()`に置き換えられます。

`req.acceptsEncoding()`は`req.acceptsEncodings()`に置き換えられます。

`req.acceptsLanguage()`は`req.acceptsLanguages()`に置き換えられました。

{% capture codemod-pluralized-methods %}
非推奨の署名を以下のコマンドで置き換えることができます:

```plain-text
npx @expressjs/codemod pluralized-methods
```

{% endcapture %}

{% include admonitions/note.html content=codemod-pluralized-methods %}

```js
// v4
app.all('/', (req, res) => {
  req.acceptsCharset('utf-8')
  req.acceptsEncoding('br')
  req.acceptsLanguage('en')

  // ...
})

// v5
app.all('/', (req, res) => {
  req.acceptsCharsets('utf-8')
  req.acceptsEncodings('br')
  req.acceptsLanguages('en')

  // ...
})
```

<h4 id="leading">app.param(name, fn) の名前の先頭コロン (:)</h4>

\`appの名前の先頭にあるコロン文字 (:) です。 aram(name, fn)関数はExpress 3の名残であり、後方互換性のため、Express 4は廃止予定の通知でサポートしています。 Express 5は黙って無視し、コロンをつけずに名前パラメータを使用します。

Express 4 の [app.param](/{{ page.lang }}/4x/api) のドキュメントに従っている場合、これはあなたのコードには影響しません。 tml#app.param)、主要なコロンの言及はありません。

<h4 id="req.param">req.param(name)</h4>

これは、潜在的に混乱し、フォームデータを取得する危険な方法が削除されました。 ここで、`req.params`、`req.body`、または`req.query`オブジェクトの中で、送信されたパラメータ名を具体的に探す必要があります。

{% capture codemod-req-param %}
非推奨の署名を以下のコマンドで置き換えることができます:

```plain-text
npx @expressjs/codemod req-param
```

{% endcapture %}

{% include admonitions/note.html content=codemod-req-param %}

```js
// v4
app.post('/user', (req, res) => {
  const id = req.param('id')
  const body = req.param('body')
  const query = req.param('query')

  // ...
})

// v5
app.post('/user', (req, res) => {
  const id = req.params.id
  const body = req.body
  const query = req.query

  // ...
})
```

<h4 id="res.json">res.json(obj, status)</h4>

Express 5 では署名 `res.json(obj, status)` がサポートされなくなりました。 代わりに、ステータスを設定し、 `res.json()` メソッドに次のようにチェーンさせます。`res.status(status).json(obj)` 。

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.post('/user', (req, res) => {
  res.json({ name: 'Ruben' }, 201)
})

// v5
app.post('/user', (req, res) => {
  res.status(201).json({ name: 'Ruben' })
})
```

<h4 id="res.jsonp">res.jsonp(obj, status)</h4>

Express 5 では署名 `res.jsonp(obj, status)` がサポートされなくなりました。 代わりに、ステータスを設定し、 `res.jsonp()` メソッドを次のようにチェーンします。`res.status(status).jsonp(obj)` 。

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.post('/user', (req, res) => {
  res.jsonp({ name: 'Ruben' }, 201)
})

// v5
app.post('/user', (req, res) => {
  res.status(201).jsonp({ name: 'Ruben' })
})
```

<h4 id="res.redirect">res.redirect(url, status)</h4>

Express 5 は、シグニチャー `res.redirect(url, status)` をサポートしなくなりました。代わりに、状況を設定してから、`res.status(status).json(obj)` のように `res.json()` メソッドにチェーニングします。 代わりに、`res.redirect(status, url)` という署名を使用します。

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.get('/user', (req, res) => {
  res.redirect('/users', 301)
})

// v5
app.get('/user', (req, res) => {
  res.redirect(301, '/users')
})
```

<h4 id="magic-redirect">res.redirect('back') と res.location('back')</h4>

Express 5では、`res.redirect()`と`res.location()`メソッドの魔法文字列`back`がサポートされなくなりました。 代わりに、 `req.get('Referrer') |'/'`の値を使用して前のページにリダイレクトします。 Express 4 では、res.`redirect('back')` と `res.location('back')` メソッドは廃止されました。

{% capture codemod-magic-redirect %}
非推奨の署名を以下のコマンドで置き換えることができます:

```plain-text
npx @expressjs/codemod magic-redirect
```

{% endcapture %}

{% include admonitions/note.html content=codemod-magic-redirect %}

```js
// v4
app.get('/user', (req, res) => {
  res.redirect('back')
})

// v5
app.get('/user', (req, res) => {
  res.redirect(req.get('Referrer') || '/')
})
```

<h4 id="res.send.body">res.send(body, status)</h4>

Express 5 では署名 `res.send(obj, status)` がサポートされなくなりました。 代わりに、ステータスを設定し、 `res.status(status).send(obj)` のように、 `res.send()` メソッドを連鎖させます。

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.get('/user', (req, res) => {
  res.send({ name: 'Ruben' }, 200)
})

// v5
app.get('/user', (req, res) => {
  res.status(200).send({ name: 'Ruben' })
})
```

<h4 id="res.send.status">res.send(status</h4>

Express 5では、`status` が数値である署名 `res.send(status)` がサポートされなくなりました。 代わりに、 `res を使ってください。 endStatus(statusCode)` 関数は、HTTP レスポンスヘッダーのステータスコードを設定し、コードのテキストバージョンを送信します。 "Not Found", "Internal Server Error"など。
\`res を使って数字を送る必要がある場合。 end()関数は、数字を文字列に変換するために引用符で囲みます Expressはサポートされていない古い署名を使用しようとしないようにします。

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.get('/user', (req, res) => {
  res.send(200)
})

// v5
app.get('/user', (req, res) => {
  res.sendStatus(200)
})
```

<h4 id="res.sendfile">res.sendfile()</h4>

`res.sendfile()`関数は、Express 5でキャメルケースのバージョン`res.sendFile()`に置き換えられました。

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.get('/user', (req, res) => {
  res.sendfile('/path/to/file')
})

// v5
app.get('/user', (req, res) => {
  res.sendFile('/path/to/file')
})
```

<h4 id="express.static.mime">express.static.mime</h4>

Express 5 では、`mime` は `static` フィールドのエクスポートされたプロパティではなくなりました。
MIME タイプの値を扱うには、[`mime-types` package](https://github.com/jshttp/mime-types) を使用します。

```js
// v4
express.static.mime.lookup('json')

// v5
const mime = require('mime-types')
mime.lookup('json')
```

<h4 id="express:router-debug-logs">express:routerデバッグログ</h4>

Express 5では、ルータの処理ロジックは依存関係によって実行されます。 したがって、ルーターの
デバッグログは、`express::` 名前空間で使用できなくなります。
v4 では、`express:router` 、 `express:router:layer` 、
および `express:router:route` の下でログを利用できました。 これらはすべて `express:*` という名前空間の下に含まれています。
v5.1以降では、ログは名前空間`router`、`router:layer`、および`router:route`の下で利用できます。
`router:layer` と `router:route` のログは、名前空間の `router:*` に含まれています。
v4 で `express:*` を使用してデバッグログの詳細を達成するには、
`express:*` 、 `router`、 `router:*` を使用します。

```sh
# v4
DEBUG=express:* node index.js

# v5
DEBUG=express:*,router,router:* node index.js
```

<h3>変更済み</h3>

<h4 id="path-syntax">パス経路一致の構文</h4>

パスルートマッチング構文は、文字列が`app.all()`、`app.use()`、`app.METHOD()`、`router.all()`、`router.METHOD()`、`router.METHOD()`、`router.METHOD()`、`router.use()` APIに最初のパラメータとして与えられた場合です。 パス文字列が受信リクエストと一致する方法を次のように変更しました:

- ワイルドカード`*`には名前が必要です。パラメータ`:`の動作に一致します。`/*`の代わりに`/*splat`を使用します。

```js
// v4
app.get('/*', async (req, res) => {
  res.send('ok')
})

// v5
app.get('/*splat', async (req, res) => {
  res.send('ok')
})
```

{% capture note_wildcard %}
`*spat` はルートパスのない任意のパスにマッチします。 `/`と同様にルートパスをマッチさせる必要がある場合は、 `/{*spat}`を使用し、ワイルドカードを括弧で囲みます。

```js
// v5
app.get('/{*splat}', async (req, res) => {
  res.send('ok')
})
```

{% endcapture %}
{% include admonitions/note.html content=note_wildcard %}

- オプションの文字 `?` はサポートされなくなりました。代わりに括弧を使用してください。

```js
// v4
app.get('/:file.:ext?', async (req, res) => {
  res.send('ok')
})

// v5
app.get('/:file{.:ext}', async (req, res) => {
  res.send('ok')
})
```

- 正規表現文字はサポートされていません。 例:

```js
app.get('/[discussion|page]/:slug', async (req, res) => {
  res.status(200).send('ok')
})
```

次に変更する必要があります：

```js
app.get(['/discussion/:slug', '/page/:slug'], async (req, res) => {
  res.status(200).send('ok')
})
```

- いくつかの文字はアップグレード中に混乱を避けるために予約されています (`()[]?+!`), それらをエスケープするために`\`を使用します。
- パラメータ名が有効な JavaScript 識別子をサポートするようになりました。また、`:"this"` のように引用符で囲まれました。

<h4 id="rejected-promises">ミドルウェアとハンドラーから取り扱われる拒否された約束。</h4>

rejected promiseを返すリクエストミドルウェアとハンドラは、「Error」として拒否された値をエラー処理ミドルウェアに転送することで処理されるようになりました。 つまり、 `async` 関数をミドルウェアとして、ハンドラを使うのはこれまで以上に簡単です。 `async` 関数でエラーがスローされるか、拒否された Promise が async 関数内で `await`ed になります。 これらのエラーは、`next(err)`を呼び出すかのようにエラーハンドラに渡されます。

Express でのエラー処理の詳細については、[Error handling documentation](/en/guide/error-handling.html)を参照してください。

<h4 id="express.urlencoded">express.urlencoded</h4>

`express.urlencoded` メソッドはデフォルトで `extended` オプション `false` を設定します。

<h4 id="app.listen">app.listen</h4>

Express 5 では、サーバーがエラーイベントを受信したときに `app.listen` メソッドがユーザーが提供するコールバック関数を呼び出します。 Express 4では、そのようなエラーがスローされます。 この変更により、エラー処理の責任が Express 5 のコールバック関数に移行されます。 エラーがある場合は、コールバックに引数として渡されます。
例:

```js
const server = app.listen(8080, '0.0.0.0', (error) => {
  if (error) {
    throw error // e.g. EADDRINUSE
  }
  console.log(`Listening on ${JSON.stringify(server.address())}`)
})
```

<h4 id="app.router">app.router</h4>

Express 4 で削除された `app.router` オブジェクトは、Express 5 で復活しました。 新しいバージョンでは、このオブジェクトはベース Express ルータへの単なる参照です。 アプリが明示的にロードしなければならなかったExpress 3とは異なります。

<h4 id="req.body">req.body</h4> 

`req.body` プロパティは、本文が解析されていない場合に `undefined` を返します。 Express 4 ではデフォルトで `{}` を返します。

<h4 id="req.host">req.host</h4>

Express 4では、`req.host`関数がポート番号を間違って剥奪しました。 Express 5ではポート番号が維持されています。

<h4 id="req.query">req.query</h4>

`req.query` プロパティはもはや書き込み可能なプロパティではなく、代わりにゲッターです。 デフォルトのクエリパーサが"extended"から"simple"に変更されました。

<h4 id="res.clearCookie">res.clearCookie</h4>

`res.clearCookie`メソッドは、ユーザーが提供する`maxAge`と`expires`オプションを無視します。

<h4 id="res.status">res.status</h4>

`res.status` メソッドは、Node によって定義された動作に従い、`100` から `999` の範囲の整数のみを受け付けます。 s, そしてステータスコードが整数でない場合にエラーを返します。

<h4 id="res.query">res.variable</h4>

`field`引数がない場合、`res.vary`はエラーをスローします。 Express 4では、引数が省略された場合、コンソールに警告が表示されました。

### 改善

<h4 id="res.render">res.render()</h4>

このメソッドは、すべてのビューエンジンの非同期動作を強制するようになりました。 同期実装されたビューエンジンによるバグを回避し、推奨されるインターフェイスに違反していました。

<h4 id="brotli-support">Brotliエンコーディングのサポート</h4>

Express 5では、サポートしているクライアントから受信したリクエストに対応するBrotliエンコーディングに対応しています。
