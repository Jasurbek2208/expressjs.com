---
layout: page
title: FAQ Express
description: Retrouvez les réponses aux questions les plus fréquemment posées sur Express.js, y compris les sujets sur la structure de l'application, les modèles, l'authentification, les moteurs de gabarit, la gestion des erreurs, et plus encore.
menu: starter
lang: fr
redirect_from: ""
---

# Foire Aux Questions

## Comment structurer ma candidature ?

Il n'y a pas de réponse définitive à cette question. La réponse dépend
de l'échelle de votre candidature et de l'équipe impliquée. Pour être aussi
flexible que possible, Express ne fait aucune supposition en terme de structure.

Les routes et autres logiques spécifiques à une application peuvent vivre dans autant de fichiers
que vous le souhaitez, dans n'importe quelle structure de répertoire que vous préférez. Pour plus d'inspiration,
consultez les exemples suivants :

- [Liste des itinéraires](https://github.com/expressjs/express/blob/4.13.1/examples/route-separation/index.js#L32-L47)
- [Route map](https://github.com/expressjs/express/blob/4.13.1/examples/route-map/index.js#L52-L66)
- [MVC style controllers](https://github.com/expressjs/express/tree/master/examples/mvc)

Il y a également des extensions tierces pour Express, qui simplifient certains de ces modèles:

- [Itinéraire de ressource](https://github.com/expressjs/express-resource)

## Comment définir des modèles?

Express n'a aucune notion de base de données. Ce concept est
laissé aux modules Node tiers, vous permettant ainsi
d'interagir avec quasiment toutes les bases de données.

Voir [LoopBack](http://loopback.io) pour un framework basé sur Express, centré autour de modèles.

## Comment puis-je authentifier les utilisateurs ?

L'authentification est une autre partie complexe dans laquelle Express
ne s'aventure pas. Vous pouvez utiliser n'importe quel schéma d'authentification que vous souhaitez.
Pour un simple nom d'utilisateur / schéma de mot de passe, voir [cet exemple](https://github.com/expressjs/express/tree/master/examples/auth).

## Quels moteurs de gabarits sont supportés par Express ?

Express prend en charge tout moteur de gabarit qui est conforme à la signature `(path, locals, callback)`.
Pour normaliser les interfaces du moteur de gabarits et la mise en cache, consultez le projet
[consolidate.js](https://github.com/visionmedia/consolidate.js)
pour plus de support. Les moteurs de gabarits non listés peuvent toujours supporter la signature Express.

Pour plus d'informations, voir [Utilisation de moteurs de gabarits avec Express](/{{page.lang}}/guide/using-template-engines.html).

## Comment gérer 404 réponses?

Dans Express, 404 réponses ne sont pas le résultat d'une erreur, donc
le middleware de gestion d'erreurs ne les capturera pas. Ce comportement est
car une réponse 404 indique simplement l'absence de travail supplémentaire à faire ;
en d'autres termes, Express a exécuté toutes les fonctions et routes du middleware,
et a trouvé qu'aucun d'eux n'a répondu. Tout ce que vous avez à faire est
d'ajouter une fonction middleware à la toute fin de la pile (en-dessous de toutes les autres fonctions)
pour gérer une réponse 404 :

```js
app.use((req, res, next) => {
  res.status(404).send("Sorry can't find that!")
})
```

Ajoute des routes dynamiquement à l'exécution sur une instance de `express.Router()`
afin que les routes ne soient pas remplacées par une fonction de middleware.

## Comment configurer un gestionnaire d'erreur ?

Vous définissez le middleware de la même manière que les autres middleware,
sauf avec quatre arguments au lieu de trois; spécifiquement avec la signature `(err, req, res, next)`:

```js
app.use((err, req, res, next) => {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```

Pour plus d'informations, voir [Gestion des erreurs](/{{ page.lang }}/guide/error-handling.html).

## Comment rendre le HTML simple ?

Vous ne le faites pas! Il n'y a pas besoin de "render" HTML avec la fonction `res.render()`.
Si vous avez un fichier spécifique, utilisez la fonction `res.sendFile()`.
Si vous utilisez beaucoup d'actifs depuis un répertoire, utilisez la fonction `express.static()`
middleware.

## Quelle version de Node.js est requise ?

- [Express 4.x](/{{ page.lang }}/4x/api.html) nécessite Node.js 0.10 ou supérieur.
- [Express 5.x](/{{ page.lang }}/5x/api.html) nécessite Node.js 18 ou plus.

### [Précédent : Plus d'exemples ](/{{ page.lang }}/starter/examples.html)
