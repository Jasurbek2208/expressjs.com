---
layout: page
title: Roteamento básico expresso
description: Aprenda os fundamentos do roteamento em aplicações Express.js, incluindo como definir rotas, lidar com métodos HTTP e criar manipuladores de rotas para seu servidor web.
menu: starter
lang: pt-br
redirect_from: ""
---

# Roteamento básico

_Routing_ refere-se a determinar como uma aplicação responde a uma solicitação do cliente para um ponto final específico, que é um URI (ou caminho) e um método de requisição HTTP específico (GET, POST, e assim por diante).

Cada rota pode ter uma ou mais funções de manipulador, que são executadas quando a rota é correspondente.

A definição de rota aceita a seguinte estrutura:

```js
app.METHOD(PATH, HANDLER)
```

Onde:

- `app` é uma instância de `express`.
- `METHOD` é um [método de solicitação HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods), em minúsculas.
- O `PATH` é um caminho no servidor.
- `HANDLER` é a função executada quando a rota é correspondente.

<div class="doc-box doc-notice" markdown="1">
Este tutorial assume que uma instância `express` chamada `app` é criada e o servidor está sendo executado. Se você não estiver familiarizado com a criação de um aplicativo e iniciando-o, veja o [exemplo Olá mundo](/{{ page.lang }}/starter/hello-world.html).
</div>

Os exemplos seguintes ilustram a definição de rotas simples.

Responda com `Olá Mundo!` na página inicial:

```js
app.get('/', (req, res) => {
  res.send('Hello World!')
})
```

Responder a solicitação POST na rota raiz (`/`), a página inicial do aplicativo:

```js
app.post('/', (req, res) => {
  res.send('Got a POST request')
})
```

Responda a uma solicitação PUT para a rota `/user`:

```js
app.put('/user', (req, res) => {
  res.send('Got a PUT request at /user')
})
```

Responder a uma solicitação de DELETE para a rota `/user`:

```js
app.delete('/user', (req, res) => {
  res.send('Got a DELETE request at /user')
})
```

Para obter mais detalhes sobre roteamento, consulte o [guia de roteamento](/{{ page.lang }}/guide/routing.html).

### [Anterior: Gerador de aplicativo expresso ](/{{ page.lang }}/starter/generator.html)&nbsp;&nbsp;&nbsp;&nbsp;[Próximo: Servendo arquivos estáticos no Express ](/{{ page.lang }}/starter/static-files.html)