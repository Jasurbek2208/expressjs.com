---
layout: page
title: 代理服务器后面的快照
description: 学习如何配置 Express.js 应用程序，在逆向代理后面正确工作，包括使用信任代理设置来处理客户端 IP 地址。
menu: guide
lang: 中
redirect_from: ""
---

# 代理服务器后面的快照

当在逆向代理后运行快递应用程序时，一些Express API可能会返回不同的值。 为了对此作出调整， “信任代理”应用程序设置可以用于泄露逆代理在Express API中提供的信息。 最常见的问题是暴露客户端的 IP 地址的快递API，反向代理的内部IP地址。

<div class="doc-box doc-info" markdown="1">
在配置 `trust proxy` 时，重要的是了解反向代理的确切设置。 因为这个设置将信任请求中提供的值。 Express中设置的组合必须与逆向代理的运作方式相匹配。
</div>

设置`trust proxy`的应用程序可以设置为下表列出的值之一。

<table class="doctable" border="1" markdown="1">
  <thead><tr><th>类型</th><th>值</th></tr></thead>
  <tbody>
    <tr>
      <td>Boolean</td>
<td markdown="1">
如果`true`，客户端的 IP 地址被理解为`X-转发-For` 标题中最左边的条目。

如果`false`，应用程序被理解为直接对应客户端，客户端的 IP 地址来自`req.socket.remoteAddress`。 这是默认设置。

<div class="doc-box doc-warn" markdown="1">
设置为 `true`时，, 重要的是确保最后一个逆向代理信任是移除/覆盖所有下列HTTP头： `X-Forwarded-For` ， `X-转发-主机'和`X-转发-Proto`，否则客户可能提供任何价值。
</div>
</td>
    </tr>
    <tr>
      <td>IP addresses</td>
<td markdown="1">
An IP address, subnet, or an array of IP addresses and subnets to trust as being a reverse proxy. The following list shows the pre-configured subnet names:

- 循环 - `127.0.0.1/8`, `:1/128`
- linklocal - `169.254.0.0/16`, `fe80:/10`
- 独特elocal - `0.0.0.0.0/8`, `172.16.0.0.0/12`, `192.168.0.0/16`, `fc00:/7`

您可以通过以下任何方式设置IP地址：

```js
app.set('trust proxy', 'loopback') // specify a single subnet
app.set('trust proxy', 'loopback, 123.123.123.123') // specify a subnet and an address
app.set('trust proxy', 'loopback, linklocal, uniquelocal') // specify multiple subnets as CSV
app.set('trust proxy', ['loopback', 'linklocal', 'uniquelocal']) // specify multiple subnets as an array
```

如果指定, IP地址或子网将被排除在地址确定过程之外。 和应用程序服务器最近的不信任的 IP 地址被确定为客户端的 IP 地址。 通过检查 `req.socket.remoteAddress` 是否是可信的来实现这一点。 如果是的话，那么`X-Forwarded-For`中的每个地址都会从右到左检查，直到第一个非信任地址。

</td>
    </tr>
    <tr>
      <td>号码</td>
<td markdown="1">
使用距离快递应用程序最多`n`的地址。 `req.socket.remoteAddress`是第一条路径，其余的是从右到左的 `X-Forwarded-For`。 `0`的值意味着第一个不信任的地址将是 `req.socket.remoteAddress`，即没有反向代理。

<div class="doc-box doc-warn" markdown="1">
在使用此设置时，重要的是确保它不是多重的 与快递应用程序不同的长度路径，客户端可以少于配置的挂断数， 否则客户可能会提供任何价值。
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

启用 "信任代理" 将产生以下影响:

<ul>
  <li markdown="1">[req.hostname](/{{ page.lang }}/api.html#req.hostname) 的值派生自 `X-Forwarded-Host` 头中设置的值（可以由客户机或代理设置此值）。
  </li>
  <li markdown="1">`X-Forwarded-Proto` 可以由反向代理设置来告诉应用它是 `https://` 或 `http` ，甚至是无效的名称。 This value is reflected by [req.protocol](/{{ page.lang }}/api.html#req.protocol).
  </li>
  <li markdown="1">[req.ip](/{{ page.lang }}/api.html#req.ip) 和 [req.ips](/{{ page.lang }}/api.html#req.ips) 值由 `X-Forwarded-For` 的地址列表填充。
  </li>
</ul>

使用 [proxy-addr](https://www.npmjs.com/package/proxy-addr软件包实现了 "信任代理" 设置。 欲了解更多信息，请查阅其文件。
