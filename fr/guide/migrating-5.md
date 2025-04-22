---
layout: page
title: Migration vers Express 5
description: Un guide complet pour migrer vos applications Express.js de la version 4 à 5, détaillant les changements cassés, les méthodes obsolètes et les nouvelles améliorations.
menu: guide
lang: fr
redirect_from: ""
---

# Déplacement vers Express 5

<h2 id="overview">Aperçu</h2>

L'Express 5 n'est pas très différent de l'Express 4 ; bien qu'il maintienne la même API de base, il y a toujours des changements qui cèdent la compatibilité avec la version précédente. Par conséquent, une application construite avec Express 4 pourrait ne pas fonctionner si vous la mettez à jour pour utiliser Express 5.

Pour installer cette version, vous devez avoir une version 18 ou supérieure de Node.js. Ensuite, exécutez la commande suivante dans le répertoire de votre application :

```sh
npm install "express@5"
```

Vous pouvez ensuite exécuter vos tests automatisés pour voir ce qui échoue, et corriger les problèmes en fonction des mises à jour listées ci-dessous. Après avoir résolu des échecs de test, exécutez votre application pour voir quelles erreurs se produisent. Vous découvrirez immédiatement si l'application utilise des méthodes ou des propriétés qui ne sont pas prises en charge.

## 5 Codemos Express

Pour vous aider à migrer votre serveur express nous avons créé un ensemble de codemods qui vous aideront à mettre à jour automatiquement votre code vers la dernière version d'Express.

Exécutez la commande suivante pour exécuter tous les codemods disponibles :

```sh
npx @expressjs/codemod upgrade
```

Si vous voulez exécuter un code spécifique, vous pouvez exécuter la commande suivante :

```sh
npx @expressjs/codemod name-of-the-codemod
```

Vous pouvez trouver la liste des codes disponibles [here](https://github.com/expressjs/codemod?tab=readme-ov-file#available-codemods).

<h2 id="changes">Changements dans Express 5</h2>

**Méthodes et propriétés supprimées**

<ul class="doclist">
  <li><a href="#app.del">app.del()</a></li>
  <li><a href="#app.param">app.param(fn)</a></li>
  <li><a href="#plural">Noms de méthodes plurialisées</a></li>
  <li><a href="#leading">Deux points principaux dans l'argument de nom à app.param(name, fn)</a></li>
  <li><a href="#req.param">req.param(nom)</a></li>
  <li><a href="#res.json">res.json(obj, statut)</a></li>
  <li><a href="#res.jsonp">res.jsonp(obj, status)</a></li>
  <li><a href="#magic-redirect">res.redirect('back') et res.location('back')</a></li>  
  <li><a href="#res.redirect">res.redirect(url, statut)</a></li>
  <li><a href="#res.send.body">res.send(body, statut)</a></li>
  <li><a href="#res.send.status">res.send(status)</a></li>
  <li><a href="#res.sendfile">res.sendfile()</a></li>
  <li><a href="#express.static.mime">express.static.mime</a></li>
  <li><a href="#express:router-debug-logs">express:le journal de débogage</a></li>
</ul>

**Modifié**

<ul class="doclist">
  <li><a href="#path-syntax">Path route matching syntax</a></li>
  <li><a href="#rejected-promises">Rejected promises handled from middleware and handlers</a></li>
  <li><a href="#express.urlencoded">express.urlencoded</a></li>
  <li><a href="#app.listen">app.listen</a></li>
  <li><a href="#app.router">app.router</a></li>
  <li><a href="#req.body">req.body</a></li>
  <li><a href="#req.host">req.host</a></li>
  <li><a href="#req.query">req.query</a></li>
  <li><a href="#res.clearCookie">res.clearCookie</a></li>
  <li><a href="#res.status">res.status</a></li>
  <li><a href="#res.vary">res.vary</a></li>
</ul>

**Améliorations**

<ul class="doclist">
  <li><a href="#res.render">res.render()</a></li>
  <li><a href="#brotli-support">Support de l'encodage Brotli</a></li>
</ul>

### Méthodes et propriétés supprimées

Si vous utilisez l'une de ces méthodes ou propriétés dans votre application, cela plantera. Donc, vous devrez changer votre application après la mise à jour vers la version 5.

<h4 id="app.del">app.del()</h4>

Express 5 ne prend plus en charge la fonction `app.del()`. Si vous utilisez cette fonction, une erreur est levée. Pour enregistrer les routes HTTP DELETE, utilisez la fonction `app.delete()` à la place.

Initialement, `del` a été utilisé à la place de `delete`, parce que `delete` est un mot-clé réservé en JavaScript. Cependant, depuis ECMAScript 6, `delete` et d'autres mots-clés réservés peuvent légalement être utilisés comme noms de propriétés.

{% capture codemod-deprecated-signatures %}
Vous pouvez remplacer les signatures obsolètes par la commande suivante :

```plain-text
npx @expressjs/codemod v4-deprecated-signatures
```

{% endcapture %}

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.del('/user/:id', (req, res) => {
  res.send(`DELETE /user/${req.params.id}`)
})

// v5
app.delete('/user/:id', (req, res) => {
  res.send(`DELETE /user/${req.params.id}`)
})
```

<h4 id="app.param">app.param(fn)</h4>

La signature `app.param(fn)` a été utilisée pour modifier le comportement de la fonction `app.param(name, fn)`. Il est obsolète depuis la version 4.11.0, et Express 5 ne le supporte plus du tout.

<h4 id="plural">Noms de méthodes pluralisées</h4>

Les noms de méthodes suivantes ont été pluralisés. Dans Express 4, l'utilisation des anciennes méthodes a donné lieu à un avertissement de dépréciation. Express 5 ne les supporte plus du tout:

`req.acceptsCharset()` est remplacé par `req.acceptsCharsets()`.

`req.acceptsEncoding()` est remplacé par `req.acceptsEncodings()`.

`req.acceptsLanguage()` est remplacé par `req.acceptsLanguages()`.

{% capture codemod-pluralized-methods %}
Vous pouvez remplacer les signatures obsolètes par la commande suivante :

```plain-text
npx @expressjs/codemod pluralized-methods
```

{% endcapture %}

{% include admonitions/note.html content=codemod-pluralized-methods %}

```js
// v4
app.all('/', (req, res) => {
  req.acceptsCharset('utf-8')
  req.acceptsEncoding('br')
  req.acceptsLanguage('en')

  // ...
})

// v5
app.all('/', (req, res) => {
  req.acceptsCharsets('utf-8')
  req.acceptsEncodings('br')
  req.acceptsLanguages('en')

  // ...
})
```

<h4 id="leading">Point-virgule (:) dans le nom de app.param(name, fn)</h4>

Un caractère de deux points (:) dans le nom de l'application`. aram(name, fn)` est un reste d'Express 3, et pour des raisons de compatibilité ascendante, Express 4 l'a supporté avec une notification de dépréciation. Express 5 l'ignorera silencieusement et utilisera le paramètre de nom sans le préfixer avec un deux-points.

Cela ne devrait pas affecter votre code si vous suivez la documentation Express 4 de [app.param](/{{ page.lang }}/4x/api. tml#app.param), car il ne mentionne pas le point-virgule principal.

<h4 id="req.param">param(nom)</h4>

Cette méthode potentiellement confuse et dangereuse de récupération des données de formulaire a été supprimée. Vous devrez maintenant spécifiquement chercher le nom du paramètre soumis dans l'objet `req.params`, `req.body`, ou `req.query`.

{% capture codemod-req-param %}
Vous pouvez remplacer les signatures obsolètes par la commande suivante :

```plain-text
npx @expressjs/codemod req-param
```

{% endcapture %}

{% include admonitions/note.html content=codemod-req-param %}

```js
// v4
app.post('/user', (req, res) => {
  const id = req.param('id')
  const body = req.param('body')
  const query = req.param('query')

  // ...
})

// v5
app.post('/user', (req, res) => {
  const id = req.params.id
  const body = req.body
  const query = req.query

  // ...
})
```

<h4 id="res.json">res.json(obj, statut)</h4>

Express 5 ne prend plus en charge la signature `res.json(obj, status)`. Au lieu de cela, définissez le statut, puis enchaînez-le à la méthode `res.json()` comme ceci: `res.status(status).json(obj)`.

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.post('/user', (req, res) => {
  res.json({ name: 'Ruben' }, 201)
})

// v5
app.post('/user', (req, res) => {
  res.status(201).json({ name: 'Ruben' })
})
```

<h4 id="res.jsonp">res.jsonp(obj, status)</h4>

Express 5 ne prend plus en charge la signature `res.jsonp(obj, status)`. Au lieu de cela, définissez le statut, puis enchaînez-le à la méthode `res.jsonp()` comme ceci: `res.status(status).jsonp(obj)`.

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.post('/user', (req, res) => {
  res.jsonp({ name: 'Ruben' }, 201)
})

// v5
app.post('/user', (req, res) => {
  res.status(201).jsonp({ name: 'Ruben' })
})
```

<h4 id="res.redirect">res.redirect(url, statut)</h4>

Express 5 ne prend plus en charge la signature `res.redirect(url, status)`. À la place, utilisez la signature suivante : `res.redirect(status, url)`.

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.get('/user', (req, res) => {
  res.redirect('/users', 301)
})

// v5
app.get('/user', (req, res) => {
  res.redirect(301, '/users')
})
```

<h4 id="magic-redirect">res.redirect('back') et res.location('back')</h4>

Express 5 ne supporte plus la chaîne magique `back` dans les méthodes `res.redirect()` et `res.location()`. À la place, utilisez la valeur `req.get('Referrer') || '/'` pour rediriger vers la page précédente. Dans Express 4, les méthodes res.`redirect('back')` et `res.location('back')` sont dépréciées.

{% capture codemod-magic-redirect %}
Vous pouvez remplacer les signatures obsolètes par la commande suivante :

```plain-text
npx @expressjs/codemod magic-redirect
```

{% endcapture %}

{% include admonitions/note.html content=codemod-magic-redirect %}

```js
// v4
app.get('/user', (req, res) => {
  res.redirect('back')
})

// v5
app.get('/user', (req, res) => {
  res.redirect(req.get('Referrer') || '/')
})
```

<h4 id="res.send.body">res.send(body, statut)</h4>

Express 5 ne prend plus en charge la signature
`res.send(obj, status)`. A la place, définissez le
statut et enchaînez-le à la méthode
`res.send()` comme suit :
`res.status(status).send(obj)`.

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.get('/user', (req, res) => {
  res.send({ name: 'Ruben' }, 200)
})

// v5
app.get('/user', (req, res) => {
  res.status(200).send({ name: 'Ruben' })
})
```

<h4 id="res.send.status">res.send(statut)</h4>

Express 5 ne prend plus en charge la signature `res.send(status)`, où `status` est un nombre. À la place, utilisez les `res. la fonction endStatus(statusCode)`, qui définit le code d'état de l'en-tête de réponse HTTP et envoie la version texte du code: "Non trouvée", "Erreur interne du serveur", et ainsi de suite.
Si vous avez besoin d'envoyer un numéro en utilisant les `res. la fonction end()`, guillemets le nombre pour le convertir en une chaîne, afin qu'Express ne l'interprète pas comme une tentative d'utiliser l'ancienne signature non supportée.

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.get('/user', (req, res) => {
  res.send(200)
})

// v5
app.get('/user', (req, res) => {
  res.sendStatus(200)
})
```

<h4 id="res.sendfile">res.sendfile()</h4>

La fonction `res.sendfile()` a été remplacée par une version à chameau `res.sendFile()` dans Express 5.

{% include admonitions/note.html content=codemod-deprecated-signatures %}

```js
// v4
app.get('/user', (req, res) => {
  res.sendfile('/path/to/file')
})

// v5
app.get('/user', (req, res) => {
  res.sendFile('/path/to/file')
})
```

<h4 id="express.static.mime">express.static.mime</h4>

Dans Express 5, `mime` n'est plus une propriété exportée du champ `static`.
Utilisez le paquet [`mime-types`](https://github.com/jshttp/mime-types) pour travailler avec les valeurs de type MIME.

```js
// v4
express.static.mime.lookup('json')

// v5
const mime = require('mime-types')
mime.lookup('json')
```

<h4 id="express:router-debug-logs">express:journaux de débogage du routeur</h4>

Dans Express 5, la logique de gestion du routeur est effectuée par une dépendance. Par conséquent, les journaux de débogage
pour le routeur ne sont plus disponibles dans l'espace de noms `express:`.
Dans la v4, les logs étaient disponibles sous les espaces de noms `express:router`, `express:router:layer`,
et `express:router:route`. Tous ces éléments ont été inclus dans l'espace de noms `express:*`.
En v5.1+, les logs sont disponibles dans les espaces de noms `router`, `router:layer`, et `router:route`.
Les logs de `router:layer` et `router:route` sont inclus dans l'espace de noms `router:*`.
Pour obtenir le même détail de débogage lors de l'utilisation de `express:*` dans la v4, utilisez une conjonction de
`express:*`, `router`, et `router:*`.

```sh
# v4
DEBUG=express:* node index.js

# v5
DEBUG=express:*,router,router:* node index.js
```

<h3>Modifié</h3>

<h4 id="path-syntax">Syntaxe correspondante au chemin</h4>

La syntaxe correspondante au chemin d'accès est lorsqu'une chaîne de caractères est fournie comme premier paramètre pour les API `app.all()`, `app.use()`, `app.METHOD()`, `router.all()`, `router.METHOD()`, et `router.use()`. Les modifications suivantes ont été apportées à la façon dont la chaîne de chemin est associée à une requête entrante :

- Le caractère générique `*` doit avoir un nom correspondant au comportement des paramètres `:`, utilisez `/*splat` au lieu de `/*`

```js
// v4
app.get('/*', async (req, res) => {
  res.send('ok')
})

// v5
app.get('/*splat', async (req, res) => {
  res.send('ok')
})
```

{% capture note_wildcard %}
`*splat` correspond à n'importe quel chemin sans le chemin racine. Si vous avez besoin de faire correspondre le chemin racine aussi bien que `/`, vous pouvez utiliser `/{*splat}`, envelopper le joker entre parenthèses.

```js
// v5
app.get('/{*splat}', async (req, res) => {
  res.send('ok')
})
```

{% endcapture %}
{% include admonitions/note.html content=note_wildcard %}

- Le caractère optionnel `?` n'est plus pris en charge, utilisez plutôt des accolades.

```js
// v4
app.get('/:file.:ext?', async (req, res) => {
  res.send('ok')
})

// v5
app.get('/:file{.:ext}', async (req, res) => {
  res.send('ok')
})
```

- Les caractères Regexp ne sont pas pris en charge. Par exemple :

```js
app.get('/[discussion|page]/:slug', async (req, res) => {
  res.status(200).send('ok')
})
```

devrait être changé en :

```js
app.get(['/discussion/:slug', '/page/:slug'], async (req, res) => {
  res.status(200).send('ok')
})
```

- Certains caractères ont été réservés pour éviter toute confusion lors de la mise à jour (`()[]?+!`), utilisez `\` pour les échapper.
- Les noms de paramètres supportent maintenant des identifiants JavaScript valides, ou des guillemets comme `:"this"`.

<h4 id="rejected-promises">Les promesses rejetées des middleware et des gestionnaires</h4>

Les requêtes de middleware et les gestionnaires qui retournent les promesses rejetées sont maintenant gérées en renvoyant la valeur rejetée comme une `Erreur` vers le middleware. Cela signifie que l'utilisation des fonctions `async` comme middleware et des gestionnaires est plus facile que jamais. Lorsqu'une erreur est levée dans une fonction `async` ou qu'une promesse rejetée est `attendu` dans une fonction asynchrone, ces erreurs seront passées au gestionnaire d'erreurs comme si elle appelait `next(err)`.

Détail de la façon dont Express gère les erreurs est couvert dans la [documentation de gestion des erreurs](/en/guide/error-handling.html).

<h4 id="express.urlencoded">express.urlencodé</h4>

La méthode `express.urlencoded` rend l'option `extended` `false` par défaut.

<h4 id="app.listen">Écouter</h4>

Dans Express 5, la méthode `app.listen` invoquera la fonction de rappel fournie par l'utilisateur (si fournie) lorsque le serveur reçoit un événement d'erreur. Dans Express 4, de telles erreurs seraient lancées. Ce changement déplace la responsabilité de gestion des erreurs vers la fonction callback dans Express 5. S'il y a une erreur, elle sera passée au callback en tant qu'argument.
Par exemple :

```js
const server = app.listen(8080, '0.0.0.0', (error) => {
  if (error) {
    throw error // e.g. EADDRINUSE
  }
  console.log(`Listening on ${JSON.stringify(server.address())}`)
})
```

<h4 id="app.router">routeur</h4>

L'objet `app.router`, qui a été supprimé dans Express 4, a fait un retour dans Express 5. Dans la nouvelle version, cet objet est juste une référence au routeur de base Express, contrairement à Express 3, où une application devait explicitement la charger.

<h4 id="req.body">Req.body</h4> 

La propriété `req.body` retourne `undefined` quand le corps n'a pas été analysé. Dans Express 4, il retourne `{}` par défaut.

<h4 id="req.host">Hôte</h4>

Dans Express 4, la fonction `req.host` a incorrectement retiré le numéro de port si elle était présente. Dans Express 5, le numéro de port est maintenu.

<h4 id="req.query">Requête</h4>

La propriété `req.query` n'est plus une propriété accessible en écriture et est plutôt un getter. L'analyseur de requête par défaut a été changé de "étendu" à "simple".

<h4 id="res.clearCookie">Effacer les cookies</h4>

La méthode `res.clearCookie` ignore les options `maxAge` et `expires` fournies par l'utilisateur.

<h4 id="res.status">Statut</h4>

La méthode `res.status` n'accepte que les entiers de la plage de `100` à `999`, suivant le comportement défini par Node. , et retourne une erreur lorsque le code de statut n'est pas un entier.

<h4 id="res.query">res.vary</h4>

Le fichier `res.vary` lance une erreur quand l'argument `field` est manquant. Dans Express 4, si l'argument a été omis, il a donné un avertissement dans la console

### Améliorations

<h4 id="res.render">res.render()</h4>

Cette méthode impose maintenant un comportement asynchrone pour tous les moteurs de vue, en évitant les bogues causés par les moteurs de vue qui avaient une implémentation synchronisée et qui violaient l'interface recommandée.

<h4 id="brotli-support">Prise en charge de l'encodage Brotli</h4>

Express 5 prend en charge l'encodage Brotli pour les requêtes reçues des clients qui le supportent.
