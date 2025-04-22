---
layout: page
title: 基本的なルーティング
description: Express.jsアプリケーションでルーティングの基礎を学びます。ルートの定義、HTTPメソッドの処理、Webサーバーのルートハンドラの作成などです。
menu: starter
lang: en
redirect_from: ""
---

# 基本ルーティング

_Routing_ は、アプリケーションが特定のエンドポイントに対してどのように応答するかを決定することを指します。 これはURI(またはパス)と特定のHTTPリクエストメソッド(GET、POSTなど)です。

各ルートは、ルートが一致したときに実行される、1つまたは複数のハンドラ関数を持つことができます。

ルート定義は以下の構造をとります:

```js
app.METHOD(PATH, HANDLER)
```

場所:

- `app` は `express` のインスタンスです。
- `METHOD` は [HTTP リクエストメソッド](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods) の小文字です。
- `PATH` はサーバー上のパスです。
- `HANDLER` はルートが一致したときに実行される関数です。

<div class="doc-box doc-notice" markdown="1">
このチュートリアルでは、`app` という名前の `express` インスタンスが作成され、サーバーが動作していることを前提としています。 
このチュートリアルでは、`app` という名前の `express` のインスタンスが作成されていて、サーバーが稼働中であることを想定しています。アプリケーションの作成と開始に慣れていない場合は、[Hello World の例](/{{ page.lang }}/starter/hello-world.html) を参照してください。

</div>

以下の例は、単純なルートの定義を示しています。

ホームページの「Hello World!」に返信:

```js
app.get('/', (req, res) => {
  res.send('Hello World!')
})
```

ルートルート (`/`) の POST リクエストに応答します。アプリケーションのホームページ:

```js
app.post('/', (req, res) => {
  res.send('Got a POST request')
})
```

`/user`ルートにPUTリクエストに応答します：

```js
app.put('/user', (req, res) => {
  res.send('Got a PUT request at /user')
})
```

`/user`ルートへのDELETEリクエストに対応:

```js
app.delete('/user', (req, res) => {
  res.send('Got a DELETE request at /user')
})
```

ルーティングについて詳しくは、[ルーティング・ガイド](/{{ page.lang }}/guide/routing.html)を参照してください。

### [Previous: Express application generator](/{{ page.lang }}/starter/generator.html)&nbsp;&nbsp;&nbsp;&nbsp;[次へ: Express で静的ファイルを提供する](/{{ page.lang }}/starter/static-files.html)