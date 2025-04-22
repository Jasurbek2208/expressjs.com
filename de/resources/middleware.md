---
layout: middleware
title: Express-Middleware
description: Entdecken Sie eine Liste der Express.js Middleware-Module, die vom Express-Team und der Community verwaltet werden, einschließlich eingebauter Middleware und beliebter Module von Drittanbietern.
menu: resources
lang: de
redirect_from: ""
module: mw-home
---

## Express-Middleware

Die hier aufgelisteten Express-Middleware-Module werden vom
[Expressjs Team](https://github.com/orgs/expressjs/people) betreut.

| Middleware-Modul                                                            | Beschreibung                                                                                                                                 |
| --------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| [body-parser](/{{page.lang}}/resources/middleware/body-parser.html)         | HTTP-Request-Körper analysieren.                                                                                             |
| [compression](/{{page.lang}}/resources/middleware/compression.html)         | HTTP Antworten komprimieren.                                                                                                 |
| [connect-rid](/{{page.lang}}/resources/middleware/connect-rid.html)         | Generiere eindeutige Request-ID.                                                                                             |
| [cookie-parser](/{{page.lang}}/resources/middleware/cookie-parser.html)     | Parsen Sie Cookie-Header und füllen Sie `req.cookies`. Siehe auch [cookies](https://github.com/jed/cookies). |
| [cookie-session](/{{page.lang}}/resources/middleware/cookie-session.html)   | Cookie-basierte Sitzungen einrichten.                                                                                        |
| [cors](/{{page.lang}}/resources/middleware/cors.html)                       | Quellenübergreifende Ressourcenfreigabe (CORS) mit verschiedenen Optionen aktivieren.                     |
| [errorhandler](/{{page.lang}}/resources/middleware/errorhandler.html)       | Entwicklung Fehlerbehandlung/Debugging.                                                                                      |
| [method-override](/{{page.lang}}/resources/middleware/method-override.html) | HTTP-Methoden mit Header überschreiben.                                                                                      |
| [morgan](/{{page.lang}}/resources/middleware/morgan.html)                   | HTTP Request Logger.                                                                                                         |
| [multer](/{{page.lang}}/resources/middleware/multer.html)                   | Mehrteilige Formulardaten behandeln.                                                                                         |
| [response-time](/{{page.lang}}/resources/middleware/response-time.html)     | HTTP-Antwortzeit aufzeichnen.                                                                                                |
| [serve-favicon](/{{page.lang}}/resources/middleware/serve-favicon.html)     | Servieren Sie ein Favicon.                                                                                                   |
| [serve-index](/{{page.lang}}/resources/middleware/serve-index.html)         | Verzeichnisliste für einen angegebenen Pfad Servieren.                                                                       |
| [serve-static](/{{page.lang}}/resources/middleware/serve-static.html)       | Statische Dateien Servieren.                                                                                                 |
| [session](/{{page.lang}}/resources/middleware/session.html)                 | Server-basierte Sitzungen einrichten (nur Entwicklung).                                                   |
| [timeout](/{{page.lang}}/resources/middleware/timeout.html)                 | Setze eine Timeout PerioHTTP Request-Verarbeitung.                                                                           |
| [vhost](/{{page.lang}}/resources/middleware/vhost.html)                     | Virtuelle Domains anlegen.                                                                                                   |

## Zusätzliche Middleware-Module

Dies sind einige weitere beliebte Middleware-Module.

{% include community-caveat.html %}

| Middleware-Modul                                    | Beschreibung                                                                                                                                                                                         |
| --------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [helmet](https://github.com/helmetjs/helmet)        | Unterstützt die Sicherung Ihrer Apps durch die Einstellung verschiedener HTTP-Header.                                                                                                |
| [passport](https://github.com/jaredhanson/passport) | Authentifizierung mit "Strategien" wie OAuth, OpenID und vielen anderen.  Siehe [passportjs.org](https://passportjs.org/) für weitere Informationen. |
