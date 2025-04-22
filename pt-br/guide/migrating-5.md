---
layout: page
title: Migrando para Express 5
description: Um guia completo para migrar seus aplicativos Express.js da versão 4 a 5, detalhando alterações quebraduras, métodos obsoletos e novas melhorias.
menu: guide
lang: pt-br
redirect_from: ""
---

# Movendo para Expresso 5

<h2 id="overview">Geral</h2>

Expresso 5 não é muito diferente do Express 4; embora ele mantenha a mesma API básica, ainda há mudanças que quebram a compatibilidade com a versão anterior. Portanto, um aplicativo construído com Express 4 pode não funcionar se você atualizá-lo para usar o Express 5.

Para instalar esta versão, você precisa ter uma versão 18 ou superior de Node.js. Em seguida, execute o seguinte comando em seu diretório de aplicativos:

```sh
npm install "express@5"
```

Você pode então executar seus testes automatizados para ver o que falhou e corrigir problemas de acordo com as atualizações listadas abaixo. Após falhas no teste, execute seu aplicativo para ver quais erros ocorrem. Você vai descobrir imediatamente se o aplicativo usa quaisquer métodos ou propriedades que não são suportadas.

## Expresse 5 Codemods

Para ajudá-lo a migrar seu servidor expresso, nós criamos um conjunto de codemods que irão ajudá-lo a atualizar automaticamente seu código para a última versão do Express.

Execute o seguinte comando para executar todos os codemods disponíveis:

```sh
npx @expressjs/codemod upgrade
```

Se você quiser executar um código específico, você pode executar o seguinte comando:

```sh
npx @expressjs/codemod name-of-the-codemod
```

Você pode encontrar a lista de codemods disponíveis [here](https://github.com/expressjs/codemod?tab=readme-ov-file#available-codemods).

<h2 id="changes">Mudanças no Express 5</h2>

**Métodos e propriedades removidos**

<ul class="doclist">
  <li><a href="#app.del">app.del()</a></li>
  <li><a href="#app.param">app.param(fn)</a></li>
  <li><a href="#plural">Nomes de métodos plurais</a></li>
  <li><a href="#leading">Evoluindo dois pontos no argumento de nome para app.param(name, fn)</a></li>
  <li><a href="#req.param">req.param(nome)</a></li>
  <li><a href="#res.json">res.json(obj, status)</a></li>
  <li><a href="#res.jsonp">res.jsonp(obj, status)</a></li>
  <li><a href="#magic-redirect">res.redirect('voltar') e res.location('voltar')</a></li>  
  <li><a href="#res.redirect">res.redirect(url, status)</a></li>
  <li><a href="#res.send.body">res.send(body, status)</a></li>
  <li><a href="#res.send.status">res.send(status)</a></li>
  <li><a href="#res.sendfile">res.sendfile()</a></li>
  <li><a href="#express.static.mime">express.static.mime</a></li>
  <li><a href="#express:router-debug-logs">expresso: roteador depurar logs</a></li>
</ul>

**Mudou**

<ul class="doclist">
  <li><a href="#path-syntax">Caminho de rota correspondente à sintaxe</a></li>
  <li>U<a href="#rejected-promises">promessas rejeitadas tratadas de middleware e manipuladores</a></li>
  <li><a href="#express.urlencoded">express.urlencoded</a></li>
  <li><a href="#app.listen">app.listen</a></li>
  <li><a href="#app.router">app.router</a></li>
  <li><a href="#req.body">req.body</a></li>
  <li><a href="#req.host">req.host</a></li>
  <li><a href="#req.query">req.query</a></li>
  <li><a href="#res.clearCookie">res.clearCookie</a></li>
  <li><a href="#res.status">res.status</a></li>
  <li><a href="#res.vary">res.vary</a></li>
</ul>

**Melhorias**

<ul class="doclist">
  <li><a href="#res.render">res.render()</a></li>
  <li><a href="#brotli-support">Suporte a codificação Brotli</a></li>
</ul>

### Métodos e propriedades removidos

Se você usar qualquer um desses métodos ou propriedades em seu aplicativo, ele irá falhar. Então, você precisará alterar seu aplicativo depois que você atualizar para a versão 5.

<h4 id="app.del">app.del()</h4>

Expresso 5 não suporta mais a função `app.del()`. Se você usa essa função, um erro é lançado. Para registrar as rotas HTTP DELETE, use a função `app.delete()`.

Inicialmente, `del` foi usado em vez de `delete`, porque `delete` é uma palavra-chave reservada em JavaScript. Entretanto, a partir do ECMAScript 6, `apagar` e outras palavras-chave reservadas podem ser usadas legalmente como nomes de propriedades.

{% capture codemod-deprecated-signatures %}
Você pode substituir as assinaturas obsoletas pelo seguinte comando:

```plain-text
npx @expressjs/codemod v4-deprecated-signatures
```

{% endcapture %}

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.del('/user/:id', (req, res) => {
  res.send(`DELETE /user/${req.params.id}`)
})

// v5
app.delete('/user/:id', (req, res) => {
  res.send(`DELETE /user/${req.params.id}`)
})
```

<h4 id="app.param">app.param(fn)</h4>

A assinatura `app.param(fn)` foi usada para modificar o comportamento da função `app.param(name, fn)`. Está obsoleto desde a versão 4.11.0, e Express 5 não apoia mais nada.

<h4 id="plural">Nomes de métodos plurais</h4>

Os nomes dos seguintes métodos foram pluralizados. No Express 4, a utilização dos métodos antigos resultou em um aviso de depreciação. Expresso 5 não os suporta de forma alguma:

`req.acceptsCharset()` foi substituído por `req.acceptsCharsets()`.

`req.acceptsEncoding()` é substituído por `req.acceptsEncodings()`.

`req.acceptsLanguage()` foi substituído por `req.acceptsLanguages()`.

{% capture codemod-pluralized-methods %}
Você pode substituir as assinaturas obsoletas pelo seguinte comando:

```plain-text
npx @expressjs/codemod pluralized-methods
```

{% endcapture %}

{% include admonitions/note.html content=codemod-pluralized-methods %}

```js
// v4
app.all('/', (req, res) => {
  req.acceptsCharset('utf-8')
  req.acceptsEncoding('br')
  req.acceptsLanguage('en')

  // ...
})

// v5
app.all('/', (req, res) => {
  req.acceptsCharsets('utf-8')
  req.acceptsEncodings('br')
  req.acceptsLanguages('en')

  // ...
})
```

<h4 id="leading">Posicionando dois pontos (:) no nome do app.param(name, fn)</h4>

Um personagem com dois pontos principais (:) no nome do `app. aram(name, fn)` é um remanescente do Express 3, e por uma questão de compatibilidade retrógrada, Express 4 apoiou-o com um aviso de depreciação. Expresso 5 irá ignorá-lo silenciosamente e usar o parâmetro de nome sem prefixá-lo com dois-pontos.

Isso não deve afetar seu código se você seguir a documentação Expresso 4 da [app.param](/{{ page.lang }}/4x/api. tml#app.param), pois não faz nenhuma menção ao dobro principal.

<h4 id="req.param">req.param(nome)</h4>

Este método potencialmente confuso e perigoso de recuperação de dados de formulários foi removido. Agora você precisará procurar especificamente o nome do parâmetro enviado em `req.params`, `req.body`, ou `req.query`.

{% capture codemod-req-param %}
Você pode substituir as assinaturas obsoletas pelo seguinte comando:

```plain-text
npx @expressjs/codemod req-param
```

{% endcapture %}

{% include admonitions/note.html content=codemod-req-param %}

```js
// v4
app.post('/user', (req, res) => {
  const id = req.param('id')
  const body = req.param('body')
  const query = req.param('query')

  // ...
})

// v5
app.post('/user', (req, res) => {
  const id = req.params.id
  const body = req.body
  const query = req.query

  // ...
})
```

<h4 id="res.json">res.json(obj, status)</h4>

Expresso 5 não suporta mais a assinatura `res.json(obj, status)`. Ao invés disso, defina o status e então encadee-o ao método `res.json()` como este: `res.status(status).json(obj)`.

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.post('/user', (req, res) => {
  res.json({ name: 'Ruben' }, 201)
})

// v5
app.post('/user', (req, res) => {
  res.status(201).json({ name: 'Ruben' })
})
```

<h4 id="res.jsonp">res.jsonp(obj, status)</h4>

Expresso 5 não suporta mais a assinatura `res.jsonp(obj, status)`. Ao invés disso, defina o status e então encadee-o ao método `res.jsonp()` como este: `res.status(status).jsonp(obj)`.

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.post('/user', (req, res) => {
  res.jsonp({ name: 'Ruben' }, 201)
})

// v5
app.post('/user', (req, res) => {
  res.status(201).jsonp({ name: 'Ruben' })
})
```

<h4 id="res.redirect">res.redirect(url, status)</h4>

Expresso 5 não suporta mais a assinatura `res.redirect(url, status)`. Ao invés disso, use a seguinte assinatura: `res.redirect(status, url)`.

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.get('/user', (req, res) => {
  res.redirect('/users', 301)
})

// v5
app.get('/user', (req, res) => {
  res.redirect(301, '/users')
})
```

<h4 id="magic-redirect">res.redirect('voltar') e res.location('voltar')</h4>

Expresse 5 não suporta mais a string mágica `back` nos métodos `res.redirect()` e `res.location()`. Ao invés disso, use o valor `req.get('Referrer') ahead '/'` para redirecionar de volta para a página anterior. No Express 4, os métodos res.`redirect('back')` e `res.location('back')` foram descontinuados.

{% capture codemod-magic-redirect %}
Você pode substituir as assinaturas obsoletas pelo seguinte comando:

```plain-text
npx @expressjs/codemod magic-redirect
```

{% endcapture %}

{% include admonitions/note.html content=codemod-magic-redirect %}

```js
// v4
app.get('/user', (req, res) => {
  res.redirect('back')
})

// v5
app.get('/user', (req, res) => {
  res.redirect(req.get('Referrer') || '/')
})
```

<h4 id="res.send.body">res.send(corpo estado)</h4>

O Express 5 não suporta mais a assinatura `res.send(obj, status)`. Ao
invés disso, configure o status e então encadeie-o ao método `res.send()` assim:
`res.status(status).send(obj)`.

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.get('/user', (req, res) => {
  res.send({ name: 'Ruben' }, 200)
})

// v5
app.get('/user', (req, res) => {
  res.status(200).send({ name: 'Ruben' })
})
```

<h4 id="res.send.status">res.send(status)</h4>

Expresso 5 não suporta mais a assinatura `res.send(status)`, onde `status` é um número. Ao invés disso, use os `res. função endStatus(statusCode)`, que define o código de status do cabeçalho de resposta HTTP e envia o texto da versão do código: "Não encontrado", "Erro interno do servidor", e assim por diante.
Se você precisar enviar um número usando os `res. função end()`, cita o número para convertê-lo em uma string, para que o Express não interprete como uma tentativa de usar a antiga assinatura não suportada.

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.get('/user', (req, res) => {
  res.send(200)
})

// v5
app.get('/user', (req, res) => {
  res.sendStatus(200)
})
```

<h4 id="res.sendfile">res.sendfile()</h4>

A função `res.sendfile()` foi substituída por uma versão caída por camelo `res.sendFile()` no Express 5.

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.get('/user', (req, res) => {
  res.sendfile('/path/to/file')
})

// v5
app.get('/user', (req, res) => {
  res.sendFile('/path/to/file')
})
```

<h4 id="express.static.mime">express.static.mime</h4>

No Express 5, `mime` não é mais uma propriedade exportada do campo `static`.
Use o [pacote `mime-types`](https://github.com/jshttp/mime-types) para trabalhar com valores do tipo MIME.

```js
// v4
express.static.mime.lookup('json')

// v5
const mime = require('mime-types')
mime.lookup('json')
```

<h4 id="express:router-debug-logs">expressão:roteador logs de depuração</h4>

No Express 5, a lógica de manipulação do roteador é realizada por uma dependência. Portanto, os logs de depuração
para o roteador não estão mais disponíveis sob o namespace 'expresso'.
No v4, os logs estavam disponíveis sob os namespaces `express:router`, `express:router:layer`,
e `express:router:route`. Todos esses foram incluídos sob o namespace `express:*`.
Na v5.1+, os logs estão disponíveis sob o namespaces `router`, `router:layer` e `router:route`.
Os logs de `roteador:layer` e `router:route` estão incluídos no namespace `router:*`.
Para alcançar os mesmos detalhes do log de depuração ao usar `express:*` no v4, use uma combinação de
`express:*`, `router` e `router:*`.

```sh
# v4
DEBUG=express:* node index.js

# v5
DEBUG=express:*,router,router:* node index.js
```

<h3>Alterado</h3>

<h4 id="path-syntax">Caminho de rota correspondente</h4>

A sintaxe de rota de correspondência de um caminho é quando uma string é fornecida como o primeiro parâmetro para o `app.all()`, `app.use()`, `app.METHOD()`, `router.all()`, `router.METHOD()`, and `router.use()` APIs. As seguintes alterações foram feitas em como a seqüência de caracteres de caminho é combinada para uma solicitação de entrada:

- O caractere curinga `*` deve ter um nome, correspondendo ao comportamento dos parâmetros `:`, use `/*splat` em vez de `/*`

```js
// v4
app.get('/*', async (req, res) => {
  res.send('ok')
})

// v5
app.get('/*splat', async (req, res) => {
  res.send('ok')
})
```

{% capture note_wildcard %}
`*splat` corresponde a qualquer caminho sem o caminho da raiz. Caso você precise coincidir com o caminho raiz também `/`, você pode usar `/{*splat}`, envolvendo o caractere curinga nos quadros.

```js
// v5
app.get('/{*splat}', async (req, res) => {
  res.send('ok')
})
```

{% endcapture %}
{% include admonitions/note.html content=note_wildcard %}

- O caractere opcional `?` não é mais suportado, use chaves em vez disso.

```js
// v4
app.get('/:file.:ext?', async (req, res) => {
  res.send('ok')
})

// v5
app.get('/:file{.:ext}', async (req, res) => {
  res.send('ok')
})
```

- Caracteres Regexp não são suportados. Por exemplo:

```js
app.get('/[discussion|page]/:slug', async (req, res) => {
  res.status(200).send('ok')
})
```

deve ser alterado para:

```js
app.get(['/discussion/:slug', '/page/:slug'], async (req, res) => {
  res.status(200).send('ok')
})
```

- Alguns personagens foram reservados para evitar confusão durante a atualização (`()[]?+!`), use `\` para escapá-los.
- Os nomes de parâmetros agora suportam identificadores JavaScript válidos, ou citados como `:"isto"`.

<h4 id="rejected-promises">promessas rejeitadas tratadas de intermediários e manipuladores</h4>

Solicite aos manipuladores e manipuladores que retornam promessas rejeitadas agora são tratados encaminhando o valor rejeitado como um `Erro` para o erro de manipulação do middleware. Isto significa que usar funções `async` como middleware e manipuladores são mais fáceis do que nunca. Quando um erro é lançado em uma função `async` ou uma promessa rejeitada é `aguardada` dentro de uma função async esses erros serão passados para o manipulador de erro como se chamando `next(err)`.

Detalhes de como Expresso lida com os erros está coberto na [documentação de manipulação de erro](/en/guide/error-handling.html).

<h4 id="express.urlencoded">expres.urlencoded</h4>

O método `express.urlencoded` torna a opção `estendida` `false` por padrão.

<h4 id="app.listen">Ouvir</h4>

No Express 5, o método `app.listen` invocará a função de callback fornecido pelo usuário (se fornecido) quando o servidor receber um evento de erro. Na Expressa 4, esses erros seriam lançados. Essa mudança desloca a responsabilidade da manipulação de erros para a função de retorno de chamada no Express 5. Se houver um erro, ele será passado para o callback como argumento.
Por exemplo:

```js
const server = app.listen(8080, '0.0.0.0', (error) => {
  if (error) {
    throw error // e.g. EADDRINUSE
  }
  console.log(`Listening on ${JSON.stringify(server.address())}`)
})
```

<h4 id="app.router">app.router</h4>

O objeto `app.router`, que foi removido no Express 4, retornou no Express 5. Na nova versão, este objeto é apenas uma referência ao roteador básico Express, Ao contrário do Express 3, onde um aplicativo teve que carregá-lo explicitamente.

<h4 id="req.body">req.corpo</h4> 

A propriedade `req.body` retorna `undefined` quando o corpo não foi analisado. No Express 4, por padrão ele retorna `{}`.

<h4 id="req.host">req.anfitrião</h4>

No Express 4, a função `req.host` incorretamente retirou o número da porta se estivesse presente. No Express 5, o número da porta é mantido.

<h4 id="req.query">req.consulta</h4>

A propriedade `req.query` não é mais uma propriedade gravável e em vez disso é um getter. O analisador de consulta padrão foi alterado de "estendido" para "simples".

<h4 id="res.clearCookie">res.clearCookie</h4>

O método `res.clearCookie` ignora as opções `maxAge` e `expires` fornecidas pelo usuário.

<h4 id="res.status">status.res.status</h4>

O método `res.status` só aceita inteiros no intervalo de `100` para `999`, seguindo o comportamento definido pelo Node. , e retorna um erro quando o código de status não é um inteiro.

<h4 id="res.query">variável.variação</h4>

O 'res.vary' lança um erro quando o argumento 'field' está faltando. No Express 4, se o argumento foi omitido, ele deu um aviso no console

### Melhorias

<h4 id="res.render">res.render()</h4>

Este método agora exige comportamento assíncrono para todos os motores de visualização, evitando erros causados por mecanismos de visualização que tiveram uma implementação síncrona e que violaram a interface recomendada.

<h4 id="brotli-support">Suporte à codificação Brotli</h4>

Expresso 5 suporta a codificação Brotli para solicitações recebidas de clientes que suportam isso.
