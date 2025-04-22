---
layout: page
title: 生产中使用快递的性能最佳做法
description: 发现快速应用在生产中的性能和可靠性能，涵盖代码优化和环境设置以实现最佳性能。
menu: advanced
lang: 中
redirect_from: ""
---

# 生产最佳做法：绩效和可靠性

本文讨论用于生产的快递应用软件的性能和可靠性最佳做法。

这个专题显然属于跨越传统发展和业务的世界范畴。 因此，资料分为两部分：

- 您的代码中要做的事情(开发部分)：
  - [使用 gzip 压缩](#use-gzip-compression)
  - [不要使用同步函数](#dont-use-synchronous-functions)
  - 正确进行日志记录
  - [正确处理异常](#handle-exceptions-properly)
- 在您的环境/设置中要做的事(应用部分)：
  - 将 NODE_ENV 设置为“production”
  - [确保您的应用自动重新启动](#ensure-your-app-automatically-restarts)
  - [在集群中运行您的应用程序](#run-your-app-in-a-cluster)
  - [缓存请求结果](#cache-request-results)
  - [使用负载平衡器](#use-a-load-balancer)
  - [使用反转代理](#use-a-reverse-proxy)

## 您的代码 {#in-code} 要做的事情。

以下是你可以在你的代码中做的一些事情来改进你的应用程序的性能：

- [使用 gzip 压缩](#use-gzip-compression)
- [不要使用同步函数](#dont-use-synchronous-functions)
- 正确进行日志记录
- [正确处理异常](#handle-exceptions-properly)

### 使用 gzip 压缩

压缩Gzip 可以大大减少响应体的大小，从而提高网页应用的速度。 在您的快递应用程序中使用 [compression](https://www.npmjs.com/package/compression) 中间件来压缩gzip 压缩。 例如：

```js
const compression = require('compression')
const express = require('express')
const app = express()

app.use(compression())
```

高流量制作网站 设置压缩的最佳方式是在反转代理一级执行压缩(见[使用反向代理](#use-a-reverse-proxy))。 在这种情况下，你不需要使用压缩中间件。 关于Nginx启用 gzip 压缩的详情，请查看Ngzip_module(http://nginx.org/en/docs/http/ngx_http_gzip_module.html) Nginx文档。

### 不要使用同步函数

同步函数和方法将执行过程连接起来，直到它们返回。 单次调用到同步函数可能会在几秒或毫秒后返回。 然而，在高流量网站，这些通话增加和降低了应用的性能。 避免在生产中使用它们。

虽然节点和许多模块提供其功能的同步和异步版本，但在生产中总是使用异步版本。 唯一可以证明同步函数正确的时间是初始开始。

您可以使用 `--trace-sync-io` 命令行标志来打印警告和堆栈跟踪，每当您的应用程序使用同步API。 当然，你不想在生产中使用这种方法，而是要确保你的代码已准备就绪供生产。 See the [node command-line options documentation](https://nodejs.org/api/cli.html#cli_trace_sync_io) for more information.

### 正确日志记录

一般来说，从您的应用登录有两个原因：调试和记录应用活动(基本上是其他一切)。 使用 `console.log()` 或者 `console.error()` 将日志消息打印到终端是开发中的常见做法。 但当目的地为终端或文件时，[这些函数是同步的](https://nodejs.org/api/console.html#console)， 这样它们不适合生产，除非你将输出管道到另一个程序。

#### 调试中

如果您登录进行调试，则不使用 `console.log()`，使用特殊调试模块，例如 [debug](https://www.npmjs.com/package/debug)。 此模块允许您使用DEBUG 环境变量来控制哪些调试消息被发送到`console.error()`，如果有的话。 为了保持您的应用纯属异步，您仍然想要将 `console.error()` 管道传输到另一个程序。 但你不是真的要在生产中调试，是吗？

#### 应用活动

如果您正在记录应用活动（例如跟踪流量或 API 调用），而不是使用 "控制台。 og()\`，使用日志库，如 [Pino](https://www.npmjs.com/package/pino)，这是可用的最快和最有效的选项。

### 正确处理异常

节点应用遇到未知异常时崩溃。 不处理异常和采取适当行动将使您的快递应用程序崩溃并离线。 如果您在下面[确保您的应用自动重新启动](#ensure-your-app-automatically-restarts)，那么您的应用将从崩溃中恢复。 幸运的是，快递应用通常有很短的启动时间。 尽管如此，您首先想避免崩溃，要做到这一点，您需要正确处理异常。

为了确保您处理所有异常，使用以下技术：

- [使用 try-catch](#use-try-catch)
- [使用 promise](#promises)

在潜入这些主题之前，您应该对Node/Express错误处理有一个基本的理解：使用错误的首次回调和传播中途传输错误。 节点使用“错误的第一回调”协议来返回异步函数错误。 回调函数的第一个参数是错误对象，接下来的参数是结果数据。 如果没有错误，则以 null 作为第一个参数。 回调函数必须相应遵循错误的第一回调约定才能有意义地处理错误。 在Express中，最佳做法是使用下一个() 函数在中间件链中传播错误。

欲了解更多错误处理的基本要素，请参阅：

- [在 Node.js中处理错误](https://www.tritondatacenter.com/node-js/production/design/errors)

#### 使用尝试性捕获功能

Try-catch 是一个 JavaScript 语言构造，您可以用来在同步代码中捕获异常。 例如使用尝试捕获来处理 JSON 解析错误，如下所示。

下面是一个利用抓取来处理潜在的过程崩溃异常的例子。
这个中间件函数接受一个名为“参数”的查询字段参数，这是一个 JSON 对象。

```js
app.get('/search', (req, res) => {
  // Simulating async operation
  setImmediate(() => {
    const jsonStr = req.query.params
    try {
      const jsonObj = JSON.parse(jsonStr)
      res.send('Success')
    } catch (e) {
      res.status(400).send('Invalid JSON string')
    }
  })
})
```

不过，试捕只适用于同步编码。 由于节点平台主要是异步平台（特别是在生产环境中），试捕不会有许多例外。

#### 使用承诺

当在一个 "async" 函数中出现错误或正在等待一个 "async" 函数中的拒绝承诺时, 这些错误将会传递到错误处理程序中，仿佛调用 "next(err)"

```js
app.get('/', async (req, res, next) => {
  const data = await userData() // If this promise fails, it will automatically call `next(err)` to handle the error.

  res.send(data)
})

app.use((err, req, res, next) => {
  res.status(err.status ?? 500).send({ error: err.message })
})
```

另外，您可以使用异步函数为您的中间件，如果许诺失败，路由器将处理错误，例如：

```js
app.use(async (req, res, next) => {
  req.locals.user = await getUser(req)

  next() // This will be called if the promise does not throw an error.
})
```

最佳做法是尽可能在站点附近处理错误。 因此，虽然现在在路由器中处理， 它最好在中间件中找到错误并处理它，而不依赖于单独处理中间件的错误。

#### 不做什么

你应该做的一件事是聆听`uncaughtException`事件。 当异常气泡回到事件循环时发出。 为`uncaughtException`添加事件侦听器将改变遇到异常的过程的默认行为； 尽管有例外情况，这一进程仍将继续进行。 这可能会很好地防止您的应用崩溃， 但在一个未捕获的异常后继续运行应用程序是一种危险的练习，不推荐。 因为该进程的状况变得不可靠和不可预测。

此外，使用 `uncaughtException` 被正式承认为 [crude](https://nodejs.org/api/process.html#process_event_uncaughtexception)。 因此，聆听`uncaughtException`只是一个坏主意。 这就是为什么我们推荐像多个进程和管理员这样的情况：崩溃和重启往往是从错误中恢复的最可靠的方法。

我们还建议不要使用 [domains](https://nodejs.org/api/domain.html)。 它通常不解决问题，也是一个废弃的模块。

## 在您的环境/设置中要做的事情。

{#in-environment}

以下是您在系统环境中可以做的一些事情，以提高您应用的性能：

- 将 NODE_ENV 设置为“production”
- [确保您的应用自动重新启动](#ensure-your-app-automatically-restarts)
- [在集群中运行您的应用程序](#run-your-app-in-a-cluster)
- [缓存请求结果](#cache-request-results)
- [使用负载平衡器](#use-a-load-balancer)
- [使用反转代理](#use-a-reverse-proxy)

### 将NODE_ENV 设置为“生产”

NODE_ENV 环境变量指定了应用程序运行的环境(通常是开发或生产)。 您可以做的最简单的事情之一是将NODE_ENV设置为“生产”。

设置NODE_ENV 为“production”使得快：

- 缓存视图模板。
- 缓存 CSS 扩展生成的 CSS 文件。
- 生成较少详细的错误信息。

[测试表明](https://www.dynatrace.com/news/blog/the-drastic-effects-of-omitting-node-env-in-your-express-js-applications/)仅仅这样做就可以使应用程序性能提高 3 倍多！

如果你需要写环境代码，你可以用 `process.env.NODE_ENV`检查NODE_ENV\`的值。 意识到检查任何环境变量的价值都会受到业绩的惩罚，因此应当少量地进行。

在开发中，您通常在交互式shell中设置环境变量，例如使用 `export` 或 `.bash_profile` 文件。 但一般而言，你不应该在生产服务器上这样做；相反，你应该使用你的操作系统中的 OSS 内部系统 (systemd)。 下一节提供更多关于使用您内部系统的详细信息。 但设置 `NODE_ENV` 对于性能（并且很容易做）非常重要，这是这里突出强调的。

使用系统，在您的设备文件中使用 `Environment` 指令。 例如：

```sh
# /etc/systemd/system/myservice.service
Environment=NODE_ENV=production
```

有关更多信息，请参阅 [Using Environment Variables In systemd Units](https://www.flatcar.org/docs/latest/setup/systemd/environment-variables/)。

### 确保您的应用自动重启

在生产中，你不想让你的应用程序脱机了。 这意味着你需要确保它在应用程序崩溃时和服务器本身崩溃时重新启动。 尽管你希望这两次事件都不会发生，但现实地说，你必须通过以下方式对这两次事件负责：

- 当应用程序崩溃时使用进程管理器重新启动(和节点)。
- 使用 OS 提供的 init 系统在操作系统崩溃时重启进程管理器。 也可以在没有流程管理器的情况下使用Init系统。

节点应用程序崩溃，如果遇到未知异常。 The foremost thing you need to do is to ensure your app is well-tested and handles all exceptions (see [handle exceptions properly](#handle-exceptions-properly) for details). 但作为一个失败的安全因素，建立了一个机制，以确保如果您的应用崩溃，它将自动重新启动。

#### 使用进程管理器

在开发过程中，您只是从命令行启动了您的应用，和 `节点server.js` 或类似的东西。 但在生产过程中这样做会造成灾难。 如果应用程序崩溃，它将脱机直到您重新启动。 为了确保您的应用在崩溃时重新启动，请使用一个流程管理器。 流程管理器是一个方便部署的应用程序的“容器”，提供了高可用性，并使您能够在运行时管理应用程序。

除了在程序崩溃时重新启动您的应用外，进程管理器可以使您能够：

- 了解运行时的性能和资源消耗情况。
- 动态修改设置以提高性能。
- 控制集群(pm2)。

历史上，使用 Node.js 进程管理器很受欢迎，比如 [PM2](https://github.com/Unitech/pm2)。 如果您想这样做，请查看他们的文档。 然而，我们建议使用您的Init系统进行流程管理。

#### 使用 init 系统

下一层可靠性是为了确保您的应用在服务器重启时重新启动。 出于各种原因，系统仍然可以运转。 为了确保您的应用在服务器崩溃时重新启动，请使用内置系统安装在您的操作系统中。 当前使用的主要内部系统是 [systemd](https://wiki.debian.org/systemd)。

您的快递应用有两种方式使用内嵌系统：

- 在进程管理器中运行您的应用，然后将进程管理器安装为 init 系统的服务。 过程管理器将在应用崩溃时重新启动您的应用，输入系统将在操作系统重新启动时重新启动过程管理器。 这是建议采用的办法。
- 直接使用 init 系统运行您的应用 (和节点)。 这有点简单，但是您无法获得使用流程管理器的额外优势。

##### Systemd

Systemd 是 Linux 系统和服务管理器。 大多数主要的Linux发行版都采用了系统作为它们的默认内部系统。

一个 systemd 服务配置文件叫做一个 _unit file_，文件名以`.service`结尾。 这是一个直接管理节点应用的示例单元文件。 替换你的系统和应用程序的<angle brackets>所包含的值：

```sh
[Unit]
Description=<Awesome Express App>

[Service]
Type=simple
ExecStart=/usr/local/bin/node </projects/myapp/index.js>
WorkingDirectory=</projects/myapp>

User=nobody
Group=nogroup

# Environment variables:
Environment=NODE_ENV=production

# Allow many incoming connections
LimitNOFILE=infinity

# Allow core dumps for debugging
LimitCORE=infinity

StandardInput=null
StandardOutput=syslog
StandardError=syslog
Restart=always

[Install]
WantedBy=multi-user.target
```

关于系统的更多信息，请参阅[systemd reference (man page)](http://www.freedesktop.org/software/systemd/man/systemd.unit.html)。

### 在集群中运行您的应用

在多核心系统中，您可以通过启动集群进程来提高节点应用的性能。 集群运行应用程序的多个实例，最好在每个CPU核心上有一个实例，从而在实例中分配负载和任务。

![Balancing between application instances using the cluster API](/images/clustering.png)

重要: 既然应用程序实例是单独运行过程，它们不共享相同的内存空间。 也就是说，每个应用的对象都是本地的。 因此，您不能在应用程序代码中保留状态。 然而，您可以使用内存数据存储，如 [Redis](http://redis.io/) 来存储与会话相关的数据和状态。 这种告诫基本上适用于所有形式的横向缩放，不管是分组多个进程还是多个物理服务器。

在集群应用中，工人流程可能单独崩溃，而不影响其他流程。 除了性能优势外，故障隔离是运行一组应用流程的另一个原因。 每当工人进程崩溃时，总是确保记录事件并使用cluster.fork()生成一个新进程。

#### 使用节点集群模块

节点的[集群模块](https://nodejs.org/api/cluster.html)使集群成为可能。 这使得一个主流程能够生成工人流程并在工人之间分配进入。

#### 使用 PM2

如果您使用 PM2 部署了您的应用程序，那么您可以利用群集_without out_ 修改您的应用代码。 您应该先确保您的 [应用程序是无国籍的](https://pm2.keymetrics.io/docs/usage/specifics/#stateless-apps) 这意味着过程中没有本地数据(例如会话、网络套接字连接等)。

当使用 PM2 运行应用程序时，您可以启用 **cluster 模式** 以便在您选择的几个实例的集群中运行它， 例如匹配机器上可用的 CPU 数量。 您可以手动使用 pm2 命令行工具更改集群中的进程数量，而不会停止应用。

要启用集群模式，请像这样启动应用程序：

```bash
# Start 4 worker processes
$ pm2 start npm --name my-app -i 4 -- start
# Auto-detect number of available CPUs and start that many worker processes
$ pm2 start npm --name my-app -i max -- start
```

这也可以在 PM2 进程文件 (`ecosystem.config) 中进行配置。 设置`exec_mode`到`cluster`和`instances`为要开始的工人数量，s`或类似)。

一旦运行，应用程序可以像这样缩放：

```bash
# Add 3 more workers
$ pm2 scale my-app +3
# Scale to a specific number of workers
$ pm2 scale my-app 2
```

关于 PM2 集群的更多信息，请访问 [Cluster Mode] (https://pm2.keymetrics.io/docs/usage/cluster-mode/) 在 PM2 文档中。

### 缓存请求结果

提高生产性能的另一项战略是应请求缓解结果。 这样您的应用就不会重复操作来为相同的请求服务。

使用 [Varnish](https://www.varnish-cache.org/) 或 [Nginx](https://blog.nginx.org/blog/nginx-caching-guide)（另请参阅 [Nginx Caching](https://serversforhackers.com/nginx-caching/)）之类的高速缓存服务器，可以显著提高应用程序的速度和性能。

### 使用负载平衡器

无论应用程序如何优化，单个实例只能处理有限数量的负载和流量。 缩放应用的一种方法是运行多个实例，并通过负载平衡器分配流量。 设置负载均衡器可以提高你的应用的性能和速度，并使它比单个实例更容易放大。

负载均衡器通常是一个反向代理，将流量调节到和从多个应用程序实例和服务器。 您可以通过使用 [Nginx](https://nginx.org/en/docs/http/load_balancing.html或 [HAProxy](https://www.digitalocean.com/community/tutorials/an-introduction-to-haproxy-and-load-balancing-concepts)，轻松地为您的应用设置负载平衡器。

在负载平衡中，您可能必须确保与特定会话 ID 相关联的请求连接到产生这些请求的过程。 这叫做_session affinity_, 或 _sticky sessions_, 可以通过上述建议处理，如使用Redis等数据存储来处理会话数据(取决于您的应用程序)。 关于讨论，请查看[使用多个节点](https://socket.io/docs/v4/using-multiple-nodes/)。

### 使用反向代理

反向代理服务器正在网络应用程序前面，对请求执行支持操作，除了将请求导向到应用程序。 它可以处理错误页、 压缩、 缓存、 服务文件以及负载平衡。

将不需要了解应用程序状态的任务移交给逆向代理，就可以释放快递来执行专门的应用程序任务。 为此原因，建议在生产中以反向代理运行快递，如 [Nginx](https://www.nginx.org/或 [HAProxy](https://www.haproxy.org/)。
