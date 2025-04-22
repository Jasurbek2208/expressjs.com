---
layout: page
title: 快速安全更新
description: 查看最新的 Express.js 安全更新和补丁，包括不同版本的详细易受伤害性列表，以帮助维护安全的应用程序。
menu: advanced
lang: 中
redirect_from: ""
---

# 安全更新

<div class="doc-box doc-notice" markdown="1">
Node.js 脆弱性直接影响Express。 因此，[在 Node.js 易受伤害性上保持监视](https://nodejs.org/en/blog/vulnerability/)，并确保您正在使用最新的稳定版本的 Node.js。
</div>

下面的列表列举了在指定版本更新中固定的快递脆弱性。

{% capture security-policy %}
如果你认为你已经发现了一个安全漏洞，请见
[Security Policy and Procedures] (/{{page.lang}}/resources/contributing.html#security-policies-and-procedures)。
{% endcapture %}

{% include admonitions/note.html content=securitypolicy %}

## 4.x

- 4.21.2
  - 依赖的 "path-to-regexp" 已被更新，以处理一个 [vulnerability](https://github.com/pillarjs/path-to-regexp/security/advisories/GHSA-rhx6-c78j-4q9w)。
- 4.21.1
  - 依赖项 `cookie` 已被更新，以处理一个 [vulnerability](https://github.com/jshttp/cookie/security/advisories/GHSA-pxg6-pf52-xh8x)，如果您使用 `res.cookie` ，它可能会影响您的应用程序。
- 4.20.0
  - 在 `res.redirect` ([advisory](https://github.com/expressjs/express/security/advisories/GHSA-qw6h-vgh9-j6wx), [CVE-2024-43796](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2024-43796))中固定的 XSS 脆弱性。
  - 依赖的 `serve-static` 已被更新，以解决一个 [vulnerability](https://github.com/advisories/GHSA-cm22-4g7w-348p)。
  - 依赖`send`已被更新，以处理一个 [vulnerability](https://github.com/advisories/GHSA-m6fv-jmcg-4jfg)。
  - 依赖的 "path-to-regexp" 已被更新，以处理一个 [vulnerability](https://github.com/pillarjs/path-to-regexp/security/advisories/GHSA-9wv6-86v2-598j)。
  - 依赖的 'body-parser' 已被更新，以添加一个 [vulnerability](https://github.com/advisories/GHSA-qwcr-r2fm-qrc7)，如果您启用了网址，可能会影响您的应用程序。
- 4.19.0, 4.19.1
  - 修复了 `res.location` 和 `res.redirect` ([advisory](https://github.com/expressjs/express/security/advisories/GHSA-rv95-896h-c2vc), [CVE-2024-29041](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2024-29041))。
- 4.17.3
  - 依赖的 `qs` 已被更新，以解决一个 [vulnerability](https://github.com/advisories/GHSA-hrpp-h998-j3pp)。 如果使用以下API，这可能会影响您的应用程序：`req.query`、`req.body`、`req.param`。
- 4.16.0
  - 依赖`转发`已被更新，以处理一个 [vulnerability](https://npmjs.com/advisories/527)。 如果使用了下列API，这可能会影响您的应用程序：`req.host`, `req.hostname`, `req.ip`, `req.ips`, `req.protocol`。
  - 依赖项 `mime` 已被更新，以处理一个 [vulnerability](https://npmjs.com/advisories/535)，但这个问题并不影响Express。
  - The dependency `send` has been updated to provide a protection against a [Node.js 8.5.0 vulnerability](https://nodejs.org/en/blog/vulnerability/september-2017-path-validation/). 这只会影响运行在 Node.js 版本的8.5.0上的 Express。
- 4.15.5
  - 依赖的 `debug` 已被更新，以处理一个 [vulnerability](https://snyk.io/vuln/npm:debug:20170905)，但这个问题不会影响Express。
  - The dependency `fresh` has been updated to address a [vulnerability](https://npmjs.com/advisories/526). 如果使用下列API，则会影响您的应用程序：`expres.static`, `req.fresh`, `res.json`, `res.jsonp`, `res.sendfile`, `res.sendfile`, `res.sendFile`, \`res.sendStatus'。
- 4.15.3
  - 依赖的 'ms' 已被更新，以解决一个 [vulnerability](https://snyk.io/vuln/npm:ms:20170412)。 这可能会影响到您的应用程序，如果在以下API中传递到`maxAge`选项：`express.static`、`res.sendfile`和`res.sendFile`。
- 4.15.2
  - 依赖的 `qs` 已被更新，以处理一个 [vulnerability](https://snyk.io/vuln/npm:qs:20170213)，但这个问题不会影响Express。 更新到4.15.2是一种良好做法，但不需要处理这种脆弱性。
- 4.11.1
  - 修复了 `expres.static`, `res.sendfile` 和 `res.sendFile` 中的 root 路径披露的脆弱性
- 4.10.7
  - 修复了 `expres.static` ([advisory](https://npmjs.com/advisories/35), [CVE-2015-1164](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-1164))中开放的重定向脆弱性。
- 4.8.8
  - 在 `explaw.static` ([advisory](http://npmjs.com/advisories/32) 、 [CVE-2014-6394](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6394)中固定的目录遍历脆弱性。
- 4.8.4
  - Node.js 0.10可以在影响`expres.static`和`res.sendfile`的某些情况下泄露`fd`s。 恶意请求可能导致fd`s泄露，并最终导致`EMFILE\`错误和服务器反应失灵。
- 4.8.0
  - 在查询字符串中具有极高索引的 Sparse 数组可能导致该进程耗尽内存并崩溃服务器。
  - 异常嵌套的查询字符串对象可能会导致进程阻止并使服务器暂时失去响应性。

## 3.x

  <div class="doc-box doc-warn" markdown="1">
  **Express 3.x enD-OF-LIFE and NO LONGER MAINTAINED**

自上次更新以来（2015年8月1日）尚未处理3.x中已知和未知的安全和业绩问题。 强烈建议使用最新版本的Express。

If you are unable to upgrade past 3.x, please consider [Commercial Support Options](/{{ page.lang }}/support#commercial-support-options).

  </div>

- 3.19.1
  - 修复了 `expres.static`, `res.sendfile` 和 `res.sendFile` 中的 root 路径披露的脆弱性
- 3.19.0
  - 修复了 `expres.static` ([advisory](https://npmjs.com/advisories/35), [CVE-2015-1164](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-1164))中开放的重定向脆弱性。
- 3.16.10
  - 在 `expres.static` 中固定的目录遍历脆弱性。
- 3.16.6
  - Node.js 0.10可以在影响`expres.static`和`res.sendfile`的某些情况下泄露`fd`s。 恶意请求可能导致fd`s泄露，并最终导致`EMFILE\`错误和服务器反应失灵。
- 3.16.0
  - 在查询字符串中具有极高索引的 Sparse 数组可能导致该进程耗尽内存并崩溃服务器。
  - 异常嵌套的查询字符串对象可能会导致进程阻止并使服务器暂时失去响应性。
- 3.3.0
  - 一个不受支持的方法的404个响应覆盖尝试可能会被跨地点的脚本攻击。