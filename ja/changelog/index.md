---
layout: page
title: エクスプレスの更新履歴
description: Express.jsのリリースchangelog、新機能、バグ修正、バージョン間での重要な変更の詳細を更新してください。
lang: en
sitemap: false
redirect_from:
  - ""
  - ""
---

<nav aria-label="sidebar-heading">
  <div class="toc-container">
    <h3 id="sidebar-heading" class="toc-heading"><em>バージョン</em></h3><button id="menu-toggle" title="show express versions">バージョン <span>►</span></button>
    <ul id="menu">
      {% capture readme %}{% include changelog/menu.md %}{% endcapture %}
      <li>
        {{ readme | markdownify }}
      </li>
    </ul>
  </div>
</nav>

<div markdown="1" id="page-doc">

# 更新履歴をリリース

すべての最新のアップデート、改善、およびExpress への修正

## Express v5

{: id="5.x"}

### 5.1.0 - リリース日: 2025-03-31

{: id="5.0.1"}

5.1.0マイナーリリースにはいくつかの新機能と改善点が含まれています。

- Uint8Array としてレスポンスを送信するサポート
- `res.sendFile()` にETag オプションのサポートを追加しました
- `res.links()`で同じrelで複数のリンクを追加する機能を追加しました
- パフォーマンス: ループを使用して acceptParams
- [body-parser@2.2.0](https://github.com/expressjs/body-parser/releases/tag/v2.2.0)
  - 従来のnode.jsのサポートはBrotliと`AsyncLocalStorage`のチェックを削除します
  - `unpipe` & `destroy` を削除
- [router@2.2.0](https://github.com/pillarjs/router/releases/tag/v2.2.0)
  - Restore `debug`. `express` の代わりに `router` スコープを使用します。
  - 従来のnode.jsサポートの`setImmediate`のチェックを削除します
  - 非ネイティブの Promise サポートを非推奨にする
  - `after`、`safe-buffer`、`array-flatten`、`setprototypeof`、`methods`、`utils-merge`を削除します
- [finalhandler@2.1.0](https://github.com/pillarjs/finalhandler/releases/tag/v2.1.0)
  - 従来のnode.jsサポートは`headersSent`、`setImmediate`、およびhttp2のサポートをチェックします。
  - `unpipe`を削除します
- ロックされたバージョンの代わりに`^`範囲を使用するために、残りのすべての依存関係を切り替えました
- package.json の資金調達フィールドを追加して、OpenCollectiveをハイライトします
- [Changelog v5.1.0](https://github.com/expressjs/express/releases/tag/v5.1.0) を参照してください。

### 5.0.1 - リリース日: 2024-10-08

{: id="5.0.1"}

5.0.1 パッチリリースには 1 つのセキュリティ修正が含まれています:

- [jshttps/cookie](https://www.npmjs.com/package/cookie) を更新して、 [vulnerability](https://github.com/advisories/GHSA-pxg6-pf52-xh8x) をアドレス指定します。

### 5.0.0 - リリース日: 2024-09-09

{: id="5.0.0"}

Check the [migration guide](/{{page.lang}}/guide/migrating-5.html) with all the changes in this new version of Express.

## Express v4

{: id="4.x"}

### 4.21.2 - リリース日: 2024-11-06

{: id="4.21.2"}

4.21.2パッチリリースには、1つのセキュリティ修正が含まれています。

- [pillajs/path-to-regexp](https://www.npmjs.com/package/path-to-regexp) を更新して、 [vulnerability](https://github.com/advisories/GHSA-rhx6-c78j-4q9w) をアドレス指定します。

### 4.21.1 - リリース日: 2024-10-08

{: id="4.21.1"}

4.21.1 パッチリリースには 1 つのセキュリティ修正が含まれています。

- [jshttps/cookie](https://www.npmjs.com/package/cookie) を更新して、 [vulnerability](https://github.com/advisories/GHSA-pxg6-pf52-xh8x) をアドレス指定します。

### 4.21.0 - リリース日: 2024-09-11

{: id="4.21.0"}

4.21.0マイナーリリースには、以下の新機能が含まれています。

- `res.location("back")` と `res.redirect("back")` マジック文字列

### 4.20.0 - リリース日: 2024-09-10

{: id="4.20.0"}

4.20.0 マイナーリリースには、以下を含むいくつかの新機能が含まれています。

- [`res.clearCookie()`メソッド](/{{ page.lang }}/4x/api.html#res.clearCookie) は、 `options.maxAge` と `options.expires` オプションを廃止します。
- [`res.redirect()`メソッド](/{{ page.lang }}/4x/api.html#res.redirect) はHTMLリンクレンダリングを削除します。
- [`express.urlencoded()`メソッド](/{{ page.lang }}/4x/api.html#express.urlencoded) メソッドは、以前は `Infinity` の深さレベルを持つようになりました。
- 正規表現を使用してルートに名前付きのマッチンググループのサポートを追加
- `\`、`|`、`^`のエンコーディングを削除し、URL仕様に合わせて整列します。

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4200--2024-09-10) を参照してください。

### 4.19.2 - リリース日: 2024-03-25

{: id="4.19.2"}

- リダイレクトを許可するオープンリダイレクトの改善された修正

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4192--2024-03-25) を参照してください。

### 4.19.1 - 発売日: 2024-03-20

{: id="4.19.1"}

- 新しいエンコーディング処理のチェックで文字列以外を res.location に渡すことを許可する

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4191--2024-03-20) を参照してください。

### 4.19.0 - リリース日:2024-03-20

{: id="4.19.0"}

- エンコードURLのためにリストバイパスを許可するオープンリダイレクトを防止する
- deps: cookie@0.6.0

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4190--2024-03-20) を参照してください。

### 4.18.3 - 発売日:2024-02-29

{: id="4.18.3"}

4.18.3 パッチリリースには、以下のバグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  メソッドのないルーティング要求を修正しました。 ([commit](https://github.com/expressjs/express/commit/74beeac0718c928b4ba249aba3652c52fbe32ca8))  
</li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4183--2024-02-26) を参照してください。

### 4.18.2 - リリース日: 2022-10-08

{: id="4.18.2"}

4.18.2 パッチリリースには、以下のバグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  単一のルートで大きなスタックの回帰ルーティングを修正しました。 ([commit](https://github.com/expressjs/express/commit/7ec5dd2b3c5e7379f68086dae72859f5573c8b9b))  
</li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4182--2022-10-08) を参照してください。

### 4.18.1 - リリース日: 2022-04-29

{: id="4.18.1"}

4.18.1 パッチリリースには、以下のバグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  Fix the condition where if an Express application is created with a very large stack of routes, and all of those routes are sync (call `next()` synchronously), then the request processing may hang.
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4181--2022-04-29) を参照してください。

### 4.18.0 - リリース日: 2022-04-25

{: id="4.18.0"}

4.18.0 マイナーリリースには、バグ修正といくつかの新機能が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  [`app.get()` method](/{{ page.lang }}/4x/api.html#app.get) と[`app.set()` method](/{{ page.lang }}/4x/api.html#app.set) が設定値を取得すると、`Object.prototype` のプロパティを直接無視するようになりました。
  </li>

  <li markdown="1" class="changelog-item">
  [`res.cookie()`メソッド](/{{ page.lang }}/4x/api.html#res.cookie) がSet-CookieレスポンスヘッダーにPriority属性を設定する「priority」オプションを受け付けるようになりました。
  </li>

  <li markdown="1" class="changelog-item">
  [`res.cookie()`メソッド](/{{ page.lang }}/4x/api.html#res.cookie) が無効な日付オブジェクトを"expires"オプションとして提供するようになりました。
  </li>

  <li markdown="1" class="changelog-item">
  [`res.cookie()` メソッド](/{{ page.lang }}/4x/api.html#res.cookie) が "maxAge" 引数として明示的に指定されている場合に動作するようになりました。
  </li>

  <li markdown="1" class="changelog-item">
  このバージョンから、Express は Node.js 18.x をサポートします。
  </li>

  <li markdown="1" class="changelog-item">
  [`res.download()`メソッド](/{{ page.lang }}/4x/api.html#res.download) は[`res.sendFile()`](/{{ page.lang }}/4x/api.html#res.sendFile)に一致する"root"オプションを受け付けるようになりました。
  </li>

  <li markdown="1" class="changelog-item">
  The [`res.download()` method](/{{ page.lang }}/4x/api.html#res.download) can be supplied with an `options` object without providing a `filename` argument, simplifying calls when the default `filename` is desired.
  </li>

  <li markdown="1" class="changelog-item">
  [`res.format()`メソッド](/{{ page.lang }}/4x/api.html#res.format)が、与えられた「デフォルト」ハンドラーを型ハンドラー(`req`、`res`、および`next`)と同じ引数で起動するようになりました。
  </li>

  <li markdown="1" class="changelog-item">
  [`res.send()`メソッド](/{{ page.lang }}/4x/api.html#res.send) はレスポンスコードが205に設定されている場合、レスポンスボディを送信しようとしません。
  </li>

  <li markdown="1" class="changelog-item">
  デフォルトのエラーハンドラは、以前に設定されていた場合、エラーレスポンスのレンダリングを壊す特定のレスポンスヘッダーを削除します。
  </li>

  <li markdown="1" class="changelog-item">
  ステータスコード425は、「無秩序なコレクション」ではなく「早すぎる」として表されるようになりました。
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4180--2022-04-25) を参照してください。

### 4.17.3 - リリース日: 2022-02-16

{: id="4.17.3"}

4.17.3 パッチリリースには 1 つのバグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  Update to [qs module](https://www.npmjs.com/package/qs) for a fix around parsing `__proto__` properties.
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4173--2022-02-16) を参照してください。

### 4.17.2 - リリース日: 2021-12-16

{: id="4.17.2"}

4.17.2 パッチリリースには、以下のバグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  コールバックが指定された場合の `res.jsonp` の `undefined` の処理を修正しました。
  </li>

  <li markdown="1" class="changelog-item">
  `"json escape"`が有効になっている場合、`res.json`と`res.jsonp`の`undefined`の処理を修正しました。
  </li>

  <li markdown="1" class="changelog-item">
  無効な値の扱いを`res.cookie()`の`maxAge`オプションに修正しました。
  </li>

  <li markdown="1" class="changelog-item">
  非推奨の `req.connection` 上で `req.socket` を使用するには、[jshttp/proxy-addr module](https://www.npmjs.com/package/proxy-addr) に更新します。
  </li>

  <li markdown="1" class="changelog-item">
  このバージョンから、Express は Node.js 14.x をサポートします。
  </li>

</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4172--2021-12-16) を参照してください。

### 4.17.1 - リリース日: 2019-05-25

{: id="4.17.1"}

4.17.1 パッチリリースには 1 つのバグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  既存の Express 4 アプリケーションでリグレッションを発生させるため、`res.status()` API への変更が取り消されました。
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4171--2019-05-25) を参照してください。

### 4.17.0 - リリース日: 2019-05-16

{: id="4.17.0"}

4.17.0 マイナーリリースには、バグ修正といくつかの新機能が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  リクエストペイロードのリクエスト本文解析を提供するために、`express.raw()` と `express.text()` ミドルウェアが追加されました。 下の[expressjs/body-parser module](https://www.npmjs.com/package/body-parser) モジュールを使用するため、モジュールを個別に必要としているアプリは組み込みパーサに切り替えることができます。
  </li>

  <li markdown="1" class="changelog-item">
  `res.cookie()` API は `sameSite` オプションの `none"`値をサポートしました。
  </li>

  <li markdown="1" class="changelog-item">
  `"trust proxy"`設定が有効になっている場合、`req.hostname`はリクエストに複数の`X-Forwarded-For`ヘッダーをサポートするようになりました。
  </li>

  <li markdown="1" class="changelog-item">
  このバージョンから、Express は Node.js 10.x および 12.x をサポートします。
  </li>

  <li markdown="1" class="changelog-item">
  `res.sendFile()` API は、文字列でないものが `path` 引数として渡されたときに、より迅速かつ容易にエラーを理解できるようになりました。
  </li>

  <li markdown="1" class="changelog-item">
  引数として `null` または `undefined` を渡すと、`res.status()` API がより迅速かつ理解しやすくなりました。
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4170--2019-05-16) を参照してください。

### 4.16.4 - リリース日: 2018-10-10

{: id="4.16.4"}

4.16.4 パッチリリースには、さまざまなバグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  `Request aborted"`が`res.sendfile`にログインされる問題を修正しました。
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4164--2018-10-10) を参照してください。

### 4.16.3 - リリース日: 2018-03-12

{: id="4.16.3"}

4.16.3 パッチリリースには、さまざまなバグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  Fix issue where a plain `%` at the end of the url in the `res.location` method or the `res.redirect` method would not get encoded as `%25`.
  </li>

  <li markdown="1" class="changelog-item">
  空白の `req.url` がデフォルトの 404 処理中にスローされる問題を修正しました。
  </li>

  <li markdown="1" class="changelog-item">
  Fix the generated HTML document for `express.static` redirect responses to properly include `</html>`.
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4163--2018-03-12) を参照してください。

### 4.16.2 - リリース日: 2017-10-09

{: id="4.16.2"}

4.16.2 パッチリリースには、回帰バグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  Fix a `TypeError` that can occur in the `res.send` method when a `Buffer` is passed to `res.send` and the `ETag` header is already set on the response.
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4162--2017-10-09) を参照してください。

### 4.16.1 - リリース日: 2017-09-29

{: id="4.16.1"}

4.16.1 パッチリリースには、回帰バグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  `express.static` の特定のユーザーに影響を与えるエッジケースの回帰を修正するために、[pillarjs/send module](https://www.npmjs.com/package/send) に更新します。
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4161--2017-09-29) を参照してください。

### 4.16.0 - リリース日: 2017-09-28

{: id="4.16.0"}

4.16.0マイナーリリースには、セキュリティの更新、バグ修正、パフォーマンスの向上、およびいくつかの新機能が含まれます。

<ul>
  <li markdown="1" class="changelog-item">
  [jshttp/forwarded module](https://www.npmjs.com/package/forwarded) に更新して、 [vulnerability](https://npmjs.com/advisories/527 ) をアドレス指定します。 以下の API が使用されている場合、アプリケーションに影響を与える可能性があります: `req.host` 、 `req.hostname` 、 `req.ips` 、 `req.protocol` 。
  </li>

  <li markdown="1" class="changelog-item">
  [pillarjs/send module](https://www.npmjs.com/package/send) の依存関係を更新して、`mime` 依存関係の [vulnerability](https://npmjs.com/advisories/535) をアドレス指定します。 信頼されていない文字列が次の API に渡されると、アプリケーションに影響を与える可能性があります: `res.type()` 。
  </li>

  <li markdown="1" class="changelog-item">
  [pillarjs/send module](https://www.npmjs.com/package/send) は Node.js 8.5.0 [vulnerability](https://nodejs.org/en/blog/vulnerability/september-2017-path-validation/ ) に対する保護を実装しました。 Express を Node.js 8.5.0 (特定の Node.js バージョン)で使用すると、次の API が脆弱になります。`express.static` 、 `res.sendfile` 、および `res.sendFile` 。
  </li>

  <li markdown="1" class="changelog-item">
  このバージョンから、Express は Node.js 8.x をサポートします。
  </li>

  <li markdown="1" class="changelog-item">
  新しい設定 `"json escape"`を有効にすると、`res.json()`、`res.json()`、`res.json()`で文字をエスケープすることができます。 `Content-Type` を尊重する代わりに、クライアントがレスポンスをHTMLとして検出するようにするためのレスポンスend()です。 これにより、Express アプリケーションを永続的な XSS ベースの攻撃のクラスから保護するのに役立ちます。
  </li>

  <li markdown="1" class="changelog-item">
  [`res.download()`メソッド](/{{ page.lang }}/4x/api.html#res.download) オプションの `options` オブジェクトを受け付けるようになりました。
  </li>

  <li markdown="1" class="changelog-item">
  リクエストボディの解析をすぐにサポートするために、`express.json()` と `express.urlencoded()` ミドルウェアが追加されました。 下の[expressjs/body-parser module](https://www.npmjs.com/package/body-parser) モジュールを使用するため、モジュールを個別に必要としているアプリは組み込みパーサに切り替えることができます。
  </li>

  <li markdown="1" class="changelog-item">
  [`express.static()` ミドルウェア](/{{ page.lang }}/4x/api.html#express.static) および [`res.sendFile()` method](/{{ page.lang }}/4x/api.html#res.sendFile) `Cache-Control` ヘッダーに `immutable` ディレクティブの設定をサポートするようになりました。 適切な `maxAge` でこのヘッダーを設定すると、サポートされているウェブブラウザがファイルがキャッシュにあるときにサーバーにリクエストを送るのを防ぎます。
  </li>

  <li markdown="1" class="changelog-item">
  [pillarjs/send module](https://www.npmjs.com/package/send) には MIME タイプの更新リストがあり、より多くのファイルの `Content-Type` を設定します。 ファイル拡張子には70種類の新しいタイプがあります。
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4160--2017-09-28) を参照してください。

### 4.15.5 - リリース日: 2017-09-24

{: id="4.15.5"}

4.15.5 パッチリリースには、セキュリティ更新、いくつかのマイナーなパフォーマンス強化、バグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  Update to [debug module](https://www.npmjs.com/package/debug) to address a [vulnerability](https://snyk.io/vuln/npm:debug:20170905), but this issue does not impact Express.
  </li>

  <li markdown="1" class="changelog-item">
  [jshttp/freshモジュール](https://www.npmjs.com/package/fresh) に更新して、 [vulnerability](https://npmjs.com/advisories/526 ) に対応します。 `express.static` 、 `req.fresh` 、 `res.json` 、 `res.json` 、 `res.send` 、 `res.send` 、 `res.sendFile` 、 `res.sendFile` 、 `res.sendStatus` などのAPIが使用されると、アプリケーションに影響します。
  </li>

  <li markdown="1" class="changelog-item">
  [jshttp/freshmodule](https://www.npmjs.com/package/fresh) に更新された変更されたヘッダの処理を無効な日付で修正し、条件付きヘッダ(If-None-Match`のような)の解析を高速化します。
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4155--2017-09-24) を参照してください。

### 4.15.4 - リリース日: 2017-08-06

{: id="4.15.4"}

4.15.4 パッチリリースには、いくつかのマイナーなバグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  特定の条件下で操作されている `"proxyを信頼する"`に設定されている配列を修正しました。
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4154--2017-08-06) を参照してください。

### 4.15.3 - リリース日: 2017-05-16

{: id="4.15.3"}

4.15.3 パッチリリースには、セキュリティアップデートといくつかのマイナーなバグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  [pillarjs/send module](https://www.npmjs.com/package/send) の依存関係を更新して、 [vulnerability](https://snyk.io/vuln/npm:ms:20170412 ) をアドレス指定します。 信頼されていない文字列が次の API で `maxAge` オプションに渡されると、アプリケーションに影響を与える可能性があります。`express.static` 、 `res.sendfile` 、 `res.sendFile` です。
  </li>

  <li markdown="1" class="changelog-item">
  `res.set` が `Content-Type` にcharset を追加できない場合のエラーを修正しました。
  </li>

  <li markdown="1" class="changelog-item">
  HTMLドキュメントの欠落している`</html>`を修正しました。
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4153--2017-05-16) を参照してください。

### 4.15.2 - リリース日: 2017-03-06

{: id="4.15.2"}

4.15.2 パッチリリースには、マイナーなバグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  拡張(デフォルト)クエリパーサの `[` で始まる回帰解析キーを修正しました。
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4152--2017-03-06) を参照してください。

### 4.15.1 - リリース日: 2017-03-05

{: id="4.15.1"}

4.15.1 パッチリリースには、マイナーなバグ修正が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  Fix compatibility issue when using the datejs 1.x library where the [`express.static()` middleware](/{{ page.lang }}/4x/api.html#express.static) and [`res.sendFile()` method](/{{ page.lang }}/4x/api.html#res.sendFile) would incorrectly respond with 412 Precondition Failed.
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4151--2017-03-05) を参照してください。

### 4.15.0 - リリース日: 2017-03-01

{: id="4.15.0"}

4.15.0 マイナーリリースには、バグ修正、パフォーマンス改善、およびその他のマイナーな機能追加が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  このバージョンから、Express は Node.js 7.x をサポートします。
  </li>

  <li markdown="1" class="changelog-item">
  [`express.static()`ミドルウェア](/{{ page.lang }}/4x/api.html#express.static) と [`res.sendFile()`メソッド](/{{ page.lang }}/4x/api.html#res.sendFile) が `If-Match` と `If-Unmodified-Since` リクエストヘッダーをサポートするようになりました。
  </li>

  <li markdown="1" class="changelog-item">
  Update to [jshttp/etag module](https://www.npmjs.com/package/etag) to generate the default ETags for responses which work when Node.js has [FIPS-compliant crypto enabled](https://nodejs.org/dist/latest/docs/api/cli.html#cli_enable_fips).
  </li>

  <li markdown="1" class="changelog-item">
  デフォルトのような様々な自動生成された HTML レスポンスが見つからず、エラーハンドラは完全な HTML 5 ドキュメントと追加のセキュリティヘッダーで応答します。
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4150--2017-03-01) を参照してください。

### 4.14.1 - リリース日: 2017-01-28

{: id="4.14.1"}

4.14.1 パッチリリースには、以下を含むバグ修正とパフォーマンス改善が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  Update to [pillarjs/finalhandler module](https://www.npmjs.com/package/finalhandler) fixes an exception when Express handles an `Error` object which has a `headers` property that is not an object.
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4141--2017-01-28) を参照してください。

### 4.14.0 - リリース日: 2016-06-16

{: id="4.14.0"}

4.14.0 マイナーリリースには、バグ修正、セキュリティアップデート、パフォーマンス改善、その他のマイナーな機能追加が含まれています。

<ul>
  <li markdown="1" class="changelog-item">
  このバージョンから、Express は Node.js 6.x をサポートします。
  </li>

  <li markdown="1" class="changelog-item">
  [jshttp/negotiator module](https://www.npmjs.com/package/negotiator) に更新すると、[正規表現によるサービス妨害の脆弱性](https://npmjs.com/advisories/106)が修正されます。
  </li>

  <li markdown="1" class="changelog-item">
  [`res.sendFile()`メソッド](/{{ page.lang }}/4x/api.html#res.sendFile) で、`acceptRanges` と `cacheControl` の2つの新しいオプションが追加されました。

- `acceptRanges` (deaut は `true`)で、レンジされたリクエストの受け付けを有効または無効にします。 無効にすると、レスポンスは `Accept-Ranges` ヘッダーを送信せず、`Range` リクエストヘッダーの内容を無視します。

- `cacheControl`, (デフォルトは `true`), `Cache-Control` レスポンスヘッダーを有効または無効にします。 無効にすると、 `maxAge` オプションは無視されます。

- `res.sendFile` は `Range` ヘッダーとリダイレクトを処理するために更新されました。

  </li>

  <li markdown="1" class="changelog-item">
  [`res.location()` method](/{{ page.lang }}/4x/api.html#res.location) と [`res.redirect()` method](/{{ page.lang }}/4x/api.html#res.redirect) はエンコードされていない場合、URL文字列をエンコードします。
  </li>

  <li markdown="1" class="changelog-item">
  The performance of the [`res.json()` method](/{{ page.lang }}/4x/api.html#res.json) and [`res.jsonp()` method](/{{ page.lang }}/4x/api.html#res.jsonp) have been improved in the common cases.
  </li>

  <li markdown="1" class="changelog-item">
  The [jshttp/cookie module](https://www.npmjs.com/package/cookie) (in addition to a number of other improvements) has been updated and now the [`res.cookie()` method](/{{ page.lang }}/4x/api.html#res.cookie) supports the `sameSite` option to let you specify the [SameSite cookie attribute](https://tools.ietf.org/html/draft-west-first-party-cookies-07).  

{% include admonitions/note.html content="この属性はまだ完全に標準化されておらず、将来変更される可能性があり、多くのクライアントがそれを無視する可能性があります。 %}

`sameSite` オプションの値は以下のとおりです。

- `true` を使用します。これは `SameSite` 属性を `Strict` に設定し、厳密に同じサイトを強制します。
- `false`。`SameSite` 属性を設定しません。
- `'lax'`, `SameSite` 属性に `Lax` を設定します。
- `strict`` はサイトを厳密に強制するために、 `SameSite`属性に`Strict\` を設定します。

  </li>

  <li markdown="1" class="changelog-item">
  Windows上での絶対パスチェックを修正しました。これは、いくつかのケースで誤っていました。
  </li>

  <li markdown="1" class="changelog-item">
  プロキシ付きIPアドレス解像度が大幅に改善されました。
  </li>

  <li markdown="1" class="changelog-item">
  The [`req.range()` method](/{{ page.lang }}/4x/api.html#req.range) options object now supports a `combine` option (`false` by default), which when `true`, combines overlapping and adjacent ranges and returns them as if they were specified that way in the header.
  </li>
</ul>

このリリースの変更点の完全な一覧については、 [History.md](https://github.com/expressjs/express/blob/master/History.md#4140--2016-06-16) を参照してください。

</div>
