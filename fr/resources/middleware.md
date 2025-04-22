---
layout: middleware
title: Schémas exprès
description: Explorez une liste de modules de middleware Express.js maintenus par l'équipe Express et la communauté, y compris les modules middleware intégrés et les modules tiers populaires.
menu: resources
lang: fr
redirect_from: ""
module: mw-home
---

## Schémas exprès

Les modules middleware Express listés ici sont maintenus par la
[équipe Expressjs](https://github.com/orgs/expressjs/people).

| Module Middleware                                                           | Libellé                                                                                                                                        |
| --------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| [body-parser](/{{page.lang}}/resources/middleware/body-parser.html)         | Analyse du corps de la requête HTTP.                                                                                           |
| [compression](/{{page.lang}}/resources/middleware/compression.html)         | Compresser les réponses HTTP.                                                                                                  |
| [connect-rid](/{{page.lang}}/resources/middleware/connect-rid.html)         | Générer un ID unique de requête.                                                                                               |
| [cookie-parser](/{{page.lang}}/resources/middleware/cookie-parser.html)     | Analyser l'en-tête des cookies et remplir `req.cookies`. Voir aussi [cookies](https://github.com/jed/cookies). |
| [cookie-session](/{{page.lang}}/resources/middleware/cookie-session.html)   | Établir des sessions basées sur les cookies.                                                                                   |
| [cors](/{{page.lang}}/resources/middleware/cors.html)                       | Activer le partage de ressources entre les origines multiples (CORS) avec diverses options.                 |
| [errorhandler](/{{page.lang}}/resources/middleware/errorhandler.html)       | Gestion des erreurs de développement/débogage.                                                                                 |
| [method-override](/{{page.lang}}/resources/middleware/method-override.html) | Remplacer les méthodes HTTP par des en-têtes.                                                                                  |
| [morgan](/{{page.lang}}/resources/middleware/morgan.html)                   | Enregistreur de requêtes HTTP.                                                                                                 |
| [multer](/{{page.lang}}/resources/middleware/multer.html)                   | Gérer les données de formulaires multi-pièces.                                                                                 |
| [response-time](/{{page.lang}}/resources/middleware/response-time.html)     | Enregistrer le temps de réponse HTTP.                                                                                          |
| [serve-favicon](/{{page.lang}}/resources/middleware/serve-favicon.html)     | Servez un favicon.                                                                                                             |
| [serve-index](/{{page.lang}}/resources/middleware/serve-index.html)         | Servez la liste des répertoires pour un chemin donné.                                                                          |
| [serve-static](/{{page.lang}}/resources/middleware/serve-static.html)       | Servir les fichiers statiques.                                                                                                 |
| [session](/{{page.lang}}/resources/middleware/session.html)                 | Établir des sessions basées sur le serveur (développement uniquement).                                      |
| [timeout](/{{page.lang}}/resources/middleware/timeout.html)                 | Définir un délai de traitement des requêtes HTTP expiré.                                                                       |
| [vhost](/{{page.lang}}/resources/middleware/vhost.html)                     | Créer des domaines virtuels.                                                                                                   |

## Modules middleware additionnels

Ce sont quelques modules additionnels populaires de middleware.

{% include community-caveat.html %}

| Module Middleware                                                                                                                                                | Libellé                                                                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [helmet](https://github.com/helmetjs/helmet) : module qui aide à sécuriser vos applications en définissant divers en-têtes HTTP. | Permet de sécuriser vos applications en définissant divers en-têtes HTTP.                                                                                                                      |
| [passport](https://github.com/jaredhanson/passport) : module de middleware Express dédié à l'authentification.                   | Authentification en utilisant des "stratégies" telles que OAuth, OpenID et bien d'autres.  See [passportjs.org](https://passportjs.org/) for more information. |
