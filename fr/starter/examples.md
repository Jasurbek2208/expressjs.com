---
layout: page
title: Exemples Express
description: Explorez une collection d'exemples d'applications Express.js couvrant divers cas d'utilisation, intégrations et configurations avancées pour vous aider à apprendre et à construire vos projets.
menu: starter
lang: fr
redirect_from: ""
---

{% capture examples %}{% include readmes/express-master/examples.md %}{% endcapture %}
{{ examples | replace: "](.", "](https://github.com/expressjs/express/tree/master/examples" }}

## Exemples supplémentaires

Ce sont quelques exemples supplémentaires avec des intégrations plus étendues.

{% include community-caveat.html %}

- [prisma-fullstack](https://github.com/prisma/prisma-examples/tree/latest/pulse/fullstack-simple-chat) - Application Fullstack avec Express et Next.js en utilisant [Prisma](https://www.npmjs.com/package/prisma) en tant qu'ORM
- [prisma-rest-api-ts](https://github.com/prisma/prisma-examples/tree/latest/orm/express) - REST API avec Express in TypeScript en utilisant [Prisma](https://www.npmjs.com/package/prisma) en tant qu'ORM

### [Précédent : Fichiers statiques](/{{ page.lang }}/starter/static-files.html)&nbsp;&nbsp;&nbsp;&nbsp;[Suivant : FAQ ](/{{ page.lang }}/starter/faq.html)
