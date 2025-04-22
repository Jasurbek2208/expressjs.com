---
layout: page
title: Installation Express
description: Apprenez à installer Express.js dans votre environnement Node.js, y compris la configuration de votre répertoire de projet et la gestion des dépendances avec npm.
menu: starter
lang: fr
redirect_from: ""
---

# Installation en cours

En supposant que vous ayez déjà installé [Node.js](https://nodejs.org/), créez un répertoire pour conserver votre application et faites de celui-ci votre répertoire de travail.

- [Express 4.x](/{{ page.lang }}/4x/api.html) nécessite Node.js 0.10 ou supérieur.
- [Express 5.x](/{{ page.lang }}/5x/api.html) nécessite Node.js 18 ou plus.

```bash
$ mkdir myapp
$ cd myapp
```

Utilisez la commande `npm init` pour créer un fichier `package.json` pour votre application.
Pour plus d'informations sur le fonctionnement de `package.json`, voir [Specifics of npm's package.json handling](https://docs.npmjs.com/files/package.json).

```bash
$ npm init
```

Cette commande vous invite à trouver un certain nombre de choses, telles que le nom et la version de votre application.
Pour l'instant, vous pouvez simplement appuyer sur RETURN pour accepter les valeurs par défaut pour la plupart d'entre eux, à l'exception de la règle suivante :

```
entry point: (index.js)
```

Entrez `app.js`, ou quel que soit le nom du fichier principal. Si vous voulez qu'il soit `index.js`, appuyez sur RETURN pour accepter le nom de fichier par défaut suggéré.

Maintenant, installez Express dans le répertoire `myapp` et sauvegardez-le dans la liste des dépendances. Par exemple :

```bash
$ npm install express
```

Pour installer Express temporairement et ne pas l'ajouter à la liste des dépendances :

```bash
$ npm install express --no-save
```

<div class="doc-box doc-info" markdown="1">
Par défaut avec la version npm 5.0+, `npm install` ajoute le module à la liste `dependencies` du paquet. son`; avec les versions antérieures de npm, vous devez spécifier explicitement l'option `--save` . Puis, par la suite, exécuter `npm install` dans le répertoire de l'application installera automatiquement les modules dans la liste des dépendances.
</div>

### [Suivant : Bonjour Monde](/{{ page.lang }}/starter/hello-world.html)