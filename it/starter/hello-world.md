---
layout: page
title: Esempio espresso "Ciao Mondo"
description: Inizia con Express.js costruendo una semplice applicazione 'Ciao Mondo', dimostrando la configurazione di base e la creazione di server per i principianti.
menu: starter
lang: it
redirect_from: ""
---

# Ciao esempio mondiale

<div class="doc-box doc-info" markdown="1">
Incorporato qui sotto è essenzialmente l'app Express più semplice che puoi creare. Si tratta di un singolo file app &mdash; _non_ quello che si otterrebbe se si utilizza il [Express generator](/{{ page.lang }}/starter/generator. tml), che crea il ponteggio per un'app completa con numerosi file JavaScript, modelli Jade e sottodirectory per vari scopi.
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

Questa app avvia un server e ascolta la porta 3000 per le connessioni. L'app risponde con "Ciao Mondo!" per le richieste
all'URL radice (`/`) o _route_. Per ogni altro percorso, risponderà con un **404 non trovato**.

### Esecuzione Localmente

Crea prima una directory chiamata `myapp`, cambiala ed esegui `npm init`. Quindi, installare `express` come dipendenza, secondo la [guida all'installazione](/{{ page.lang }}/starter/installing.html).

Nella directory `myapp`, crea un file chiamato `app.js` e copia il codice dall'esempio qui sopra.

<div class="doc-box doc-notice" markdown="1">
I valori `req` (richiesta) e `res` (risposta) sono esattamente gli stessi oggetti forniti da Node, quindi è possibile richiamare
`req.pipe()`, `req.on('data', callback)` e qualsiasi cosa che si farebbe senza il coinvolgimento di Express.
</div>

Eseguire l'app con il seguente comando:

```bash
$ node app.js
```

Quindi, caricare `http://localhost:3000/` in un browser per vedere l'output.

### [Precedente: Installazione ](/{{ page.lang }}/starter/installing.html)&nbsp;&nbsp;&nbsp;&nbsp;[Next: Express Generator ](/{{ page.lang }}/starter/generator.html)
