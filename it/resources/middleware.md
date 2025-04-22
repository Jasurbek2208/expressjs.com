---
layout: middleware
title: middleware espresso
description: Esplora un elenco di moduli middleware Express.js gestiti dal team Express e dalla comunità, inclusi middleware incorporati e popolari moduli di terze parti.
menu: resources
lang: it
redirect_from: ""
module: mw-home
---

## middleware espresso

Di seguito vengono riportati alcuni moduli middleware Express:

| Modulo Middleware                                                           | Descrizione                                                                                                                                                      |
| --------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [body-parser](/{{page.lang}}/resources/middleware/body-parser.html)         | Analizza il corpo della richiesta HTTP.                                                                                                          |
| [compression](/{{page.lang}}/resources/middleware/compression.html)         | Comprimi le risposte HTTP.                                                                                                                       |
| [connect-rid](/{{page.lang}}/resources/middleware/connect-rid.html)         | Genera ID richiesta univoco.                                                                                                                     |
| [cookie-parser](/{{page.lang}}/resources/middleware/cookie-parser.html)     | Analizza l'intestazione dei cookie e popola `req.cookies`. Cfr. anche [cookies](https://github.com/jed/cookies). |
| [cookie-session](/{{page.lang}}/resources/middleware/cookie-session.html)   | Stabilisci sessioni basate sui cookie.                                                                                                           |
| [cors](/{{page.lang}}/resources/middleware/cors.html)                       | Abilita la condivisione delle risorse di origine incrociata (CORS) con varie opzioni.                                         |
| [errorhandler](/{{page.lang}}/resources/middleware/errorhandler.html)       | Gestione errori di sviluppo/debug.                                                                                                               |
| [method-override](/{{page.lang}}/resources/middleware/method-override.html) | Ignora i metodi HTTP usando l'intestazione.                                                                                                      |
| [morgan](/{{page.lang}}/resources/middleware/morgan.html)                   | Registratore di richieste HTTP.                                                                                                                  |
| [multer](/{{page.lang}}/resources/middleware/multer.html)                   | Gestire i dati multi-parte.                                                                                                                      |
| [response-time](/{{page.lang}}/resources/middleware/response-time.html)     | Registra il tempo di risposta HTTP.                                                                                                              |
| [serve-favicon](/{{page.lang}}/resources/middleware/serve-favicon.html)     | Servire una favicon.                                                                                                                             |
| [serve-index](/{{page.lang}}/resources/middleware/serve-index.html)         | Serve l'elenco delle directory per un percorso specificato.                                                                                      |
| [serve-static](/{{page.lang}}/resources/middleware/serve-static.html)       | Servire file statici.                                                                                                                            |
| [session](/{{page.lang}}/resources/middleware/session.html)                 | Stabilisci sessioni basate su server (solo sviluppo).                                                                         |
| [timeout](/{{page.lang}}/resources/middleware/timeout.html)                 | Imposta un timeout elaborazione richiesta perioHTTP.                                                                                             |
| [vhost](/{{page.lang}}/resources/middleware/vhost.html)                     | Crea domini virtuali.                                                                                                                            |

## Moduli middleware aggiuntivi

Questi sono alcuni moduli middleware popolari aggiuntivi.

{% include community-caveat.html %}

| Modulo Middleware                                   | Descrizione                                                                                                                                                                                         |
| --------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [helmet](https://github.com/helmetjs/helmet)        | Aiuta a proteggere le tue app impostando varie intestazioni HTTP.                                                                                                                   |
| [passport](https://github.com/jaredhanson/passport) | Autenticazione utilizzando "strategie" come OAuth, OpenID e molte altre.  Vedi [passportjs.org](https://passportjs.org/) per maggiori informazioni. |
