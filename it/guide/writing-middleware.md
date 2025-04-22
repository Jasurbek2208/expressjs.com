---
layout: page
title: Scrittura middleware per l'utilizzo in applicazioni Express
description: Scopri come scrivere funzioni middleware personalizzate per le applicazioni Express.js, inclusi esempi e migliori pratiche per migliorare la gestione delle richieste e delle risposte.
menu: guide
lang: it
redirect_from: ""
---

# Scrittura middleware per l'utilizzo in applicazioni Express

<h2>Panoramica</h2>

Le funzioni _Middleware_ sono funzioni che hanno accesso al [request object](/{{ page.lang }}/4x/api. tml#req) (`req`), il [response object](/{{ page.lang }}/4x/api.html#res) (`res`), e la funzione `next` nel ciclo request-response dell'applicazione. La funzione `next` è una funzione nel router Express che, quando invocato, esegue il middleware con successo al middleware corrente.

Le funzioni Middleware possono eseguire le seguenti attività:

- Esegue qualsiasi codice.
- Effettuare modifiche alla richiesta e agli oggetti di risposta.
- Terminare il ciclo richiesta-risposta.
- Chiama il prossimo middleware nello stack.

Se la funzione middleware corrente non termina il ciclo richiesta-risposta, deve chiamare `next()` per passare il controllo alla successiva funzione middleware. In caso contrario, la richiesta sarà sospesa.

La figura seguente mostra gli elementi di una chiamata di una funzione middleware:

<table id="mw-fig">
<tbody><tr><td id="mw-fig-imgcell">
<img src="/images/express-mw.png" alt="Elements of a middleware function call" id="mw-fig-img" />
</td>
<td class="mw-fig-callouts">
<div class="callout" id="callout1">Metodo HTTP per il quale si applica la funzione middleware.</div></tbody>

<div class="callout" id="callout2">Percorso (percorso) per il quale si applica la funzione middleware.</div>

<div class="callout" id="callout3">La funzione middleware.</div>

<div class="callout" id="callout4">Argomento di richiamo alla funzione middleware, chiamato "next" per convenzione.</div>

<div class="callout" id="callout5">Argomento HTTP <a href="/{{ page.lang }}/4x/api.html#res">risposta</a> alla funzione middleware, chiamato "res" per convenzione.</div>

<div class="callout" id="callout6">HTTP <a href="/{{ page.lang }}/4x/api.html#req">richiede l'argomento</a> alla funzione middleware, chiamata "req" per convenzione.</div>
</td></tr>
</table>

A partire da Express 5, le funzioni middleware che restituiscono una Promise chiameranno `next(value)` quando rifiutano o lanciano un errore. `next` verrà chiamato con il valore rifiutato o con l'errore lanciato.

<h2>Esempio</h2>

Ecco un esempio di una semplice applicazione "Hello World" Express.
Il resto di questo articolo definirà e aggiungerà tre funzioni middleware all'applicazione:
uno chiamato `myLogger` che stampa un semplice messaggio di registro, uno chiamato `requestTime` che
visualizza il timestamp della richiesta HTTP e uno chiamato `validateCookies` che convalida i cookie in entrata.

```js
const express = require('express')
const app = express()

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(3000)
```

<h3>Funzione middleware myLogger</h3>
Ecco un semplice esempio di una funzione middleware chiamata "myLogger". Questa funzione semplicemente stampa "LOGGED" quando una richiesta all'app passa attraverso di essa. La funzione middleware è assegnata a una variabile chiamata `myLogger`.

```js
const myLogger = function (req, res, next) {
  console.log('LOGGED')
  next()
}
```

<div class="doc-box doc-notice" markdown="1">
Notare la chiamata sopra a `next()`. Chiamando questa funzione invoca la prossima funzione middleware nell'app.
La funzione `next()` non è una parte dell'API Node.js o Express, ma è il terzo argomento che viene passato alla funzione middleware. La funzione `next()` potrebbe essere chiamata qualsiasi cosa, ma per convenzione è sempre chiamata "next".
Per evitare confusione, utilizzare sempre questa convenzione.
</div>

Per caricare la funzione middleware, chiama `app.use()`, specificando la funzione middleware.
Ad esempio, il seguente codice carica la funzione middleware `myLogger` prima del percorso al percorso root (/).

```js
const express = require('express')
const app = express()

const myLogger = function (req, res, next) {
  console.log('LOGGED')
  next()
}

app.use(myLogger)

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(3000)
```

Ogni volta che l'app riceve una richiesta, stampa il messaggio "LOGGED" al terminale.

L'ordine di caricamento del middleware è importante: le funzioni middleware che vengono caricate per primo vengono eseguite per prime.

Se il file `myLogger` viene caricato dopo il percorso verso il percorso root, la richiesta non lo raggiunge mai e l'applicazione non stampa "LOGGED", perché il gestore del percorso del percorso radice termina il ciclo richiesta-risposta.

La funzione middleware `myLogger` semplicemente stampa un messaggio, poi passa la richiesta alla funzione middleware successiva nello stack chiamando la funzione `next()`.

<h3>Richiesta funzione Middleware</h3>

Successivamente, creeremo una funzione middleware chiamata "requestTime" e aggiungeremo una proprietà chiamata `requestTime`
all'oggetto richiesta.

```js
const requestTime = function (req, res, next) {
  req.requestTime = Date.now()
  next()
}
```

L'app utilizza ora la funzione middleware `requestTime`. Inoltre, la funzione callback del percorso del percorso del percorso di root utilizza la proprietà che la funzione middleware aggiunge a `req` (il oggetto richiesta).

```js
const express = require('express')
const app = express()

const requestTime = function (req, res, next) {
  req.requestTime = Date.now()
  next()
}

app.use(requestTime)

app.get('/', (req, res) => {
  let responseText = 'Hello World!<br>'
  responseText += `<small>Requested at: ${req.requestTime}</small>`
  res.send(responseText)
})

app.listen(3000)
```

Quando si effettua una richiesta alla root dell'app, l'app ora visualizza il timestamp della richiesta nel browser.

<h3>Middleware function validateCookies</h3>

Infine, creeremo una funzione middleware che convalida i cookie in arrivo e invia una risposta 400 se i cookie non sono validi.

Ecco una funzione di esempio che convalida i cookie con un servizio asincronico esterno.

```js
async function cookieValidator (cookies) {
  try {
    await externallyValidateCookie(cookies.testCookie)
  } catch {
    throw new Error('Invalid cookies')
  }
}
```

Qui utilizziamo il middleware [`cookie-parser`](/resources/middleware/cookie-parser.html) per analizzare i cookie in arrivo fuori dall'oggetto `req` e passarli alla nostra funzione `cookieValidator`. Il middleware `validateCookies` restituisce una Promessa che al momento del rifiuto attiverà automaticamente il nostro gestore di errori.

```js
const express = require('express')
const cookieParser = require('cookie-parser')
const cookieValidator = require('./cookieValidator')

const app = express()

async function validateCookies (req, res, next) {
  await cookieValidator(req.cookies)
  next()
}

app.use(cookieParser())

app.use(validateCookies)

// error handler
app.use((err, req, res, next) => {
  res.status(400).send(err.message)
})

app.listen(3000)
```

<div class="doc-box doc-notice" markdown="1">
Nota come `next()` viene chiamato dopo `await cookieValidator(req.cookies)`. Questo assicura che se `cookieValidator` si risolve, il prossimo middleware nello stack verrà chiamato. Se si trasmette qualsiasi cosa alla funzione `next()` (ad eccezione della stringa `'route'`), Express considera la richiesta corrente come se contenesse errori e ignorerà qualsiasi altra funzione middleware e routing di non gestione degli errori restante.
</div>

Poiché hai accesso all'oggetto richiesta, all'oggetto risposta, alla funzione middleware successiva nello stack, e all'intero Node. s API, le possibilità con funzioni middleware sono infinite.

Per ulteriori informazioni su Express middleware, si veda: [Using Express middleware](/{{ page.lang }}/guide/using-middleware.html).

<h2>Middleware configurabile</h2>

Se hai bisogno del tuo middleware per essere configurabile, esporta una funzione che accetta un oggetto di opzioni o altri parametri, che, poi, restituisce l'implementazione middleware in base ai parametri di input.

File: `my-middleware.js`

```js
module.exports = function (options) {
  return function (req, res, next) {
    // Implement the middleware function based on the options object
    next()
  }
}
```

Il middleware può ora essere utilizzato come mostrato di seguito.

```js
const mw = require('./my-middleware.js')

app.use(mw({ option1: '1', option2: '2' }))
```

Fare riferimento a [cookie-session](https://github.com/expressjs/cookie-session) e [compression](https://github.com/expressjs/compression) per esempi di middleware configurabile.
