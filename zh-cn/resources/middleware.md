---
layout: middleware
title: 快递中间件
description: 探索一个 Express 团队和社区维护的 Express.js 中间件模块列表，包括内置的中间件和受欢迎的第三方模块。
menu: resources
lang: 中
redirect_from: ""
module: mw-home
---

## 快递中间件

The Express middleware modules listed here are maintained by the
[Expressjs team](https://github.com/orgs/expressjs/people).

| 中间件模块                                                                       | 描述                                                                                         |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| [body-parser](/{{page.lang}}/resources/middleware/body-parser.html)         | 解析 HTTP 请求正文。                                                                              |
| [compression](/{{page.lang}}/resources/middleware/compression.html)         | 压缩HTTP响应。                                                                                  |
| [connect-rid](/{{page.lang}}/resources/middleware/connect-rid.html)         | 生成唯一的请求 ID。                                                                                |
| [cookie-parser](/{{page.lang}}/resources/middleware/cookie-parser.html)     | 解析 cookie 头并使用 "req.cookies" 另见 [cookies](https://github.com/jed/cookies)。 |
| [cookie-session](/{{page.lang}}/resources/middleware/cookie-session.html)   | 建立基于 cookie 的会话。                                                                           |
| [cors](/{{page.lang}}/resources/middleware/cors.html)                       | 启用具有各种选项的跨源资源共享 (CORS)。                                                 |
| [errorhandler](/{{page.lang}}/resources/middleware/errorhandler.html)       | 开发错误处理/调试错误。                                                                               |
| [method-override](/{{page.lang}}/resources/middleware/method-override.html) | 使用标题覆盖 HTTP 方法。                                                                            |
| [morgan](/{{page.lang}}/resources/middleware/morgan.html)                   | HTTP 请求日志记录器。                                                                              |
| [multer](/{{page.lang}}/resources/middleware/multer.html)                   | 处理多部分格式数据。                                                                                 |
| [response-time](/{{page.lang}}/resources/middleware/response-time.html)     | 记录 HTTP 响应时间。                                                                              |
| [serve-favicon](/{{page.lang}}/resources/middleware/serve-favicon.html)     | 提供一个收藏夹。                                                                                   |
| [serve-index](/{{page.lang}}/resources/middleware/serve-index.html)         | 提供给定路径的目录列表。                                                                               |
| [serve-static](/{{page.lang}}/resources/middleware/serve-static.html)       | 服务静态文件。                                                                                    |
| [session](/{{page.lang}}/resources/middleware/session.html)                 | 建立基于服务器的会议(仅开发)。                                                        |
| [timeout](/{{page.lang}}/resources/middleware/timeout.html)                 | 设置超时的 perioHTTP 请求处理。                                                                      |
| [vhost](/{{page.lang}}/resources/middleware/vhost.html)                     | 创建虚拟域名。                                                                                    |

## 额外的中间件模块

这些是一些其他受欢迎的中间件模块。

{% include community-caveat.html %}

| 中间件模块                                               | 描述                                                                                                |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| [helmet](https://github.com/helmetjs/helmet)        | 通过设置各种HTTP头来帮助安全您的应用。                                                                             |
| [passport](https://github.com/jaredhanson/passport) | 使用 OAuth 、 OpenID 等“策略”进行身份验证。  更多信息请见 [passportjs.org](https://passportjs.org/)。 |
