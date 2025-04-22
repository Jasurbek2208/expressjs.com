---
layout: page
title: Instalando o Express
description: Aprenda a instalar o Express.js no seu ambiente Node.js, incluindo a configuração do diretório do seu projeto e o gerenciamento de dependências com npm.
menu: starter
lang: pt-br
redirect_from: ""
---

# Instalando

Supondo que você já instalou [Node.js](https://nodejs.org/), crie um diretório para segurar seu aplicativo e torne essa sua pasta de trabalho.

- [Expresso 4.x](/{{ page.lang }}/4x/api.html) requer Node.js 0.10 ou superior.
- [Express 5.x](/{{ page.lang }}/5x/api.html) requer Node.js 18 ou superior.

```bash
$ mkdir myapp
$ cd myapp
```

Use o comando `npm init` para criar um arquivo `package.json` para sua aplicação.
Para obter mais informações sobre como funciona o arquivo `package.json`, veja [Especificações da manipulação do package.json do npm](https://docs.npmjs.com/files/package.json).

```bash
$ npm init
```

Este comando avisa você para várias coisas, como o nome e a versão de seu aplicativo.
Por enquanto, você simplesmente pode clicar em RETURN para aceitar os padrões para a maioria deles, com a seguinte exceção:

```
entry point: (index.js)
```

Digite `app.js`, ou o que quiser que o nome do arquivo principal seja. Se você quer que seja `index.js`, pressione RETURN para aceitar o nome de arquivo padrão sugerido.

Agora, instale o Express no diretório `myapp` e salve-o na lista de dependências. Por exemplo:

```bash
$ npm install express
```

Para instalar o Express temporariamente e não adicioná-lo à lista de dependências:

```bash
$ npm install express --no-save
```

<div class="doc-box doc-info" markdown="1">
Por padrão com a versão npm 5.0+, `npm install` adiciona o módulo à lista de `dependências` no `package. arquivo son`; com versões anteriores do npm, você deve especificar a opção `--save` explicitamente. Então, depois, executar `npm install` no diretório de aplicativos irá instalar automaticamente módulos na lista de dependências.
</div>

### [Próximo: Olá Mundo ](/{{ page.lang }}/starter/hello-world.html)