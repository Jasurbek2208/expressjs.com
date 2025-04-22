---
layout: page
title: Express-Beispiele
description: Entdecken Sie eine Sammlung von Express.js Anwendungsbeispielen, die verschiedene Anwendungsfälle, Integrationen und erweiterte Konfigurationen umfassen, um Ihnen zu helfen Ihre Projekte zu erlernen und zu bauen.
menu: starter
lang: de
redirect_from: ""
---

{% capture examples %}{% include readmes/express-master/examples.md %}{% endcapture %}
{{ examples | replace: "](.", "](https://github.com/expressjs/express/tree/master/examples" }}

## Zusätzliche Beispiele

Dies sind einige zusätzliche Beispiele mit umfassenderen Integrationen.

{% include community-caveat.html %}

- [prisma-fullstack](https://github.com/prisma/prisma-examples/tree/latest/pulse/fullstack-simple-chat) - Vollstack App mit Express und Next.js mit [Prisma](https://www.npmjs.com/package/prisma) als ORM
- [prisma-rest-api-ts](https://github.com/prisma/prisma-examples/tree/latest/orm/express) - REST API mit Express in TypeScript mit [Prisma](https://www.npmjs.com/package/prisma) als ORM

### [Vorherige: Statische Dateien ](/{{ page.lang }}/starter/static-files.html)&nbsp;&nbsp;&nbsp;&nbsp;[Weiter: FAQ ](/{{ page.lang }}/starter/faq.html)
