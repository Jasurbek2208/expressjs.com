---
layout: page
title: 调试快照
description: 学习如何在 Express.js 应用程序中启用和使用调试日志，方法是设置 DEBUG 环境变量来增强疑难解答。
menu: guide
lang: 中
redirect_from: ""
---

# 调试快照

要看到所有内部日志在Express中使用，请将`DEBUG`环境变量设置为
`express:*` 。

```bash
$ DEBUG=express:* node index.js
```

在 Windows 上，使用相应的命令。

```bash
> $env:DEBUG = "express:*"; node index.js
```

在 [Express 生成器](/{{ page.lang }}/starter/generator.html)所生成的缺省应用程序上运行此命令将显示以下输出：

```bash
$ DEBUG=express:* node ./bin/www
  express:router:route new / +0ms
  express:router:layer new / +1ms
  express:router:route get / +1ms
  express:router:layer new / +0ms
  express:router:route new / +1ms
  express:router:layer new / +0ms
  express:router:route get / +0ms
  express:router:layer new / +0ms
  express:application compile etag weak +1ms
  express:application compile query parser extended +0ms
  express:application compile trust proxy false +0ms
  express:application booting in development mode +1ms
  express:router use / query +0ms
  express:router:layer new / +0ms
  express:router use / expressInit +0ms
  express:router:layer new / +0ms
  express:router use / favicon +1ms
  express:router:layer new / +0ms
  express:router use / logger +0ms
  express:router:layer new / +0ms
  express:router use / jsonParser +0ms
  express:router:layer new / +1ms
  express:router use / urlencodedParser +0ms
  express:router:layer new / +0ms
  express:router use / cookieParser +0ms
  express:router:layer new / +0ms
  express:router use / stylus +90ms
  express:router:layer new / +0ms
  express:router use / serveStatic +0ms
  express:router:layer new / +0ms
  express:router use / router +0ms
  express:router:layer new / +1ms
  express:router use /users router +0ms
  express:router:layer new /users +0ms
  express:router use / &amp;lt;anonymous&amp;gt; +0ms
  express:router:layer new / +0ms
  express:router use / &amp;lt;anonymous&amp;gt; +0ms
  express:router:layer new / +0ms
  express:router use / &amp;lt;anonymous&amp;gt; +0ms
  express:router:layer new / +0ms
```

当向应用程序提出请求时，您将看到在快递代码中指定的日志：

```bash
  express:router dispatching GET / +4h
  express:router query  : / +2ms
  express:router expressInit  : / +0ms
  express:router favicon  : / +0ms
  express:router logger  : / +1ms
  express:router jsonParser  : / +0ms
  express:router urlencodedParser  : / +1ms
  express:router cookieParser  : / +0ms
  express:router stylus  : / +0ms
  express:router serveStatic  : / +2ms
  express:router router  : / +2ms
  express:router dispatching GET / +1ms
  express:view lookup "index.pug" +338ms
  express:view stat "/projects/example/views/index.pug" +0ms
  express:view render "/projects/example/views/index.pug" +1ms
```

要看到仅来自路由器实现的日志，请将 `DEBUG` 的值设置为 `express:router` 。 同样，只看到应用程序执行中的日志，将`DEBUG`设置为 `express:application` ，等等。

## “明确”产生的应用程序

一个 `express` 命令生成的应用程序使用了 `debug` 模块，其调试命名空间的范围被扩展到应用程序的名称。

例如，如果你用`$ expressed sample-app`生成应用程序，你可以通过以下命令启用调试语句：

```bash
$ DEBUG=sample-app:* node ./bin/www
```

您可以通过分配逗号分隔的名称列表来指定多个调试命名空间：

```bash
$ DEBUG=http,mail,express:* node index.js
```

## 高级选项

当运行到 Node.js时，您可以设置几个环境变量来改变调试日志的行为：

| 名称                  | 目的                             |
| ------------------- | ------------------------------ |
| `DEBUG`             | 启用/禁用特定调试命名空间. |
| `DEBUG_COLORS`      | 是否在调试输出中使用颜色。                  |
| `DEBUG_DEPTH`       | 对象检查深度。                        |
| `DEBUG_FD`          | 要写入调试输出的文件描述符。                 |
| `DEBUG_SHOW_HIDDEN` | 在检查对象上显示隐藏属性。                  |

{% include admontions/note tml content="以 `DEBUG_` 开头的环境变量最终为
转换成一个选项对象，它会被使用 `%o`/`%O`格式.
See the Node.js documentation for
[`util.inspect()`](https://nodejs.org/api/util.html#util_util_inspect_object_options)
for the complete list." %}
