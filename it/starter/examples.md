---
layout: page
title: Esempi espressi
description: Esplora una raccolta di esempi di applicazioni Express.js che coprono vari casi di utilizzo, integrazioni e configurazioni avanzate per aiutarti a imparare e costruire i tuoi progetti.
menu: starter
lang: it
redirect_from: ""
---

{% capture examples %}{% include readmes/express-master/examples.md %}{% endcapture %}
{{ examples | replace: "](.", "](https://github.com/expressjs/express/tree/master/examples" }}

## Esempi aggiuntivi

Questi sono alcuni esempi aggiuntivi con integrazioni più estese.

{% include community-caveat.html %}

- [prisma-fullstack](https://github.com/prisma/prisma-examples/tree/latest/pulse/fullstack-simple-chat) - Fullstack app con Express e Next.js utilizzando [Prisma](https://www.npmjs.com/package/prisma) come ORM
- [prisma-rest-api-ts](https://github.com/prisma/prisma-examples/tree/latest/orm/express) - REST API with Express in TypeScript using [Prisma](https://www.npmjs.com/package/prisma) as an ORM

### [Precedente: File Statici ](/{{ page.lang }}/starter/static-files.html)&nbsp;&nbsp;&nbsp;&nbsp;[Next: FAQ ](/{{ page.lang }}/starter/faq.html)
