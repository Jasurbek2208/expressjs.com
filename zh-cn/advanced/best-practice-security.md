---
layout: page
title: 快速生产安全最佳做法
description: 在生产中发现快速应用的关键安全最佳做法，包括使用TLS、输入验证、安全cookies和防止脆弱性。
menu: advanced
lang: 中
redirect_from: ""
---

# 生产最佳做法：安全

## 概览

“生产”一词是指软件生命周期中的阶段，当应用程序或API一般提供给其最终用户或消费者时。 与此相对照，在_“开发”阶段，您仍然在积极编写和测试代码，应用程序不能对外开放。 相应的系统环境分别称为_production_和 _development_environment。

发展和生产环境的建立通常不同，要求也大不相同。 在生产中可能不能接受发展带来的好处。 例如，在开发环境中，您可能需要详细记录调试错误， 而同一行为可能成为生产环境中的一个安全问题。 在发展中，你不需要担心可扩展性、可靠性和性能，而这些问题在生产中变得至关重要。

{% include admonitions/note.html content="If you believe you have discovered a security vulnerability in Express, please see
[Security Policies and Procedures](/en/resources/contributing.html#security-policies-and-procedures).
" %}

用于生产快递应用的安全最佳做法包括：

- [Production Best Practices: Security](#production-best-practices-security)
  - [Overview](#overview)
  - 还请确保您未使用[安全性更新页面](/{{ page.lang }}/advanced/security-updates.html)中列出的任何存在漏洞的 Express 版本。如果在使用，请更新到某个稳定发行版，首选为最新版本。
  - [hsts](https://github.com/helmetjs/hsts) 用于设置 `Strict-Transport-Security` 头，实施安全的服务器连接 (HTTP over SSL/TLS)。
  - [不信任用户输入](#do-not-trust-user-input)
    - [防止打开重定向](#prevent-open-redirects)
  - [hidePoweredBy](https://github.com/helmetjs/hide-powered-by) 用于移除 `X-Powered-By` 头。
  - [Reduce fingerprinting](#reduce-fingerprinting)
  - [安全使用 cookie ](#use-cookies-securely)
    - [不使用默认会话 cookie 名称](#dont-use-the-default-session-cookie-name)
    - [设置 cookie 安全选项](#set-cookie-security-options)
  - [防止使用暴力攻击授权](#prevent-brute-force-attacks-against-authorization)
  - [确保您的依赖是安全的](#ensure-your-dependencies-are-secure)
    - [避免其他已知的脆弱性](#avoid-other-known-vulnerabilities)
  - [Additional considerations](#additional-considerations)

## 不要使用过时或易受伤害的快递版本

快递2.x 和 3.x 不再维持。 这些版本中的安全和性能问题不会被修复。 不要使用它们！ If you haven't moved to version 4, follow the [migration guide](/{{ page.lang }}/guide/migrating-4.html) or consider [Commercial Support Options](/{{ page.lang }}/support#commercial-support-options).

Also ensure you are not using any of the vulnerable Express versions listed on the [Security updates page](/{{ page.lang }}/advanced/security-updates.html). 如果您是的话，请更新到稳定的版本之一，最好是最晚的版本。

## 使用 TLS

如果您的应用处理或传输敏感数据，请使用 [传输图层安全](https://en.wikipedia.org/wiki/Transport_Layer_Security(TLS) 来保护连接和数据。 此技术在将数据从客户端发送到服务器之前加密，从而防止了一些常见（容易）的黑客。 虽然Ajax 和 POST 请求可能并不明显，并且似乎在浏览器中“隐藏”， 他们的网络流量易受[数据包狙击](https://en.wikipedia.org/wiki/Packet_analyzer) 和 [中途人为攻击](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)的伤害。

您可能熟悉安全套接字层(SSL)加密。 [TLS is simply the next progression of SSL](https://msdn.microsoft.com/en-us/library/windows/desktop/aa380515\(v=vs.85\).aspx). 换句话说，如果你以前使用过SSL，请考虑升级到TLS。 一般而言，我们建议Nginx处理TLS。 关于在Nginx 上配置TLS (和其他服务器)的良好参考，请参阅[推荐的服务器配置(Mozilla Wiki)](https://wiki.mozilla.org/Security/Server_Side_TLS#Recommended_Server_Configurations)。

另外，获得免费的 TLS 证书的简单工具是 [我们要加密](https://letsencrypt.org/about/)，一个免费的自动， 由[因特网安全研究组(ISRG)](CA)提供的开放式证书权威(CA)(https://www.abetterinternet.org/)。

## 不信任用户输入

对于网络应用程序来说，最关键的安全要求之一是适当的用户输入验证和处理。 这有多种形式，我们不会在这里涵盖所有这些问题。
最终，验证和正确处理用户输入应用程序所接受的类型的责任是您。

### 防止打开重定向

潜在危险用户输入的一个例子是_open redirect_， 在哪里应用程序接受一个 URL 作为用户输入 (通常在 URL 查询中，例如`? rl=https://示例。 om`) 并使用 `res.redirect` 来设置 `location` 标题和
返回一个 3xx 状态。

应用程序必须验证它支持重定向到传入的URL，以避免将用户发送到恶意链接，如钓鱼网站， 除其他风险外，还有其他风险。

这是使用 "res.redirect" 或 "res.location" 前检查URL的一个例子：

```js
app.use((req, res) => {
  try {
    if (new Url(req.query.url).host !== 'example.com') {
      return res.status(400).end(`Unsupported redirect to host: ${req.query.url}`)
    }
  } catch (e) {
    return res.status(400).end(`Invalid url: ${req.query.url}`)
  }
  res.redirect(req.query.url)
})
```

## 使用头盔

[Helmet][helmet] 可以通过正确设置 HTTP 头来保护您的应用免受一些著名的网页脆弱性。

Helmet 是一个中间件功能，用于设置与安全相关的 HTTP 响应头。 头盔默认设置下列标题：

- `Content-Security-Policy`: 一个强大的允许列表来显示你的页面上可能发生的事件，从而缓解许多攻击
- `跨原产地-Opener-Policy`: 帮助进程隔离你的页面
- “跨源资源政策”：阻止其他人加载您的资源跨源数据
- “原生Agent-Cluster”: 改变过程隔离状态以便是基于原始的
- `Referrer-Policy`: 控制[`Referer`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer) 标题
- `Strict-Transport-Security`: 电话浏览器更喜欢HTTPS
- `X-Content-Type-Options`: avoids [MIME sniffing](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types#mime_sniffing)
- “X-DNS-预取控制”：控制DNS预取”
- `X-Download-Options`：要保存的力量下载 (仅限Internet Explorer)
- `X-Frameworks`: 减少 [Clickjacking](https://en.wikipedia.org/wiki/Clickjacking) 攻击的遗留标题
- `X-Permitted-Cross-Domain-Policies`: Controls cross-domaine behavior for Adobe products, such as Acrobat
- `X-Poed-By`: 关于网页服务器的信息。 已删除，因为它可以用于简单的攻击
- `X-XSS-Protection`: 试图缓解[XSS attack](https://developer.mozilla.org/en-US/docs/Glossary/Cross-site_scripting)但使情况更糟的传统标题, 所以头盔禁用它

每个头可以配置或禁用。 若要阅读更多信息，请前往[其文档网站][helmet]。

像其他模块一样安装头盔：

```bash
$ npm install helmet
```

然后在你的代码中使用它：

```js
// ...

const helmet = require('helmet')
app.use(helmet())

// ...
```

## 减少指纹

它可以帮助提供额外的安全层，以降低攻击者确定服务器使用的软件
的能力。 称为"指纹"
虽然不是一个安全问题，但降低应用程序指纹的能力改善了其总体安全态势。
服务器软件可以通过查询来打印，如何响应特定请求，例如在
中 HTTP 响应头中。

By default, Express sends the `X-Powered-By` response header that you can
disable using the `app.disable()` method:

```js
app.disable('x-powered-by')
```

{% include admonitions/note.html content="禁用 `X-Powered-By header` 并不能阻止一个
复杂的攻击者确定应用程序正在运行Express。 It may
discourage a casual exploit, but there are other ways to determine an app is running
Express." %}

快递也发送自己格式的“404未找到”消息和格式化器错误
响应消息。 这些可以由
[添加您自己找不到的处理程序](/en/starter/faq.html#how-do-i-handle-404-responses)
和
[编写您自己的错误处理程序](/en/guide/error-handling.html#writing-error-handlers):

```js
// last app.use calls right before app.listen():

// custom 404
app.use((req, res, next) => {
  res.status(404).send("Sorry can't find that!")
})

// custom error handler
app.use((err, req, res, next) => {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```

## 安全使用 cookie

为了确认 cookie 不要打开您的应用程序来探索，请不要使用默认会话 cookie 名称并正确设置 cookie 安全选项。

有两个主要的中间件 cookie 会话模块：

- 将`express.session` 内置的 [express-session](https://www.npmjs.com/package/express-session)替换为 Express 3.x。
- 替换`express.cookieSession`为内置的 [cookie-session](https://www.npmjs.com/package/cookie-session)

这两个模块之间的主要区别是它们如何保存 cookie 会话数据。 [express-session](https://www.npmjs.com/package/express-session) 中间件存储服务器上的会话数据；它只在 cookie 中保存会话ID，而不是会话数据。 默认情况下，它使用内存存储，而不是为生产环境设计的。 在生产中，您需要设置一个可扩展的会话存储；查看[兼容会话存储](https://github.com/expressjs/session#compatible-session-stores)的列表。

与此相对照， [cookie-session](https://www.npmjs.com/package/cookie-session) 中间件实现 cookie支持的存储：它将整个会话序列化为 cookie，而不只是一个会话密钥。 只有当会话数据相对较小且易于编码为原始值(而不是对象)时才使用它。 虽然浏览器应该支持每cookie至少4096字节， 为了确保您不超过限制，每个域不超过4093字节的大小。 并意识到 cookie 数据将对客户端可见， 所以，如果有任何理由使它安全或模糊不清，那么`express-session` 可能是一个更好的选择。

### 不要使用默认会话 cookie 名称

使用默认会话 cookie 名称可以打开您的应用程序进行攻击。 提出的安全问题类似于“X-Poed-By”：潜在的攻击者可以用它来指纹服务器并相应地攻击目标。

为了避免这个问题，使用通用的 cookie 名称；例如使用 [express-session](https://www.npmjs.com/package/express-session) 中间码：

```js
const session = require('express-session')
app.set('trust proxy', 1) // trust first proxy
app.use(session({
  secret: 's3Cur3',
  name: 'sessionId'
}))
```

### 设置 cookie 安全选项

设置下面的 cookie 选项以增强安全性：

- `secure` - 确保浏览器只通过 HTTPS 发送 cookie 。
- `httpOnly` - 确保只通过 HTTP(S) 而不是客户端 JavaScript 发送cookie ，以帮助防止跨网站的脚本攻击。
- `domain` - 表示cookie的域名；使用它来比较请求URL的服务器域名。 如果它们匹配，然后检查路径属性。
- `path` - 表示cookie的路径；使用它与请求路径相比较。 如果这个域匹配，然后在请求中发送 cookie 。
- `expires` - 用来设置持久的 cookie 的过期日期。

这是一个使用 [cookie-session](https://www.npmjs.com/package/cookie-session)中间仓库的示例：

```js
const session = require('cookie-session')
const express = require('express')
const app = express()

const expiryDate = new Date(Date.now() + 60 * 60 * 1000) // 1 hour
app.use(session({
  name: 'session',
  keys: ['key1', 'key2'],
  cookie: {
    secure: true,
    httpOnly: true,
    domain: 'example.com',
    path: 'foo/bar',
    expires: expiryDate
  }
}))
```

## 防止违反授权的暴力攻击

确保登录端点受到保护，以使私人数据更加安全。

一种简单而强大的技术是使用两个尺度阻止授权尝试：

1. 相同的用户名和 IP 地址连续尝试失败的次数。
2. 在一段长时间内尝试IP地址失败的次数。 例如，如果IP地址在一天内尝试了100次失败，请阻止此地址。

[rate-limiter-flexible](https://github.com/animir/node-rate-limiter-flexible) 软件包提供了使这种技术更加简单快捷的工具。 您可以找到 [文档中的暴力保护示例](https://github.com/animir/node-rate-limiter-flexible/wiki/Overall-example#login-endpoint-protection)

## 确保您的依赖关系安全

使用 npm 管理您的应用程序依赖关系是强大和方便的。 但您使用的软件包可能包含重要的安全弱点，也可能影响到您的应用程序。 您的应用的安全性仅与依赖中的“最弱链接”一样强大。

从 npm@6 开始，npm 自动审查每个安装请求。 另外，您可以使用 `npm audit` 分析依赖树。

```bash
$ npm audit
```

If you want to stay more secure, consider [Snyk](https://snyk.io/).

Snyk offers both a [command-line tool](https://www.npmjs.com/package/snyk) and a [Github integration](https://snyk.io/docs/github) that checks your application against [Snyk's open source vulnerability database](https://snyk.io/vuln/) for any known vulnerabilities in your dependencies. 安装如下CLI：

```bash
$ npm install -g snyk
$ cd your-app
```

使用此命令测试您的应用程序的易受伤害性：

```bash
$ snyk test
```

### 避免其他已知的脆弱性

留意[节点安全项目](https://npmjs.com/advisories) 或 [Snyk](https://snyk.io/vuln/) 咨询意见，可能会影响您的应用使用的快递或其他模块。 一般而言，这些数据库是关于节点安全知识和工具的极好资源。

Finally, Express apps&mdash;like any other web apps&mdash;can be vulnerable to a variety of web-based attacks. 熟悉已知的 [web vulnerabilities] (https://www.owasp.org/www-project-top-ten/) 并采取预防措施避免他们。

## 其他考虑

以下是出色的 [Node.js 安全检查清单] (https://blog.risingstack.com/node-js-security-checklist/ )的一些进一步建议。 关于这些建议的所有详细信息，请参阅该博客帖子：

- 总是过滤和净化用户输入以防止跨站脚本(XSS)和命令注入攻击。
- 使用参数化查询或准备好的语句来保卫不受SQL注入攻击。
- 使用开源的 [sqlmap](http://sqlmap.org/工具来检测您的应用程序中的 SQL 注入脆弱性。
- 使用 [nmap](https://nmap.org/) 和 [sslyze](https://github.com/nabla-c0d3/sslyze) 工具来测试您的 SSL 密码配置， 密钥、重新谈判以及您的证书的有效性。
- 使用 [safe-regex](https://www.npmjs.com/package/safe-regex) 确保您的正则表达式不会被[正则表达式拒绝服务](https://www.owasp.org/index.php/Regular_expression_Denial_of_Service_-_ReDoS) 攻击。

[helmet]: https://helmetjs.github.io/