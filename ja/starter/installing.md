---
layout: page
title: Express のインストール
description: プロジェクトディレクトリの設定やnpmとの依存関係の管理など、Node.js 環境で Express.js をインストールする方法を学びます。
menu: starter
lang: en
redirect_from: ""
---

# インストール中

既に [Node.js](https://nodejs.org/) がインストールされていると仮定して、アプリケーションを保持するディレクトリを作成し、作業ディレクトリを作成します。

- [Express 4.x](/{{ page.lang }}/4x/api.html) には Node.js 0.10 以上が必要です。
- [Express 5.x](/{{ page.lang }}/5x/api.html) には Node.js 18 以上が必要です。

```bash
$ mkdir myapp
$ cd myapp
```

`npm init` コマンドを使用して、アプリケーション用の `package.json` ファイルを作成します。
`package.json` がどのように動作するかについては、[npm の package.json handling](https://docs.npmjs.com/files/package.json) を参照してください。

```bash
$ npm init
```

このコマンドを実行すると、アプリケーションの名前やバージョンなど、さまざまなものが表示されます。
今のところ、RETURNを押すと、ほとんどのデフォルトを受け入れることができます。以下の例外があります。

```
entry point: (index.js)
```

`app.js`、またはメインファイルの名前を何でも入力します。 `index.js`にしたい場合は、RETURNを押して、推奨されるデフォルトのファイル名を受け入れます。

次に、Expressを`myapp`ディレクトリにインストールし、依存関係リストに保存します。 例:

```bash
$ npm install express
```

Express を一時的にインストールし、依存関係リストに追加しないでください。

```bash
$ npm install express --no-save
```

<div class="doc-box doc-info" markdown="1">
デフォルトでは、バージョン npm 5.0以降では、 `npm install` はモジュールを `package` の `dependencies` リストに追加します。 son` ファイル; 以前のバージョンの npm では、明示的に `--save` オプションを指定する必要があります。 その後、appディレクトリで`npm install`を実行すると、依存関係リストにモジュールが自動的にインストールされます。
</div>

### [次: Hello World ](/{{ page.lang }}/starter/hello-world.html)