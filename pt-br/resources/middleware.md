---
layout: middleware
title: Middleware expresso
description: Explore uma lista de módulos de middleware Express.js mantidos pela equipe Express e pela comunidade, incluindo módulos de intermediários e de terceiros populares.
menu: resources
lang: pt-br
redirect_from: ""
module: mw-home
---

## Middleware expresso

Os módulos Express middleware listados aqui são mantidos pela
[equipe de Expressjs](https://github.com/orgs/expressjs/people).

| Módulo de Middleware                                                        | Descrição:                                                                                                                    |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| [body-parser](/{{page.lang}}/resources/middleware/body-parser.html)         | Analisar corpo da requisição HTTP.                                                                                            |
| [compression](/{{page.lang}}/resources/middleware/compression.html)         | Comprimir respostas HTTP.                                                                                                     |
| [connect-rid](/{{page.lang}}/resources/middleware/connect-rid.html)         | Gerar ID único de requisição.                                                                                                 |
| [cookie-parser](/{{page.lang}}/resources/middleware/cookie-parser.html)     | Analise o cabeçalho de cookie e preencha `req.cookies`. Ver também [cookies](https://github.com/jed/cookies). |
| [cookie-session](/{{page.lang}}/resources/middleware/cookie-session.html)   | Estabelecer sessões baseadas em cookies.                                                                                      |
| [cors](/{{page.lang}}/resources/middleware/cors.html)                       | Ativa o compartilhamento de recursos entre origens (CORS) com várias opções.                               |
| [errorhandler](/{{page.lang}}/resources/middleware/errorhandler.html)       | Processamento/depuração do desenvolvimento.                                                                                   |
| [method-override](/{{page.lang}}/resources/middleware/method-override.html) | Substituir métodos HTTP utilizando cabeçalho.                                                                                 |
| [morgan](/{{page.lang}}/resources/middleware/morgan.html)                   | Log do pedido HTTP.                                                                                                           |
| [multer](/{{page.lang}}/resources/middleware/multer.html)                   | Manipular dados de formulários de várias partes.                                                                              |
| [response-time](/{{page.lang}}/resources/middleware/response-time.html)     | Registrar tempo de resposta HTTP.                                                                                             |
| [serve-favicon](/{{page.lang}}/resources/middleware/serve-favicon.html)     | Sirva um favicon.                                                                                                             |
| [serve-index](/{{page.lang}}/resources/middleware/serve-index.html)         | Serve a lista de diretório para um determinado caminho.                                                                       |
| [serve-static](/{{page.lang}}/resources/middleware/serve-static.html)       | Servir arquivos estáticos.                                                                                                    |
| [session](/{{page.lang}}/resources/middleware/session.html)                 | Estabelecer sessões baseadas no servidor (apenas desenvolvimento).                                         |
| [timeout](/{{page.lang}}/resources/middleware/timeout.html)                 | Definir tempo limite de processamento de requisição periodicamente.                                                           |
| [vhost](/{{page.lang}}/resources/middleware/vhost.html)                     | Criar domínios virtuais.                                                                                                      |

## Módulos adicionais de middleware

Estes são alguns módulos de middleware mais populares.

{% include community-caveat.html %}

| Módulo de Middleware                                | Descrição:                                                                                                                                                                         |
| --------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [helmet](https://github.com/helmetjs/helmet)        | Ajuda a proteger seus aplicativos, definindo vários cabeçalhos HTTP.                                                                                                               |
| [passport](https://github.com/jaredhanson/passport) | Autenticação usando "estratégias" como OAuth, OpenID e muitas outras.  Veja [passportjs.org](https://passportjs.org/) para obter mais informações. |
