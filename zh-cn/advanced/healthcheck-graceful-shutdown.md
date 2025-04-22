---
layout: page
title: 健康检查和平滑关闭
description: 学习如何在Express应用中进行健康检查和体面关闭，以提高可靠性，管理部署，并与Kubernetes等负载平衡器集成。
menu: advanced
lang: 中
redirect_from: ""
---

# 健康检查和平滑关闭

## 平滑关闭

当你部署一个新版本的应用程序时，你必须替换以前的版本。 您正在使用的进程管理器将首先向应用程序发送一个SIGTERM信号以通知它将被杀死. 一旦应用程序收到这个信号，它应该停止接受新的请求，完成所有正在进行的请求。 清理它使用的资源，包括数据库连接和文件锁，然后退出。

### 示例

```js
const server = app.listen(port)

process.on('SIGTERM', () => {
  debug('SIGTERM signal received: closing HTTP server')
  server.close(() => {
    debug('HTTP server closed')
  })
})
```

## 健康检查

负载平衡器使用健康检查来确定应用程序实例是否健康并可以接受请求。 For example, [Kubernetes has two health checks](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/):

- `liveness`, 它决定何时重新启动一个容器。
- “准备就绪”，这决定一个容器何时准备接受流量。 当一个pod 尚未准备好时，它将从服务负载平衡器中删除。