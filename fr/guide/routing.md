---
layout: page
title: Routage express
description: Apprenez à définir et utiliser des routes dans les applications Express.js, y compris les méthodes de trajet, les chemins de trajet, les paramètres et l'utilisation du routeur pour le routage modulaire.
menu: guide
lang: fr
redirect_from: ""
---

# Routage

_Routing_ indique comment les terminaux (URIs) d'une application répondent aux requêtes du client.
Pour une introduction au routage, voir [routage de base](/{{ page.lang }}/starter/basic-routing.html).

Vous définissez le routage à l'aide des méthodes de l'objet Express `app` qui correspondent aux méthodes HTTP;
par exemple, `app. et()` pour gérer les requêtes GET et `app.post` pour gérer les requêtes POST. Pour une liste complète,
voir [app.METHOD](/{{ page.lang }}/5x/api.html#app.METHOD). Vous pouvez également utiliser [app.all()](/{{ page.lang }}/5x/api.html#app.all) pour gérer toutes les méthodes HTTP et [app.use()](/{{ page.lang }}/5x/api.html#app. se) à
spécifiez le middleware comme fonction de rappel (Voir [Utilisation du middleware](/{{ page.lang }}/guide/using-middleware.html) pour plus de détails).

Ces méthodes de routage spécifient une fonction de rappel (parfois appelée "fonctions de gestionnaire") appelée lorsque l'application reçoit une requête vers la route spécifiée (endpoint) et la méthode HTTP. En d'autres termes, l'application "écoute" les requêtes qui correspondent à la(les) route(s) spécifiée(s) et à la(les) méthode(s), et quand il détecte une correspondance, il appelle la fonction de rappel spécifiée.

En fait, les méthodes de routage peuvent avoir plus d'une fonction de rappel en tant qu'arguments.
Avec plusieurs fonctions de rappel, il est important de fournir `next` comme argument à la fonction de callback puis appeler `next()` dans le corps de la fonction pour distribuer le contrôle
au prochain rappel.

Le code suivant est un exemple de route très basique.

```js
const express = require('express')
const app = express()

// respond with "hello world" when a GET request is made to the homepage
app.get('/', (req, res) => {
  res.send('hello world')
})
```

<h2 id="route-methods">Méthodes de la route</h2>

Une méthode de route est dérivée d'une des méthodes HTTP, et est attachée à une instance de la classe `express`.

Le code suivant est un exemple de routes qui sont définies pour le `GET` et les méthodes `POST` à la racine de l'application.

```js
// GET method route
app.get('/', (req, res) => {
  res.send('GET request to the homepage')
})

// POST method route
app.post('/', (req, res) => {
  res.send('POST request to the homepage')
})
```

Express supporte les méthodes qui correspondent à toutes les méthodes de requête HTTP : `get`, `post`, et ainsi de suite.
Pour une liste complète, voir [app.METHOD](/{{ page.lang }}/5x/api.html#app.METHOD).

Il y a une méthode de routage spéciale, `app.all()`, utilisée pour charger les fonctions du middleware à un chemin pour _toutes_ les méthodes de requête HTTP. Par exemple, le gestionnaire suivant est exécuté pour les requêtes vers la route `"/secret"` si vous utilisez `GET`, `POST`, `PUT`, `DELETE`, ou toute autre méthode de requête HTTP supportée dans le module [http](https://nodejs.org/api/http.html#http_http_methods).

```js
app.all('/secret', (req, res, next) => {
  console.log('Accessing the secret section ...')
  next() // pass control to the next handler
})
```

<h2 id="route-paths">Chemins de la route</h2>

Les chemins de la route, en combinaison avec une méthode de requête, définissent les points de terminaison à partir desquels les requêtes peuvent être faites. Les chemins de route peuvent être des chaînes, des chaînes de caractères ou des expressions régulières.

{% capture caution-character %} En express 5, les caractères `? , `+`, `\*`, `[]`et `()\` sont gérés différemment de la version 4, veuillez consulter le [guide de migration](/{{ page.lang }}/guide/migrating-5. tml#path-syntax) pour plus d'informations.{% endcapture %}

{% include admonitions/caution.html content=caution-character %}

{% capture note-dollar-character %}En express 4, des caractères d'expression régulière tels que `$` doivent être échappés avec un `\`.
{% endcapture %}

{% include admonitions/caution.html content=note-dollar-character %}

{% capture note-path-to-regexp %}
Express utilise [path-to-regexp](https://www.npmjs.com/package/path-to-regexp) pour correspondre aux chemins de route ; reportez-vous à la documentation path-to-regexp pour toutes les possibilités de définition des chemins de route. [Express Playground Router](https://bjohansebas.github.io/playground-router/) est un outil pratique pour tester les routes Express de base, bien qu'il ne supporte pas la recherche de patterns.
{% endcapture %}

{% include admonitions/note.html content=note-path-to-regexp %}

{% include admonitions/warning.html content="Les chaînes de requête ne font pas partie du chemin de la route." %}

### Chemins de route basés sur des chaînes de caractères

Ce chemin de route correspond aux requêtes vers la route racine, `/`.

```js
app.get('/', (req, res) => {
  res.send('root')
})
```

Ce chemin de route correspond aux requêtes à `/about`.

```js
app.get('/about', (req, res) => {
  res.send('about')
})
```

Ce chemin de route correspondra aux requêtes à `/random.text`.

```js
app.get('/random.text', (req, res) => {
  res.send('random.text')
})
```

### Chemins de route basés sur des chaînes de caractères

{% capture caution-string-patterns %} The string patterns in Express 5 no longer work. Veuillez vous référer au [guide de migration](/{{ page.lang }}/guide/migrating-5.html#path-syntax) pour plus d'informations.{% endcapture %}

{% include admonitions/caution.html content=caution-string-patterns %}

Ce chemin de route correspondra à `acd` et `abcd`.

```js
app.get('/ab?cd', (req, res) => {
  res.send('ab?cd')
})
```

Ce chemin correspondra à `abcd`, `abbcd`, `abbbcd`, et ainsi de suite.

```js
app.get('/ab+cd', (req, res) => {
  res.send('ab+cd')
})
```

Ce chemin correspondra à `abcd`, `abxcd`, `abRANDOMcd`, `ab123cd`, et ainsi de suite.

```js
app.get('/ab*cd', (req, res) => {
  res.send('ab*cd')
})
```

Ce chemin de route correspondra à `/abe` et `/abcde`.

```js
app.get('/ab(cd)?e', (req, res) => {
  res.send('ab(cd)?e')
})
```

### Chemins de route basés sur des expressions régulières

Ce chemin d'itinéraire correspondra à tout ce qui contient un "a".

```js
app.get(/a/, (req, res) => {
  res.send('/a/')
})
```

Ce chemin d'itinéraire correspondra à `butterfly` et `dragonfly`, mais pas `butterflyman`, `dragonflyman`, et ainsi de suite.

```js
app.get(/.*fly$/, (req, res) => {
  res.send('/.*fly$/')
})
```

<h2 id="route-parameters">Paramètres de la route</h2>

Les paramètres de la route sont des segments d'URL nommés qui sont utilisés pour capturer les valeurs spécifiées à leur position dans l'URL. Les valeurs capturées sont remplies dans l'objet `req.params`, avec le nom du paramètre route spécifié dans le chemin comme leurs clés respectives.

```
Route path: /users/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userId": "34", "bookId": "8989" }
```

Pour définir des routes avec des paramètres d'itinéraire, il suffit de spécifier les paramètres de l'itinéraire dans le chemin de la route comme indiqué ci-dessous.

```js
app.get('/users/:userId/books/:bookId', (req, res) => {
  res.send(req.params)
})
```

<div class="doc-box doc-notice" markdown="1">
Le nom de l'itinéraire paramčtres doit ętre constitué de "mot caractčres" ([A-Za-z0-9_]).
</div>

Puisque le trait d'union (`-`) et le point (`.`) sont interprétés littéralement, ils peuvent être utilisés avec des paramètres d'itinéraire à des fins utiles.

```
Route path: /flights/:from-:to
Request URL: http://localhost:3000/flights/LAX-SFO
req.params: { "from": "LAX", "to": "SFO" }
```

```
Route path: /plantae/:genus.:species
Request URL: http://localhost:3000/plantae/Prunus.persica
req.params: { "genus": "Prunus", "species": "persica" }
```

{% capture warning-regexp %}
En express 5, les caractères Regexp ne sont pas pris en charge dans les chemins de route, pour plus d'informations, veuillez vous référer au [guide de migration](/{{ page.lang }}/guide/migrating-5.html#path-syntax).{% endcapture %}

{% include admonitions/caution.html content=warning-regexp %}

Pour avoir plus de contrôle sur la chaîne exacte qui peut être associée à un paramètre de route, vous pouvez ajouter une expression régulière entre parenthèses (`()`) :

```
Route path: /user/:userId(\d+)
Request URL: http://localhost:3000/user/42
req.params: {"userId": "42"}
```

{% include admonitions/avertissement. tml content="Parce que l'expression régulière fait généralement partie d'une chaîne littérale, Assurez-vous d'échapper tous les caractères `\` avec un antislash supplémentaire, par exemple `\\d+`." %}

{% capture warning-version %}
En Express 4.x, <a href="https://github.com/expressjs/express/issues/2495">le caractère `*` dans les expressions régulières n'est pas interprété de la manière habituelle</a>. Comme solution de contournement, utilisez `{0,}` au lieu de `*`. Cela sera probablement corrigé dans Express 5.
{% endcapture %}

{% include admonitions/warning.html content=warning-version %}

<h2 id="route-handlers">Gestionnaires de routes</h2>

Vous pouvez fournir plusieurs fonctions de rappel qui se comportent comme [middleware](/{{ page.lang }}/guide/using-middleware.html) pour traiter une requête. La seule exception est que ces callbacks peuvent appeler `next('route')` pour contourner les rappels de route restants. Vous pouvez utiliser ce mécanisme pour imposer des conditions préalables sur une route, passent ensuite le contrôle aux routes suivantes s'il n'y a pas de raison de poursuivre l'itinéraire courant.

Les gestionnaires de routes peuvent être sous la forme d'une fonction, d'un tableau de fonctions, ou de combinaisons des deux, comme indiqué dans les exemples suivants.

Une seule fonction de rappel peut gérer une route. Par exemple :

```js
app.get('/example/a', (req, res) => {
  res.send('Hello from A!')
})
```

Plus d'une fonction de rappel peut gérer une route (assurez-vous de spécifier l'objet `next`). Par exemple :

```js
app.get('/example/b', (req, res, next) => {
  console.log('the response will be sent by the next function ...')
  next()
}, (req, res) => {
  res.send('Hello from B!')
})
```

Un tableau de fonctions de rappel peut gérer une route. Par exemple :

```js
const cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

const cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

const cb2 = function (req, res) {
  res.send('Hello from C!')
}

app.get('/example/c', [cb0, cb1, cb2])
```

Une combinaison de fonctions indépendantes et de tableaux de fonctions peut gérer une route. Par exemple :

```js
const cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

const cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

app.get('/example/d', [cb0, cb1], (req, res, next) => {
  console.log('the response will be sent by the next function ...')
  next()
}, (req, res) => {
  res.send('Hello from D!')
})
```

<h2 id="response-methods">Méthodes de réponse</h2>

Les méthodes de l'objet de réponse (`res`) dans la table suivante peuvent envoyer une réponse au client et terminer le cycle de réponse de la requête. Si aucune de ces méthodes n'est appelée à partir d'un gestionnaire d'itinéraire, la requête du client sera suspendue.

| Méthode                                                                                                                                                                                                                   | Libellé                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| [res.download()](/{{ page.lang }}/5x/api.html#res.download)     | Demander au téléchargement un fichier.                                                            |
| [res.end()](/{{ page.lang }}/5x/api.html#res.end)               | Terminer le processus de réponse.                                                                 |
| [res.json()](/{{ page.lang }}/5x/api.html#res.json)             | Envoyer une réponse JSON.                                                                         |
| [res.jsonp()](/{{ page.lang }}/5x/api.html#res.jsonp)           | Envoyer une réponse JSON avec le support JSONP.                                                   |
| [res.redirect()](/{{ page.lang }}/5x/api.html#res.redirect)     | Rediriger une requête.                                                                            |
| [res.render()](/{{ page.lang }}/5x/api.html#res.render)         | Afficher un modèle de vue.                                                                        |
| [res.send()](/{{ page.lang }}/5x/api.html#res.send)             | Envoyer une réponse de différents types.                                                          |
| [res.sendFile()](/{{ page.lang }}/5x/api.html#res.sendFile)     | Envoyer un fichier en tant que flux octet.                                                        |
| [res.sendStatus()](/{{ page.lang }}/5x/api.html#res.sendStatus) | Définit le code de statut de la réponse et envoie sa représentation en tant que corps de réponse. |

<h2 id="app-route">app.route()</h2>

Vous pouvez créer des gestionnaires de routes chaînables pour un chemin en utilisant `app.route()`.
Parce que le chemin est spécifié à un seul endroit, la création de routes modulaires est utile, tout comme la réduction de la redondance et des fautes de frappe. Pour plus d'informations sur les routes, voir : [documentation Router()](/{{ page.lang }}/5x/api.html#router).

Voici un exemple de gestionnaires de routes enchaînés qui sont définis en utilisant `app.route()`.

```js
app.route('/book')
  .get((req, res) => {
    res.send('Get a random book')
  })
  .post((req, res) => {
    res.send('Add a book')
  })
  .put((req, res) => {
    res.send('Update the book')
  })
```

<h2 id="express-router">Routeur</h2>

Utilisez la classe `express.Router` pour créer des gestionnaires de route modulaires et montables. Une instance `Router` est un système complet de middleware et de routage ; pour cette raison, elle est souvent appelée "mini-app".

L'exemple suivant crée un routeur en tant que module, charge une fonction middleware dedans, définit quelques routes, et monte le module routeur sur un chemin dans l'application principale.

Créez un fichier de routeur nommé `birds.js` dans le répertoire de l'application, avec le contenu suivant :

```js
const express = require('express')
const router = express.Router()

// middleware that is specific to this router
const timeLog = (req, res, next) => {
  console.log('Time: ', Date.now())
  next()
}
router.use(timeLog)

// define the home page route
router.get('/', (req, res) => {
  res.send('Birds home page')
})
// define the about route
router.get('/about', (req, res) => {
  res.send('About birds')
})

module.exports = router
```

Ensuite, chargez le module routeur dans l'application :

```js
const birds = require('./birds')

// ...

app.use('/birds', birds)
```

L'application sera maintenant en mesure de traiter les demandes vers `/birds` et `/birds/about`, ainsi que d'appeler la fonction middleware `timeLog` qui est spécifique à la route.

Mais si la route parente `/birds` a des paramètres de chemin, elle ne sera pas accessible par défaut à partir des sous-routes. Pour le rendre accessible, vous devrez passer l'option `mergeParams` au constructeur de routeur [reference](/{{ page.lang }}/5x/api.html#app.use).

```js
const router = express.Router({ mergeParams: true })
```
