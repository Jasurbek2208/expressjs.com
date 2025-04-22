---
layout: page
title: プロキシの背後にあるエクスプレス
description: クライアントの IP アドレスを処理するトラストプロキシ設定を使用するなど、リバース・プロキシの背後で正しく動作するように Express.js アプリケーションを構成する方法を学びます。
menu: guide
lang: en
redirect_from: ""
---

# プロキシの背後にあるエクスプレス

リバースプロキシの背後で Express アプリケーションを実行する場合、Express API の中には予想以外の値が返されるものがあります。 これを調整するために `trust proxy` アプリケーションの設定は、Express API のリバースプロキシによって提供された情報を公開するために使用することができます。 最も一般的な問題は、クライアントのIPアドレスを公開するAPIで、リバースプロキシの内部IPアドレスが表示される可能性があります。

<div class="doc-box doc-info" markdown="1">
`trust proxy` の設定では、リバースプロキシの正確な設定を理解することが重要です。 この設定はリクエストで提供された値を信頼するためです Express での設定の組み合わせは、リバースプロキシの動作と一致することが重要です。
</div>

`trust proxy`を設定するアプリケーションは、次の表に示されている値のいずれかを設定することができます。

<table class="doctable" border="1" markdown="1">
  <thead><tr><th>タイプ</th><th>値</th></tr></thead>
  <tbody>
    <tr>
      <td>Boolean</td>
<td markdown="1">
`true` の場合、クライアントの IP アドレスは、 `X-Forwarded-For` ヘッダーの一番左のエントリとして理解されます。

`false` の場合、アプリはクライアントに直接向いていると理解され、クライアントの IP アドレスは `req.socket.remoteAddress` に由来します。 これはデフォルトの設定です。

<div class="doc-box doc-warn" markdown="1">
When setting to `true`, it is important to ensure that the last reverse proxy trusted is removing/overwriting all of the following HTTP headers: `X-Forwarded-For`, `X-Forwarded-Host`, and `X-Forwarded-Proto`, otherwise it may be possible for the client to provide any value.
</div>
</td>
    </tr>
    <tr>
      <td>IP addresses</td>
<td markdown="1">
An IP address, subnet, or an array of IP addresses and subnets to trust as being a reverse proxy. The following list shows the pre-configured subnet names:

- loopback - `127.0.0.1/8`, `::1/128`
- linklocal - `169.254.0.0/16`, `fe80::/10`
- uniqueloc - `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, `fc00::/7`

IPアドレスは以下のいずれかの方法で設定できます。

```js
app.set('trust proxy', 'loopback') // specify a single subnet
app.set('trust proxy', 'loopback, 123.123.123.123') // specify a subnet and an address
app.set('trust proxy', 'loopback, linklocal, uniquelocal') // specify multiple subnets as CSV
app.set('trust proxy', ['loopback', 'linklocal', 'uniquelocal']) // specify multiple subnets as an array
```

指定された場合、IPアドレスまたはサブネットはアドレス決定プロセスから除外されます。 アプリケーションサーバーに最も近い信頼できないIPアドレスは、クライアントのIPアドレスとして決定されます。 これは `req.socket.remoteAddress` が信頼されているかどうかをチェックすることで動作します。 その場合、`X-Forwarded-For`内の各アドレスは、最初の信頼されていないアドレスまで右から左にチェックされます。

</td>
    </tr>
    <tr>
      <td>数値</td>
<td markdown="1">
Expressアプリケーションから離れたホップの最大数のアドレスを使用してください。 `req.socket.remoteAddress` は最初のホップで、残りは右から左への `X-Forwarded-For` ヘッダで探します。 `0`の値は、最初に信頼されていないアドレスが`req.socket.remoteAddress`であることを意味します。つまり、リバースプロキシは存在しません。

<div class="doc-box doc-warn" markdown="1">
When using this setting, it is important to ensure there are not multiple, different-length paths to the Express application such that the client can be less than the configured number of hops away, otherwise it may be possible for the client to provide any value.
</div>
</td>
    </tr>
    <tr>
      <td>Function</td>
<td markdown="1">
Custom trust implementation.

```js
app.set('trust proxy', (ip) => {
  if (ip === '127.0.0.1' || ip === '123.123.123.123') return true // trusted IPs
  else return false
})
```

</td>
    </tr>
  </tbody>
</table>

`trust proxy` を有効にすると、次のような影響を与えます。

<ul>
  <li markdown="1">[req.hostname](/{{ page.lang }}/api.html#req.hostname) の値は、クライアントまたはプロキシーが設定できる `X-Forwarded-Host` ヘッダーに設定された値から導き出されます。</li>
  <li markdown="1">`X-Forwarded-Proto`はリバースプロキシによって設定することで、アプリがhttps`かhttp`か無効な名前かをアプリに伝えることができます。 この値は [req.protocol](/{{ page.lang }}/api.html#req.protocol) に反映されます。
  </li>
  <li markdown="1">[req.ip](/{{ page.lang }}/api.html#req.ip) および [req.ips](/{{ page.lang }}/api.html#req.ips) の値は、`X-Forwarded-For` のアドレス・リストから取り込まれます。</li>
</ul>

`trust proxy` は、 [proxy-addr](https://www.npmjs.com/package/proxy-addr) パッケージを使用して実装されています。 詳細については、そのドキュメントを参照してください。
