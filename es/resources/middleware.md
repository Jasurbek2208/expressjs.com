---
layout: middleware
title: Middleware Express
description: Explore una lista de módulos de middleware de Express.js mantenidos por el equipo Express y la comunidad, incluyendo middleware integrado y módulos populares de terceros.
menu: resources
lang: es
redirect_from: ""
module: mw-home
---

## Middleware Express

Los módulos de middleware Express listados aquí son mantenidos por el equipo
[Expressjsjs](https://github.com/orgs/expressjs/people).

| Módulo Middleware                                                           | Descripción                                                                                                                                  |
| --------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| [body-parser](/{{page.lang}}/resources/middleware/body-parser.html)         | Analizar cuerpo de petición HTTP.                                                                                            |
| [compression](/{{page.lang}}/resources/middleware/compression.html)         | Comprimir respuestas HTTP.                                                                                                   |
| [connect-rid](/{{page.lang}}/resources/middleware/connect-rid.html)         | Generar ID de solicitud única.                                                                                               |
| [cookie-parser](/{{page.lang}}/resources/middleware/cookie-parser.html)     | Analizar cabecera de cookie y rellenar `req.cookies`. Ver también [cookies](https://github.com/jed/cookies). |
| [cookie-session](/{{page.lang}}/resources/middleware/cookie-session.html)   | Establecer sesiones basadas en cookies.                                                                                      |
| [cors](/{{page.lang}}/resources/middleware/cors.html)                       | Habilitar compartir recursos de origen cruzado (CORS) con varias opciones.                                |
| [errorhandler](/{{page.lang}}/resources/middleware/errorhandler.html)       | Desarrollo/depuración de errores de desarrollo.                                                                              |
| [method-override](/{{page.lang}}/resources/middleware/method-override.html) | Anular los métodos HTTP usando la cabecera.                                                                                  |
| [morgan](/{{page.lang}}/resources/middleware/morgan.html)                   | Logger de solicitudes HTTP.                                                                                                  |
| [multer](/{{page.lang}}/resources/middleware/multer.html)                   | Manejar datos de forma multiparte.                                                                                           |
| [response-time](/{{page.lang}}/resources/middleware/response-time.html)     | Grabar tiempo de respuesta HTTP.                                                                                             |
| [serve-favicon](/{{page.lang}}/resources/middleware/serve-favicon.html)     | Sirva un favicón.                                                                                                            |
| [serve-index](/{{page.lang}}/resources/middleware/serve-index.html)         | Servir listado de directorios para una ruta determinada.                                                                     |
| [serve-static](/{{page.lang}}/resources/middleware/serve-static.html)       | Servir archivos estáticos.                                                                                                   |
| [session](/{{page.lang}}/resources/middleware/session.html)                 | Establecer sesiones basadas en servidores (sólo desarrollo).                                              |
| [timeout](/{{page.lang}}/resources/middleware/timeout.html)                 | Establece un tiempo de espera de procesamiento de peticiones para HTTP.                                                      |
| [vhost](/{{page.lang}}/resources/middleware/vhost.html)                     | Crear dominios virtuales.                                                                                                    |

## Módulos adicionales de Middleware

Estos son algunos módulos de middleware más populares.

{% include community-caveat.html %}

| Módulo Middleware                                   | Descripción                                                                                                                                                                                |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [helmet](https://github.com/helmetjs/helmet)        | Ayuda a proteger tus aplicaciones configurando varias cabeceras HTTP.                                                                                                      |
| [passport](https://github.com/jaredhanson/passport) | Autenticación usando "estrategias" como OAuth, OpenID y muchas otras.  Ver [passportjs.org](https://passportjs.org/) para más información. |
