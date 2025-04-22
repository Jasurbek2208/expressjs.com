---
layout: page
title: Installazione Di Express
description: Scopri come installare Express.js nel tuo ambiente Node.js, inclusa la creazione della directory del progetto e la gestione delle dipendenze con npm.
menu: starter
lang: it
redirect_from: ""
---

# Installazione

Supponendo che tu abbia già installato [Node.js](https://nodejs.org/), crea una directory per tenere premuta la tua applicazione, e crea la tua directory di lavoro.

- [Express 4.x](/{{ page.lang }}/4x/api.html) richiede Node.js 0.10 o superiore.
- [Express 5.x](/{{ page.lang }}/5x/api.html) richiede Node.js 18 o superiore.

```bash
$ mkdir myapp
$ cd myapp
```

Usa il comando `npm init` per creare un file `package.json` per la tua applicazione.
Per maggiori informazioni sul funzionamento di `package.json`, vedere [Specifiche della gestione di npm.json](https://docs.npmjs.com/files/package.json).

```bash
$ npm init
```

Questo comando ti richiede un certo numero di cose, come il nome e la versione della tua applicazione.
Per ora, puoi semplicemente premere RETURN per accettare i valori predefiniti per la maggior parte di essi, con la seguente eccezione:

```
entry point: (index.js)
```

Inserisci `app.js`, o qualsiasi cosa desideri che sia il nome del file principale. Se vuoi che sia `index.js`, premi RETURN per accettare il nome del file predefinito suggerito.

Ora, installa Express nella directory `myapp` e salvalo nella lista delle dipendenze. Per esempio:

```bash
$ npm install express
```

Per installare Express temporaneamente e non aggiungerlo alla lista delle dipendenze:

```bash
$ npm install express --no-save
```

<div class="doc-box doc-info" markdown="1">
Per impostazione predefinita con la versione npm 5.0+, `npm install` aggiunge il modulo alla lista `dependencies` nel `package. file son`; con versioni precedenti di npm, è necessario specificare esplicitamente l'opzione `--save`. Poi, in seguito, l'esecuzione di `npm install` nella directory dell'app installerà automaticamente i moduli nell'elenco delle dipendenze.
</div>

### [Successivo: Ciao Mondo ](/{{ page.lang }}/starter/hello-world.html)