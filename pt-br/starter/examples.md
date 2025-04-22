---
layout: page
title: Exemplos expressos
description: Explore uma coleção de exemplos de aplicativos do Express.js cobrindo vários casos de uso, integrações e configurações avançadas para ajudá-lo a aprender e construir seus projetos.
menu: starter
lang: pt-br
redirect_from: ""
---

{% capture examples %}{% include readmes/express-master/examples.md %}{% endcapture %}
{{ examples | replace: "](.", "](https://github.com/expressjs/express/tree/master/examples" }}

## Exemplos adicionais

Estes são alguns exemplos adicionais com integrações mais extensas.

{% include community-caveat.html %}

- [prisma-fullstack](https://github.com/prisma/prisma-examples/tree/latest/pulse/fullstack-simple-chat) - Aplicativo Fullstack com Express and Next.js usando [Prisma](https://www.npmjs.com/package/prisma) como ORM
- [prisma-rest-api-ts](https://github.com/prisma/prisma-examples/tree/latest/orm/express) - API REST com Express in TypeScript usando [Prisma](https://www.npmjs.com/package/prisma) como ORM

### [Anterior: Arquivos estáticos ](/{{ page.lang }}/starter/static-files.html)&nbsp;&nbsp;&nbsp;&nbsp;[Próximo: FAQ ](/{{ page.lang }}/starter/faq.html)
