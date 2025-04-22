---
layout: page
title: エクスプレスユーティリティ
description: Express.jsとNode.jsに関連するユーティリティモジュール、Cookie、CSRF保護、URLの解析、ルーティングなど、アプリケーションを強化するためのツールを含む。
menu: resources
lang: en
redirect_from: ""
---

## Express ユーティリティ関数

[pillarjs](https://github.com/pillarjs) GitHub Organization には、一般的に便利なユーティリティ関数用の多くのモジュール
が含まれています。

| ユーティリティモジュール                                                   | 説明                                                                                                                                                                           |
| -------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [cookies](https://www.npmjs.com/package/cookies)               | HTTP(S) Cookie を取得して設定し、改ざんを防ぐために署名できます。Keygrip を使用します。 Node.js HTTP ライブラリまたは Express ミドルウェアとして使用できます。                                    |
| [csrf](https://www.npmjs.com/package/csrf)                     | CSRFトークンの作成と検証の背後にあるロジックが含まれています。  このモジュールを使用して、カスタム CSRF ミドルウェアを作成します。                                                                                                      |
| [finalhandler](https://www.npmjs.com/package/finalhandler)     | HTTP リクエストに応答するための最後のステップとして呼び出す関数。                                                                                                                                          |
| [parseurl](https://www.npmjs.com/package/parseurl)             | URLをキャッシュで解析します。                                                                                                                                                             |
| [path-match](https://www.npmjs.com/package/path-match)         | [path-to-regexp](https://github.com/component/path-to-regexp) の周りの薄いラッパーは、パラメータ名の抽出を容易にします。                                                                                  |
| [path-to-regexp](https://www.npmjs.com/package/path-to-regexp) | \`\`/user/:name\`のようなExpressスタイルのパス文字列を正規表現に変換します。                                                                                                           |
| [resolve-path](https://www.npmjs.com/package/resolve-path)     | 検証されたルートパスに対して相対パスを解決します。                                                                                                                                                    |
| [router](https://www.npmjs.com/package/router)                 | シンプルなミドルウェアスタイルのルータ。                                                                                                                                                         |
| [routington](https://www.npmjs.com/package/routington)         | URLを定義しマッチングするためのTri-based URLルータ。                                                                                                                                           |
| [send](https://www.npmjs.com/package/send)                     | HTTP レスポンスとしてファイルをストリーミングするためのライブラリで、部分的な応答 (範囲)、条件付きの GET ネゴシエーション、および細かいイベントをサポートします。                                                                   |
| [templation](https://www.npmjs.com/package/templation)         | [co-views](https://github.com/visionmedia/co-views) や [consolidate.js](https://github.com/visionmedia/consolidate.js/) に触発された `res.render()` と同様のシステムを表示します。 |

低レベルの HTTP 関連モジュールについては、 [jshttp](http://jshttp.github.io/) を参照してください。
