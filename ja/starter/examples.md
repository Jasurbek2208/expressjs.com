---
layout: page
title: エクスプレス例
description: さまざまなユースケース、インテグレーション、高度な構成を網羅した Express.jsアプリケーション例のコレクションをご覧ください。プロジェクトの学習と構築に役立ちます。
menu: starter
lang: en
redirect_from: ""
---

{% capture examples %}{% include readmes/express-master/examples.md %}{% endcapture %}
{{ examples | replace: "](.", "](https://github.com/expressjs/express/tree/master/examples" }}

## その他の例

これらは、より広範な統合を伴ういくつかの追加の例です。

{% include community-caveat.html %}

- [prisma-fullstack](https://github.com/prisma/prisma-examples/tree/latest/pulse/fullstack-simple-chat) - ORMとしてExpressとNext.jsを使用したフルスタックアプリ [Prisma](https://www.npmjs.com/package/prisma)
- [prisma-rest-api-ts](https://github.com/prisma/prisma-examples/tree/latest/orm/express) - ORMとして [Prisma](https://www.npmjs.com/package/prisma) を使用する Express をTypeScript で REST API

### [Previous: Static Files ](/{{ page.lang }}/starter/static-files.html)&nbsp;&nbsp;&nbsp;&nbsp;[次へ: FAQ ](/{{ page.lang }}/starter/faq.html)
