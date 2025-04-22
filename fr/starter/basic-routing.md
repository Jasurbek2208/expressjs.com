---
layout: page
title: Routage de base express
description: Apprenez les fondamentaux du routage dans les applications Express.js, y compris comment définir des routes, gérer des méthodes HTTP et créer des gestionnaires de routes pour votre serveur web.
menu: starter
lang: fr
redirect_from: ""
---

# Routage de base

_Routing_ désigne la façon dont une application répond à une requête client à un point de terminaison particulier, qui est une URI (ou un chemin) et une méthode spécifique de requête HTTP (GET, POST, etc.).

Chaque route peut avoir une ou plusieurs fonctions de gestionnaire, qui sont exécutées lorsque la route est correspondante.

La définition de la route prend la structure suivante :

```js
app.METHOD(PATH, HANDLER)
```

Où :

- `app` est une instance de `express`.
- `METHOD` est une [méthode de requête HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods), en minuscule.
- `PATH` est un chemin sur le serveur.
- `HANDLER` est la fonction exécutée lorsque la route est correspondante.

<div class="doc-box doc-notice" markdown="1">
Ce tutoriel suppose qu'une instance de `express` nommée `app` est créée et que le serveur est en cours d'exécution. Si vous n'êtes pas familier avec la création d'une application et son démarrage, consultez [Hello world example](/{{ page.lang }}/starter/hello-world.html).
</div>

Les exemples suivants illustrent la définition de routes simples.

Répondez avec `Hello World!` sur la page d'accueil:

```js
app.get('/', (req, res) => {
  res.send('Hello World!')
})
```

Répondre à la requête POST sur la route racine (`/`), la page d'accueil de l'application :

```js
app.post('/', (req, res) => {
  res.send('Got a POST request')
})
```

Répondre à une requête PUT sur la route `/user`:

```js
app.put('/user', (req, res) => {
  res.send('Got a PUT request at /user')
})
```

Répondre à une requête DELETE sur la route `/user`:

```js
app.delete('/user', (req, res) => {
  res.send('Got a DELETE request at /user')
})
```

Pour plus de détails sur le routage, consultez le [guide de routage](/{{ page.lang }}/guide/routing.html).

### [Précédent : Générateur d'application Express ](/{{ page.lang }}/starter/generator.html)&nbsp;&nbsp;&nbsp;&nbsp;[Suivant : Servir des fichiers statiques dans Express ](/{{ page.lang }}/starter/static-files.html)