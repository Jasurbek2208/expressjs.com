---
layout: page
title: Migrando para Express 4
description: Um guia para migrar seus aplicativos Express.js da versão 3 para 4, cobrindo mudanças no middleware, roteamento e como atualizar sua base de código eficazmente.
menu: guide
lang: pt-br
redirect_from: ""
---

# Mover para Expresso 4

<h2 id="overview">Geral</h2>

Expresso 4 é uma mudança quebrada do Express 3. Isso significa que um aplicativo Expresso 3 não funcionará se você atualizar a versão Expresso em suas dependências.

Cobertos deste artigo:

<ul class="doclist">
  <li><a href="#changes">Alterações no Express 4</a>.</li>
  <li><a href="#example-migration">Um exemplo</a> de migração de um aplicativo do Express 3 para o Express 4.</li>
  <li><a href="#app-gen">Atualizando para o gerador de aplicativos Express 4</a>.</li>
</ul>

<h2 id="changes">Mudanças no Express 4</h2>

Há várias mudanças significativas na Expresso 4:

<ul class="doclist">
  <li><a href="#core-changes">Altera para Express core e sistema de middleware.</a> As dependências de conexão e de middleware embutido foram removidas, então você deve adicionar middleware você mesmo.
  </li>
  <li><a href="#routing">Altera o sistema de roteamento.</a></li>
  <li><a href="#other-changes">Várias outras mudanças.</a></li>
</ul>

Ver também:

- [Novas funcionalidades em 4.x.](https://github.com/expressjs/express/wiki/New-features-in-4.x)
- [Migrando da 3.x para a versão 4.x.](https://github.com/expressjs/express/wiki/Migrating-from-3.x-to-4.x)

<h3 id="core-changes">
Altera no Núcleo Express e sistema de middleware
</h3>

O Express 4 não depende mais do Connect, e remove todos os
middlewares integrados do seu núcleo, exceto pela função
`express.static`. Isto significa que
Express agora é uma estrutura web de roteamento e middleware independente e
Versões e versões Express não são afetados por atualizações de middleware.

Sem o intermediário integrado, você deve adicionar explicitamente todo o intermediário
que é necessário para executar seu aplicativo. Basta seguir estes passos:

1. Instale o módulo: \`npm install --save <module-name>
2. Na sua aplicação, requer o módulo: `require('module-name')`
3. Use o módulo de acordo com sua documentação: `app.use( ... )`

A seguinte tabela lista Express 3 middleware e seus homólogos no Express 4.

<table class="doctable" border="1">
<tbody><tr><th>Expresso 3</th><th>Expresso 4</th></tr>
<tr><td><code>express.bodyParser</code></td>
<td><a href="https://github.com/expressjs/body-parser">body-parser</a> +
<a href="https://github.com/expressjs/multer">multer</a></td></tr>
<tr><td><code>express.compress</code></td>
<td><a href="https://github.com/expressjs/compression">compressão</a></td></tr>
<tr><td><code>express.cookieSession</code></td>
<td>U<a href="https://github.com/expressjs/cookie-session">cookie-session</a></td></tr>
<tr><td><code>express.cookieParser</code></td>
<td><a href="https://github.com/expressjs/cookie-parser">cookie-parser</a></td></tr>
<tr><td><code>express.logger</code></td>
<td><a href="https://github.com/expressjs/morgan">Morgan</a></td></tr>
<tr><td>U<code>expressão.sessão</code></td>
<td><a href="https://github.com/expressjs/session">express-session</a></td></tr>
<tr><td><code>express.favicon</code></td>
<td><a href="https://github.com/expressjs/serve-favicon">serve-favicon</a></td></tr>
<tr><td><code>express.responseTime</code></td>
<td><a href="https://github.com/expressjs/response-time">response-time</a></td></tr>
<tr><td><code>express.errorHandler</code></td>
<td><a href="https://github.com/expressjs/errorhandler">errorhandler</a></td></tr>
<tr><td><code>express.methodOverride</code></td>
<td><a href="https://github.com/expressjs/method-override">method-override</a></td></tr>
<tr><td><code>express.timeout</code></td>
<td><a href="https://github.com/expressjs/timeout">connect-timeout</a></td></tr>
<tr><td><code>express.vhost</code></td>
<td><a href="https://github.com/expressjs/vhost">vhost</a></td></tr>
<tr><td><code>express.csrf</code></td>
<td><a href="https://github.com/expressjs/csurf">csurf</a></td></tr>
<tr><td><code>express.directory</code></td>
<td><a href="https://github.com/expressjs/serve-index">serve-index</a></td></tr>
<tr><td>U<code>express.static</code></td>
<td><a href="https://github.com/expressjs/serve-static">Ave-estática</a></td></tr>
</tbody></table>

Aqui está a [lista completa](https://github.com/senchalabs/connect#middleware) de Express 4 middleware.

Na maioria dos casos, você pode simplesmente substituir a versão antiga 3 middleware com
seu Expresso 4. Para obter detalhes, consulte a documentação do módulo no
GitHub.

<h4 id="app-use"><code>app.use</code> aceita parâmetros</h4>

Na versão 4 você pode usar um parâmetro variável para definir o caminho onde as funções de middleware são carregadas, em seguida, leia o valor do parâmetro a partir do manipulador de reta.
Por exemplo:

```js
app.use('/book/:id', (req, res, next) => {
  console.log('ID:', req.params.id)
  next()
})
```

<h3 id="routing">
O sistema de roteamento
</h3>

Apps agora carregam implicitamente roteando middleware, então você não tem mais que
se preocupar com a ordem em que o middleware é carregado em relação a
o middleware do `router`.

A forma como você define rotas é inalterada, mas o sistema de roteamento tem dois
novos recursos para ajudar a organizar suas rotas:

{: .doclist }

- Um novo método, `app.route()`, para criar gerenciadores de rotas em cadeia para um caminho de rota.
- Uma nova classe, `express.Router`, para criar modular montável handlers.

<h4 id="app-route">Método <code>app.route()</code></h4>

O novo método `app.route()` permite que você crie gerenciadores de rotas
encadeáveis para um caminho de rota. Como o caminho é especificado em um único local, é útil criar rotas modulares, assim como reduzir a redundância e os tipos. Para obter mais informações
sobre rotas, consulte [documentação `Router()`](/{{ page.lang }}/4x/api.html#router).

Aqui está um exemplo de manipuladores de rota encadeados que são definidos usando a função `app.route()`.

```js
app.route('/book')
  .get((req, res) => {
    res.send('Get a random book')
  })
  .post((req, res) => {
    res.send('Add a book')
  })
  .put((req, res) => {
    res.send('Update the book')
  })
```

<h4 id="express-router"><code>express.Router</code> class</h4>

O outro recurso que ajuda a organizar rotas é uma nova classe,
`express.Router`, que você pode usar para criar modular montável um controlador de rotas
. Uma instância `Router` é um sistema de roteamento de intermediários e
completo; por esta razão, é muitas vezes referido como um "mini-app".

O exemplo a seguir cria um roteador como um módulo, carrega middleware em
ele, define algumas rotas e o conecta em um caminho no aplicativo principal.

Por exemplo, crie um arquivo de roteador chamado `birds.js` no diretório de aplicativos,
com o seguinte conteúdo:

```js
var express = require('express')
var router = express.Router()

// middleware specific to this router
router.use((req, res, next) => {
  console.log('Time: ', Date.now())
  next()
})
// define the home page route
router.get('/', (req, res) => {
  res.send('Birds home page')
})
// define the about route
router.get('/about', (req, res) => {
  res.send('About birds')
})

module.exports = router
```

Em seguida, carregue o módulo do roteador no aplicativo:

```js
var birds = require('./birds')

// ...

app.use('/birds', birds)
```

Agora o aplicativo será capaz de lidar com pedidos para os caminhos `/birds` e
`/birds/about`, e irá chamar o middleware `timeLog`
que é específico da rota.

<h3 id="other-changes">
Outras mudanças
</h3>

A tabela a seguir lista outras pequenas mas importantes mudanças no Express 4:

<table class="doctable" border="1">
<tbody><tr>
<th>Objeto</th>
<th>Descrição:</th>
</tr>
<tr>
<td>Node.js</td>
<td>Expresso 4 requer Node.js 0.10.x ou posterior e deixou de funcionar como
Node.js 0.8.x.</td>
</tr>
<tr>
<td markdown="1">
`http.createServer()`
</td>
<td markdown="1">
O módulo `http` não é mais necessário, a menos que você precise trabalhar diretamente com ele (socket.io/SPDY/HTTPS). O aplicativo pode ser iniciado usando a função
`app.listen()`.
</td>
</tr>
<tr>
<td markdown="1">
`app.configure()`
</td>
<td markdown="1">
A função `app.configure()` foi removida.  Use a função
`process.env.NODE_ENV` ou
`app.get('env')` para detectar o ambiente e configurar o aplicativo de acordo.
</td>
</tr>
<tr>
<td markdown="1">
`espaços json`
</td>
<td markdown="1">
A propriedade de aplicativos `json spaces` está desativada por padrão no Express 4.
</td>
</tr>
<tr>
<td markdown="1">
`req.accepted()`
</td>
<td markdown="1">
Use `req.accepts()`, `req.acceptsEncodings()`,
`req.acceptsCharsets()`, e `req.acceptsLanguages()`.
</td>
</tr>
<tr>
<td markdown="1">
`res.location()`
</td>
<td markdown="1">
Não resolve mais URLs relativas.
</td>
</tr>
<tr>
<td markdown="1">
`req.params`
</td>
<td markdown="1">
Era uma matriz; agora é um objeto.
</td>
</tr>
<tr>
<td markdown="1">
`res.locals`
</td>
<td markdown="1">
Era uma função; agora um objeto.
</td>
</tr>
<tr>
<td markdown="1">
`res.headerSent`
</td>
<td markdown="1">
Mudado para `res.headersSent`.
</td>
</tr>
<tr>
<td markdown="1">
`app.route`
</td>
<td markdown="1">
Agora disponível como `app.mountpath`.
</td>
</tr>
<tr>
<td markdown="1">
`res.on('header')`
</td>
<td markdown="1">
Removido.
</td>
</tr>
<tr>
<td markdown="1">
`res.charset`
</td>
<td markdown="1">
Removido.
</td>
</tr>
<tr>
<td markdown="1">
`res.setHeader('Set-Cookie', val)`
</td>
<td markdown="1">
A funcionalidade agora está limitada a definir o valor básico de cookie. Use
`res.cookie()` para a funcionalidade adicionada.
</td>
</tr>
</tbody></table>

<h2 id="example-migration">Exemplo de migração de aplicativos</h2>

Aqui está um exemplo de migração de um aplicativo Express 3 para o Express 4.
Os arquivos de interesse são `app.js` e `package.json`.

<h3 id="">Aplicação 
Versão 3
</h3>

<h4 id=""><code>app.js</code></h4>

Considere um aplicativo Express v.3 com o seguinte arquivo `app.js`:

```js
var express = require('express')
var routes = require('./routes')
var user = require('./routes/user')
var http = require('http')
var path = require('path')

var app = express()

// all environments
app.set('port', process.env.PORT || 3000)
app.set('views', path.join(__dirname, 'views'))
app.set('view engine', 'pug')
app.use(express.favicon())
app.use(express.logger('dev'))
app.use(express.methodOverride())
app.use(express.session({ secret: 'your secret here' }))
app.use(express.bodyParser())
app.use(app.router)
app.use(express.static(path.join(__dirname, 'public')))

// development only
if (app.get('env') === 'development') {
  app.use(express.errorHandler())
}

app.get('/', routes.index)
app.get('/users', user.list)

http.createServer(app).listen(app.get('port'), () => {
  console.log('Express server listening on port ' + app.get('port'))
})
```

<h4 id=""><code>package.json</code></h4>

O arquivo de acompanhamento da versão 3 `package.json` pode parecer
algo como isto:

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "3.12.0",
    "pug": "*"
  }
}
```

<h3 id="">
Processo
</h3>

Inicie o processo de migração instalando o middleware necessário para o aplicativo
Express 4 e atualize o Express e o Pug para sua respectiva versão
mais recente com o seguinte comando:

```bash
$ npm install serve-favicon morgan method-override express-session body-parser multer errorhandler express@latest pug@latest --save
```

Faça as seguintes alterações no `app.js`:

1. As funções embutidas do Express middleware `express.favicon`,
  `express.logger`, `express.methodOverride`,
  `express.session`, `express.bodyParser` e
  `express.errorHandler` não estão mais disponíveis no objeto
  `express`. Você deve instalar suas alternativas
  manualmente e carregá-las no aplicativo.

2. Você não precisa mais carregar a função `app.router`.
  Não é um objeto de aplicativo Expresso 4, então remova o código
  `app.use(app.router);`.

3. Certifique-se de que as funções de middleware estão carregadas na ordem correta - carregue o `errorHandler` após carregar as rotas do aplicativo.

<h3 id="">Versão 4 do aplicativo</h3>

<h4 id=""><code>package.json</code></h4>

Executar o comando `npm` acima atualizará o `package.json` da seguinte forma:

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "body-parser": "^1.5.2",
    "errorhandler": "^1.1.1",
    "express": "^4.8.0",
    "express-session": "^1.7.2",
    "pug": "^2.0.0",
    "method-override": "^2.1.2",
    "morgan": "^1.2.2",
    "multer": "^0.1.3",
    "serve-favicon": "^2.0.1"
  }
}
```

<h4 id=""><code>app.js</code></h4>

Em seguida, remova o código inválido, carregue o middleware
necessário e faça outras alterações conforme necessárias. O arquivo `app.js` será parecido com este:

```js
var http = require('http')
var express = require('express')
var routes = require('./routes')
var user = require('./routes/user')
var path = require('path')

var favicon = require('serve-favicon')
var logger = require('morgan')
var methodOverride = require('method-override')
var session = require('express-session')
var bodyParser = require('body-parser')
var multer = require('multer')
var errorHandler = require('errorhandler')

var app = express()

// all environments
app.set('port', process.env.PORT || 3000)
app.set('views', path.join(__dirname, 'views'))
app.set('view engine', 'pug')
app.use(favicon(path.join(__dirname, '/public/favicon.ico')))
app.use(logger('dev'))
app.use(methodOverride())
app.use(session({
  resave: true,
  saveUninitialized: true,
  secret: 'uwotm8'
}))
app.use(bodyParser.json())
app.use(bodyParser.urlencoded({ extended: true }))
app.use(multer())
app.use(express.static(path.join(__dirname, 'public')))

app.get('/', routes.index)
app.get('/users', user.list)

// error handling middleware should be loaded after the loading the routes
if (app.get('env') === 'development') {
  app.use(errorHandler())
}

var server = http.createServer(app)
server.listen(app.get('port'), () => {
  console.log('Express server listening on port ' + app.get('port'))
})
```

<div class="doc-box doc-info" markdown="1">
A não ser que precise trabalhar diretamente com
o módulo `http` (socket.io/SPDY/HTTPS),
carregá-lo não é necessário, e o aplicativo pode ser iniciado
simplesmente desta forma:

```js
app.listen(app.get('port'), () => {
  console.log('Express server listening on port ' + app.get('port'))
})
```

</div>

<h3 id="">Executar o aplicativo</h3>

O processo de migração está completo, e o aplicativo agora é um aplicativo
Express 4. Para confirmar, inicie o aplicativo usando o seguinte comando:

```bash
$ node .
```

Carregue [http://localhost:3000](http://localhost:3000)
e veja a página inicial sendo renderizada pelo Express 4.

<h2 id="app-gen">Atualizando para o gerador de aplicativos Express 4</h2>

A ferramenta de linha de comando para gerar um app Express ainda é
`express`, mas para atualizar para a nova versão, você deve desinstalar
o gerador de aplicativo Express 3 e então instalar o novo gerador
`express-generator`.

<h3 id="">Instalando </h3>

Se você já tiver o gerador de aplicativo Express 3 instalado em seu sistema,
você deve desinstalá-lo:

```bash
$ npm uninstall -g express
```

Dependendo de como seus privilégios de arquivo e diretório são configurados,
talvez você precise executar este comando com `sudo`.

Agora instale o novo gerador:

```bash
$ npm install -g express-generator
```

Dependendo de como seus privilégios de arquivo e diretório são configurados,
talvez você precise executar este comando com `sudo`.

Agora o comando `express` no seu sistema é atualizado para o gerador
Express 4.

<h3 id="">Alterações no gerador de aplicativos </h3>

Opções de comando e uso em grande parte permanecem iguais, com as seguintes exceções:

{: .doclist }

- A opção `--sessions` foi removida.
- A opção `--jshtml` foi removida.
- Adicionado a opção `--hogan` para apoiar [Hogan.js](http://twitter.github.io/hogan.js/).

<h3 id="">Exemplo</h3>

Execute o seguinte comando para criar um aplicativo Express 4:

```bash
$ express app4
```

Se você olhar o conteúdo do arquivo `app4/app.js`, você notará
que todas as funções de middleware (exceto `expressos. tatic`) que são necessários para
o aplicativo são carregados como módulos independentes, e o 'router' middleware
não está mais carregado explicitamente no aplicativo.

Você também vai notar que o arquivo `app.js` agora é um Node. módulo s, em contraste com o app autônomo gerado pelo gerador antigo.

Depois de instalar as dependências, inicie o aplicativo usando o seguinte comando:

```bash
$ npm start
```

Se você olhar o script `npm start` no `package. arquivo son`,
você notará que o comando real que inicia o aplicativo é
`node . bin/www`, que costumava ser `node app.js`
no Express 3.

Porque o arquivo `app.js` que foi gerado pelo gerador Express 4
agora é um Node. Módulo s não pode mais ser iniciado de forma independente como um aplicativo
(a menos que você modifique o código). O módulo deve ser carregado em um arquivo Node.js
e iniciado via arquivo Node.js. O arquivo Node.js é `./bin/www`
neste caso.

Nem o diretório `bin` nem o arquivo `www`
sem extensão são obrigatórios para a criação de um aplicativo Express ou para iniciar o aplicativo. Eles são apenas sugestões
feitas pelo gerador, portanto fique a vontade para modificá-los para
adequá-los às suas necessidades.

Para se livrar do diretório `www` e manter as coisas no caminho "Express 3",
apague a linha que diz `módulo. xports = app;` no final do arquivo
`app.js`, e então cole o seguinte código em seu lugar:

```js
app.set('port', process.env.PORT || 3000)

var server = app.listen(app.get('port'), () => {
  debug('Express server listening on port ' + server.address().port)
})
```

Certifique-se de carregar o módulo `debug` no topo do arquivo `app.js` usando o seguinte código:

```js
var debug = require('debug')('app4')
```

Em seguida, mude `"start": "node ./bin/www"` no arquivo `package.json` para `"start": "node app.js"`.

Você moveu a funcionalidade `./bin/www` de volta para
`app.js`. Esta mudança não é recomendada, mas o exercício ajuda você
a entender como o `. arquivo bin/www` funciona, e porque o arquivo `app.js`
não inicia mais por conta própria.
