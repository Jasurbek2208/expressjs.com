---
layout: page
title: Escrever middleware para uso nos aplicativos Express
description: Aprenda a escrever funções de middleware personalizadas para aplicativos Express.js, incluindo exemplos e melhores práticas para melhorar a resolução de pedidos e respostas.
menu: guide
lang: pt-br
redirect_from: ""
---

# Escrever middleware para uso nos aplicativos Express

<h2>Geral</h2>

Middleware_ são funções que têm acesso ao [objeto de solicitação](/{{ page.lang }}/4x/api. tml#req) (`req`), o [objeto de resposta](/{{ page.lang }}/4x/api.html#res) (`res`) e a função `next` no ciclo de solicitação-resposta do aplicativo. A função `próxima` é uma função no roteador Expresso que, quando invocado, executa o intermediário sucedendo ao intermediário atual.

As funções do Middleware podem executar as seguintes tarefas:

- Execute qualquer código.
- Fazer alterações na solicitação e nos objetos de resposta.
- Encerrar o ciclo de solicitação-resposta.
- Chame o próximo middleware na pilha.

Se a função middleware atual não encerra o ciclo de resposta de solicitação, ela deve chamar `next()` para passar o controle para a próxima função middleware. Caso contrário, o pedido ficará pendurado.

A figura a seguir mostra os elementos de uma chamada de função middleware:

<table id="mw-fig">
<tbody><tr><td id="mw-fig-imgcell">
<img src="/images/express-mw.png" alt="Elements of a middleware function call" id="mw-fig-img" />
</td>
<td class="mw-fig-callouts">
<div class="callout" id="callout1">Método HTTP para o qual se aplica a função middleware.</div></tbody>

<div class="callout" id="callout2">Caminho (rota) para o qual a função middleware se aplica.</div>

<div class="callout" id="callout3">A função middleware.</div>

<div class="callout" id="callout4">Argumento de retorno para a função middleware, chamado "próximo" por convenção.</div>

<div class="callout" id="callout5">HTTP <a href="/{{ page.lang }}/4x/api.html#res">resposta</a> argumento para a função middleware, chamado "res" pela convenção.</div>

<div class="callout" id="callout6">HTTP <a href="/{{ page.lang }}/4x/api.html#req">solicite argumento</a> para a função middleware, chamado "req" pela convenção.</div>
</td></tr>
</table>

Começando com as funções de middleware Express, funções de intermediário que retornam uma Promessa chamarão `próximo(valor)` quando eles rejeitarem ou lançarem um erro. `next` será chamado com o valor rejeitado ou o erro lançado.

<h2>Exemplo</h2>

Aqui está um exemplo de uma aplicação simples "Hello World" Express.
The remainder of this article will define and add three middleware functions to the application:
one called `myLogger` that prints a simple log message, one called `requestTime` that
displays the timestamp of the HTTP request, and one called `validateCookies` that validates incoming cookies.

```js
const express = require('express')
const app = express()

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(3000)
```

<h3>Função Middleware myLogger</h3>
Aqui está um exemplo simples de uma função de middleware chamada "myLogger". Essa função apenas imprime "LOGGGED" quando uma solicitação para o aplicativo passa por ela. A função middleware é atribuída a uma variável chamada `myLogger`.

```js
const myLogger = function (req, res, next) {
  console.log('LOGGED')
  next()
}
```

<div class="doc-box doc-notice" markdown="1">
Observe a chamada acima para `next()`. Chamar esta função chama a próxima função de middleware no app.
A função `next()` não faz parte do Node.js ou API Express, mas é o terceiro argumento passado para a função middleware. A função `next()` pode ser nomeada qualquer coisa, mas por convenção, é sempre chamada de "next".
Para evitar confusões, utilize sempre esta convenção.
</div>

Para carregar a função middleware, chame `app.use()`, especificando a função middleware.
Por exemplo, o código a seguir carrega a função `myLogger` middleware antes da rota para o caminho raiz (/).

```js
const express = require('express')
const app = express()

const myLogger = function (req, res, next) {
  console.log('LOGGED')
  next()
}

app.use(myLogger)

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(3000)
```

Toda vez que o aplicativo recebe uma solicitação, ele imprime a mensagem "LOGGED" no terminal.

A ordem do carregamento do middleware é importante: as funções de middleware que são carregadas primeiro também são executadas primeiro.

Se o `myLogger` é carregado após a rota para o caminho raiz, a solicitação nunca chega a ela e o aplicativo não imprime "LOGGED", porque o gerenciador de rotas do caminho raiz termina o ciclo de resposta-requisição.

A função middleware `myLogger` simplesmente imprime uma mensagem, então passa a requisição para a próxima função de middleware na pilha chamando a função `next()`.

<h3>Tempo de solicitação de função Middleware</h3>

Em seguida, vamos criar uma função middleware chamada "requestTime" e adicionar uma propriedade chamada `requestTime`
ao objeto solicitado.

```js
const requestTime = function (req, res, next) {
  req.requestTime = Date.now()
  next()
}
```

O aplicativo agora usa a função middleware `requestTime`. Além disso, a função de retorno de chamada da rota raiz usa a propriedade que a função middleware adiciona a `req` (o objeto de solicitação).

```js
const express = require('express')
const app = express()

const requestTime = function (req, res, next) {
  req.requestTime = Date.now()
  next()
}

app.use(requestTime)

app.get('/', (req, res) => {
  let responseText = 'Hello World!<br>'
  responseText += `<small>Requested at: ${req.requestTime}</small>`
  res.send(responseText)
})

app.listen(3000)
```

Quando você faz uma solicitação na raiz do aplicativo, o aplicativo agora mostra a marcação de hora da sua solicitação no navegador.

<h3>Função Middleware validateCookies</h3>

Finalmente, vamos criar uma função de middleware que valida os cookies recebidos e envia uma resposta de 400 se cookies forem inválidos.

Aqui está uma função de exemplo que valida cookies com um serviço assíncrono externo.

```js
async function cookieValidator (cookies) {
  try {
    await externallyValidateCookie(cookies.testCookie)
  } catch {
    throw new Error('Invalid cookies')
  }
}
```

Aqui, usamos o [`cookie-parser`](/resources/middleware/cookie-parser.html) middleware para analisar cookies recebidos do objeto `req` e passá-los para a nossa função `cookieValidator`. O middleware 'validateCookies' retorna a promessa de que, após a rejeição, irá automaticamente acionar o nosso manipulador de erros.

```js
const express = require('express')
const cookieParser = require('cookie-parser')
const cookieValidator = require('./cookieValidator')

const app = express()

async function validateCookies (req, res, next) {
  await cookieValidator(req.cookies)
  next()
}

app.use(cookieParser())

app.use(validateCookies)

// error handler
app.use((err, req, res, next) => {
  res.status(400).send(err.message)
})

app.listen(3000)
```

<div class="doc-box doc-notice" markdown="1">
Observe como `next()` é chamado depois `await cookieValidator(req.cookies)`. Isso garante que se o `cookieValidator` resolver, o próximo middleware na pilha será chamado. Se passar qualquer coisa para a função `next()`
(exceto a sequência de caracteres `'route'`),
o Express considera a solicitação atual como estando em erro e irá
ignorar quaisquer funções restantes de roteamento e middleware que
não sejam de manipulação de erros.
</div>

Como você tem acesso ao objeto de solicitação, o objeto de resposta, a próxima função de middleware na pilha, e todo o nó. s API, as possibilidades com funções de middleware são infinitas.

Para mais informações sobre Express middleware, veja: [Usando Express middleware](/{{ page.lang }}/guide/using-middleware.html).

<h2>middleware configurável</h2>

Se precisar de seu middleware para ser configurável, exporte uma função que aceite um objeto de opções ou outros parâmetros, que então retorna a implementação intermediária com base nos parâmetros de entrada.

Arquivo: `meu-middleware.js`

```js
module.exports = function (options) {
  return function (req, res, next) {
    // Implement the middleware function based on the options object
    next()
  }
}
```

O middleware agora pode ser usado como mostrado abaixo.

```js
const mw = require('./my-middleware.js')

app.use(mw({ option1: '1', option2: '2' }))
```

Consulte [cookie-session](https://github.com/expressjs/cookie-session) e [compression](https://github.com/expressjs/compression) para ver exemplos de intermediário configurável.
