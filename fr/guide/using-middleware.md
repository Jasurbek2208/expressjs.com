---
layout: page
title: Utilisation du middleware Express
description: Apprenez à utiliser les middleware dans les applications Express.js, y compris les middleware de niveau application et routeur, la gestion des erreurs et l'intégration de logiciels tiers middleware.
menu: guide
lang: fr
redirect_from: ""
---

# Utilisation du middleware

Express est un framework web de routage et de middleware qui possède des fonctionnalités minimales : Une application Express est essentiellement une série d'appels de fonctions de middleware.

Les fonctions _Middleware_ sont des fonctions qui ont accès à [l'objet de requête](/{{ page.lang }}/4x/api. tml#req) (`req`), l'objet de [réponse](/{{ page.lang }}/4x/api.html#res) (`res`), et la prochaine fonction de middleware dans le cycle de réponse de l'application. La prochaine fonction du middleware est généralement dénotée par une variable nommée `next`.

Les fonctions Middleware peuvent effectuer les tâches suivantes :

- Exécuter n'importe quel code.
- Effectuez des modifications à la requête et aux objets de réponse.
- Termine le cycle de réponse de la requête.
- Appeler la prochaine fonction du middleware dans la pile.

Si la fonction middleware actuelle ne met pas fin au cycle de réponse de requête, elle doit appeler `next()` pour passer le contrôle à la prochaine fonction du middleware. Sinon, la demande sera laissée en suspens.

Une application Express peut utiliser les types de middleware suivants :

- (#middleware.application)
- [middleware au niveau du routeur] (#middleware.router)
- (#middleware.error-handling)
- (#middleware.built-in)
- [middleware de tierce partie](#middleware.third-party)

Vous pouvez charger le middleware au niveau de l'application et du routeur avec un chemin de montage optionnel.
Vous pouvez également charger une série de fonctions middleware ensemble, ce qui crée une sous-pile du système middleware à un point de montage.

<h2 id='middleware.application'>Outil d'interface de l'application</h2>

Lier le middleware au niveau de l'application à une instance de l'objet [app object](/{{ page.lang }}/4x/api.html#app) en utilisant `app.use()` et `app. Les fonctions ETHOD()`, où `METHOD` est la méthode HTTP de la requête que la fonction middleware gère (comme GET, PUT ou POST) en minuscule.

Cet exemple montre une fonction middleware sans chemin de montage. La fonction est exécutée chaque fois que l'application reçoit une requête.

```js
const express = require('express')
const app = express()

app.use((req, res, next) => {
  console.log('Time:', Date.now())
  next()
})
```

Cet exemple montre une fonction middleware montée sur le chemin `/user/:id`. La fonction est exécutée pour n'importe quel type de requête HTTP
sur le chemin `/user/:id`.

```js
app.use('/user/:id', (req, res, next) => {
  console.log('Request Type:', req.method)
  next()
})
```

Cet exemple montre une route et sa fonction de gestion (système middleware). La fonction gère les requêtes GET vers le chemin `/user/:id`.

```js
app.get('/user/:id', (req, res, next) => {
  res.send('USER')
})
```

Voici un exemple de chargement d'une série de fonctions middleware à un point de montage, avec un chemin de montage.
Il illustre une sous-pile middleware qui affiche les informations de requête pour tout type de requête HTTP vers le chemin `/user/:id`.

```js
app.use('/user/:id', (req, res, next) => {
  console.log('Request URL:', req.originalUrl)
  next()
}, (req, res, next) => {
  console.log('Request Type:', req.method)
  next()
})
```

Les gestionnaires de routes vous permettent de définir plusieurs routes pour un chemin. L'exemple ci-dessous définit deux routes pour les requêtes GET vers le chemin `/user/:id`. La deuxième route ne posera aucun problème, mais elle ne sera jamais appelée parce que le premier parcours termine le cycle de réponse de la requête.

Cet exemple montre une sous-pile middleware qui gère les requêtes GET vers le chemin `/user/:id`.

```js
app.get('/user/:id', (req, res, next) => {
  console.log('ID:', req.params.id)
  next()
}, (req, res, next) => {
  res.send('User Info')
})

// handler for the /user/:id path, which prints the user ID
app.get('/user/:id', (req, res, next) => {
  res.send(req.params.id)
})
```

Pour sauter le reste des fonctions du middleware à partir d'une pile de middleware du routeur, appelez `next('route')` pour passer le contrôle à la route suivante.

{% include admonitions/note.html content="`next('route')` ne fonctionnera que dans les fonctions du middleware qui ont été chargées en utilisant les fonctions `app.METHOD()` ou `router.METHOD()`. %}

Cet exemple montre une sous-pile middleware qui gère les requêtes GET vers le chemin `/user/:id`.

```js
app.get('/user/:id', (req, res, next) => {
  // if the user ID is 0, skip to the next route
  if (req.params.id === '0') next('route')
  // otherwise pass the control to the next middleware function in this stack
  else next()
}, (req, res, next) => {
  // send a regular response
  res.send('regular')
})

// handler for the /user/:id path, which sends a special response
app.get('/user/:id', (req, res, next) => {
  res.send('special')
})
```

Les Middleware peuvent également être déclarés dans un tableau pour être réutilisables.

Cet exemple montre un tableau avec une sous-pile middleware qui gère les requêtes GET vers le chemin `/user/:id`

```js
function logOriginalUrl (req, res, next) {
  console.log('Request URL:', req.originalUrl)
  next()
}

function logMethod (req, res, next) {
  console.log('Request Type:', req.method)
  next()
}

const logStuff = [logOriginalUrl, logMethod]
app.get('/user/:id', logStuff, (req, res, next) => {
  res.send('User Info')
})
```

<h2 id='middleware.router'>middleware au niveau du routeur</h2>

Le middleware au niveau du routeur fonctionne de la même manière que le middleware au niveau de l'application, sauf qu'il est lié à une instance de `express.Router()`.

```js
const router = express.Router()
```

Charger le middleware au niveau du routeur en utilisant les fonctions `router.use()` et `router.METHOD()`.

L'exemple suivant réplique le système middleware qui est affiché ci-dessus pour le middleware au niveau de l'application, en utilisant le middleware au niveau du routeur:

```js
const express = require('express')
const app = express()
const router = express.Router()

// a middleware function with no mount path. This code is executed for every request to the router
router.use((req, res, next) => {
  console.log('Time:', Date.now())
  next()
})

// a middleware sub-stack shows request info for any type of HTTP request to the /user/:id path
router.use('/user/:id', (req, res, next) => {
  console.log('Request URL:', req.originalUrl)
  next()
}, (req, res, next) => {
  console.log('Request Type:', req.method)
  next()
})

// a middleware sub-stack that handles GET requests to the /user/:id path
router.get('/user/:id', (req, res, next) => {
  // if the user ID is 0, skip to the next router
  if (req.params.id === '0') next('route')
  // otherwise pass control to the next middleware function in this stack
  else next()
}, (req, res, next) => {
  // render a regular page
  res.render('regular')
})

// handler for the /user/:id path, which renders a special page
router.get('/user/:id', (req, res, next) => {
  console.log(req.params.id)
  res.render('special')
})

// mount the router on the app
app.use('/', router)
```

Pour sauter le reste des fonctions du middleware du routeur, appelez `next('router')`
pour passer le contrôle hors de l'instance du routeur.

Cet exemple montre une sous-pile middleware qui gère les requêtes GET vers le chemin `/user/:id`.

```js
const express = require('express')
const app = express()
const router = express.Router()

// predicate the router with a check and bail out when needed
router.use((req, res, next) => {
  if (!req.headers['x-auth']) return next('router')
  next()
})

router.get('/user/:id', (req, res) => {
  res.send('hello, user!')
})

// use the router and 401 anything falling through
app.use('/admin', router, (req, res) => {
  res.sendStatus(401)
})
```

<h2 id='middleware.error-handling'>Gestion des erreurs du middleware</h2>

<div class="doc-box doc-notice" markdown="1">
La gestion d'erreurs du middleware prend toujours _four_ arguments. Vous devez fournir quatre arguments pour l'identifier comme une fonction de gestion des erreurs du middleware. Même si vous n'avez pas besoin d'utiliser l'objet `next`, vous devez le spécifier pour maintenir la signature. Sinon, l'objet `next` sera interprété comme un middleware régulier et ne gérera pas les erreurs.
</div>

Définissez les fonctions du middleware de la même manière que les autres fonctions du middleware, sauf avec quatre arguments au lieu de trois, spécifiquement avec la signature `(err, req, res, next)`:

```js
app.use((err, req, res, next) => {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```

Pour plus de détails sur la gestion des erreurs du middleware, voir : [Gestion des erreurs](/{{ page.lang }}/guide/error-handling.html).

<h2 id='middleware.built-in'>middleware intégré</h2>

À partir de la version 4.x, Express ne dépend plus de [Connect](https://github.com/senchalabs/connect). Les fonctions du middleware
qui étaient précédemment incluses avec Express sont maintenant dans des modules séparés ; voir [la liste des fonctions du middleware] (https://github.com/senchalabs/connect#middleware).

Express a les fonctions internes suivantes :

- [express.static](/en/4x/api.html#express.static) serves static assets such as HTML files, images, and so on.
- [express.json](/en/4x/api.html#express.json) analyse les requêtes entrantes avec des charges utiles JSON. **NOTE : Disponible avec Express 4.16.0+**
- [express.urlencoded](/en/4x/api.html#express.urlencoded) analyse les requêtes entrantes avec des charges utiles encodées en URL.  **NOTE : Disponible avec Express 4.16.0+**

<h2 id='middleware.third-party'>middleware de tierce partie</h2>

Utilisez des logiciels tiers pour ajouter des fonctionnalités aux applications Express.

Installez le module Node.js pour la fonctionnalité requise, puis chargez-le dans votre application au niveau de l'application ou au niveau du routeur.

L'exemple suivant illustre l'installation et le chargement de la fonction middleware d'analyse de cookies `cookie-parser`.

```bash
$ npm install cookie-parser
```

```js
const express = require('express')
const app = express()
const cookieParser = require('cookie-parser')

// load the cookie-parsing middleware
app.use(cookieParser())
```

Pour une liste partielle des fonctions middleware tierces qui sont couramment utilisées avec Express, voir : [middleware de tierce] (../resources/middleware.html).
