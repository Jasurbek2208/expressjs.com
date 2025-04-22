---
layout: page
title: Exemple Express "Hello World"
description: Commencez avec Express.js en construisant une simple application 'Hello World', en démontrant la configuration de base et la création de serveurs pour les débutants.
menu: starter
lang: fr
redirect_from: ""
---

# Bonjour l'exemple du monde

<div class="doc-box doc-info" markdown="1">
Intégré ci-dessous est essentiellement l'application Express la plus simple que vous puissiez créer. C'est une application de fichier unique &mdash; _pas_ ce que vous obtiendrez si vous utilisez le [générateur Express](/{{ page.lang }}/starter/generator. tml), qui crée l'échafaudage pour une application complète avec de nombreux fichiers JavaScript, des modèles Jade et des sous-répertoires pour divers usages.
</div>

```js
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```

Cette application démarre un serveur et écoute le port 3000 pour les connexions. L'application répond avec "Hello World!" pour les demandes
à l'URL racine (`/`) ou _route_. Pour tous les autres chemins, il répondra avec un **404 Not Found**.

### Exécution locale

Créez d'abord un répertoire nommé `myapp`, changez et exécutez `npm init`. Ensuite, installez `express` en tant que dépendance, conformément au [guide d'installation](/{{ page.lang }}/starter/installing.html).

Dans le dossier `myapp`, créez un fichier nommé `app.js` et copiez le code à partir de l'exemple ci-dessus.

<div class="doc-box doc-notice" markdown="1">
Les `req` (request) et `res` (response) sont les mêmes objets que Node fournit, donc vous pouvez appeler
`req. ipe()`, `req.on('data', callback)`, et tout autre chose que vous feriez sans Express impliqué.
</div>

Exécutez l'application avec la commande suivante :

```bash
$ node app.js
```

Ensuite, chargez `http://localhost:3000/` dans un navigateur pour voir la sortie.

### [Précédent : Installation](/{{ page.lang }}/starter/installing.html)&nbsp;&nbsp;&nbsp;&nbsp;[Next: Express Generator ](/{{ page.lang }}/starter/generator.html)
