---
layout: page
title: Servindo arquivos estáticos no Express
description: Entenda como servir arquivos estáticos como imagens, CSS e JavaScript em aplicativos Express.js usando o middleware "static".
menu: starter
lang: pt-br
redirect_from: ""
---

# Servindo arquivos estáticos no Express

Para servir arquivos estáticos como imagens, arquivos CSS e arquivos JavaScript, use a função `express.static` middleware embutida no Express.

A assinatura da função é:

```js
express.static(root, [options])
```

O argumento `root` especifica o diretório raiz do qual se destinam os assets estáticos.
Para obter mais informações sobre o argumento `options`, consulte [express.static](/{{page.lang}}/4x/api.html#express.static).

Por exemplo, use o seguinte código para servir imagens, arquivos CSS e arquivos JavaScript em um diretório chamado `public`:

```js
app.use(express.static('public'))
```

Agora, você pode carregar os arquivos que estão no diretório `public`:

```text
http://localhost:3000/images/kitten.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/images/bg.png
http://localhost:3000/hello.html
```

<div class="doc-box doc-info">
Expresso analisa os arquivos relativos ao diretório estático, então o nome do diretório estático não faz parte do URL.
</div>

Para usar vários diretórios de ativos estáticos, chame a função `express.static` middleware várias vezes:

```js
app.use(express.static('public'))
app.use(express.static('files'))
```

Expresso olha os arquivos na ordem em que você definiu os diretórios estáticos com a função de middleware `express.static`.

{% capture alert_content %}
Para obter melhores resultados, [use um proxy reverso](/{{page.lang}}/advanced/best-practice-performance.html#use-a-reverse-proxy) cache para melhorar o desempenho do serviço de ativos estáticos.
{% endcapture %}
{% include admonitions/note.html content=alert_content %}

Para criar um prefixo de caminho virtual (onde o caminho não existe realmente no sistema de arquivos) para arquivos que são servidos pelo `express. função tatic`, [especifique um caminho de montagem](/{{ page.lang }}/4x/api.html#app.use) para o diretório estático, como mostrado abaixo:

```js
app.use('/static', express.static('public'))
```

Agora, você pode carregar os arquivos que estão no diretório `public` a partir do prefixo de caminho `/static`.

```text
http://localhost:3000/static/images/kitten.jpg
http://localhost:3000/static/css/style.css
http://localhost:3000/static/js/app.js
http://localhost:3000/static/images/bg.png
http://localhost:3000/static/hello.html
```

No entanto, o caminho que você fornece para a função `express.static` é relativo ao diretório de onde você inicia seu processo `node`. Se você executar o aplicativo expresso a partir de outro diretório, é mais seguro usar o caminho absoluto do diretório que você deseja servir:

```js
const path = require('path')
app.use('/static', express.static(path.join(__dirname, 'public')))
```

Para mais detalhes sobre a função `serve-static` e suas opções, consulte  [serve-static](/resources/middleware/serve-static.html).

### [Anterior: Rota Básica](/{{ page.lang }}/starter/basic-routing.html)&nbsp;&nbsp;&nbsp;&nbsp;[Próximo: Mais exemplos](/{{ page.lang }}/starter/examples.html)
