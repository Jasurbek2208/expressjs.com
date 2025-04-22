---
layout: page
title: 覆盖快递API
description: 探索如何在请求上通过覆盖方法和属性自定义和扩展Express.js API，并使用原型对应对象。
menu: guide
lang: 中
---

# 覆盖快递API

Express API 包含请求和响应对象上的各种方法和属性。 这些都是原型继承的。 Express API有两个扩展点：

1. 在 `expres.request` 和 `express.response` 中的全局原型。
2. 在 `app.request` 和 `app.response` 的 Appspecific 原型。

更改全局原型将在同一进程中影响所有加载的快速应用。 如果需要，只能在创建新应用后更改特定应用的原型。

## 方法

您可以通过分配自定义函数来覆盖现有方法的签名和行为。

下面是覆盖 [res.sendStatus](/4x/api.html#res.sendStatus)行为的例子。

```js
app.response.sendStatus = function (statusCode, type, message) {
  // code is intentionally kept simple for demonstration purpose
  return this.contentType(type)
    .status(statusCode)
    .send(message)
}
```

上述实现完全改变了`res.sendStatus`的原始签名。 它现在接受一个状态代码、编码类型和要发送到客户端的消息。

重写方法现在可以通过以下方式使用：

```js
res.sendStatus(404, 'application/json', '{"error":"resource not found"}')
```

## 属性

Express API 中的属性是以下两者之一：

1. 分配属性(例如: `req.baseUrl`, `req.originalUrl`)
2. 定义为getters(例如: `req.secure`, `req.ip`)

因为第1类属性是在当前请求-响应周期中在 "request" 和 "response" 对象上被动态分配的， 他们的行为不能被覆盖。

类别2下的属性可以使用Express API 扩展 API覆盖。

下面的代码重写`req.ip`的值。 现在，它只是返回 `Client-IP` 请求头的值。

```js
Object.defineProperty(app.request, 'ip', {
  configurable: true,
  enumerable: true,
  get () { return this.get('Client-IP') }
})
```

## 原型

为了提供Express API，请求/响应对象传递给Express(通过 `app(req), 例如，`……'需要从同一原型链中继承遗产。 默认情况下，这个请求是`http.IncomingRequest.prototype`，响应是`http.ServerResponse.prototype`。

除非有必要，建议只在申请一级，而不是在全球一级这样做。 还有，请注意正在使用的原型尽可能与默认原型匹配。

```js
// Use FakeRequest and FakeResponse in place of http.IncomingRequest and http.ServerResponse
// for the given app reference
Object.setPrototypeOf(Object.getPrototypeOf(app.request), FakeRequest.prototype)
Object.setPrototypeOf(Object.getPrototypeOf(app.response), FakeResponse.prototype)
```
