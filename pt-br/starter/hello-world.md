---
layout: page
title: Expresse o exemplo "Hello World"
description: Comece com o Express.js construindo uma simples aplicação 'Hello World'', demonstrando a configuração básica e a criação de servidor para iniciantes.
menu: starter
lang: pt-br
redirect_from: ""
---

# Olá, exemplo do mundo

<div class="doc-box doc-info" markdown="1">
Embutido abaixo é essencialmente o aplicativo Expresso mais simples que você pode criar. É um único aplicativo de arquivo &mdash; _não_ o que você obteria se você usar o [gerador Expresso](/{{ page.lang }}/starter/generator. tml), que cria o andaime para uma aplicação completa com vários arquivos JavaScript, modelos Jade e subdiretórios para vários fins.
</div>

```js
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```

Este aplicativo inicia um servidor e escuta na porta 3000 para conexões. O aplicativo responde com "Olá Mundo!" para solicitações
para a URL raiz (`/`) ou _route_. Para todos os outros caminhos, responderá com um **404 Não Encontrado**.

### Executando localmente

Primeiro, crie um diretório chamado `myapp`, mude para ele e execute `npm init`. Em seguida, instale `express` como uma dependência, conforme o [guia de instalação](/{{ page.lang }}/starter/installing.html).

No diretório `myapp`, crie um arquivo chamado `app.js` e copie o código do exemplo acima.

<div class="doc-box doc-notice" markdown="1">
O `req` (solicitação) e `res` (resposta) são exatamente os mesmos objetos que o Node fornece, para que você possa invocar
`req. ipe()`, `req.on('data', callback)`, e qualquer coisa que você faria sem o Expresso envolvido.
</div>

Execute o aplicativo com o seguinte comando:

```bash
$ node app.js
```

Em seguida, carregue `http://localhost:3000/` em um navegador para ver a saída.

### [Anterior: Instalando ](/{{ page.lang }}/starter/installing.html)&nbsp;&nbsp;&nbsp;&nbsp;[Próximo: Gerador Expresso ](/{{ page.lang }}/starter/generator.html)
