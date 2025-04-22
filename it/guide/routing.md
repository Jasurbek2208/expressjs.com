---
layout: page
title: Instradamento rapido
description: Scopri come definire e utilizzare i percorsi nelle applicazioni Express.js, inclusi i metodi di percorso, i percorsi e i parametri e utilizzando Router per il routing modulare.
menu: guide
lang: it
redirect_from: ""
---

# Routing

_Routing_ si riferisce a come gli endpoint di un'applicazione (URI) rispondono alle richieste del client.
Per un'introduzione al routing, vedere [routing base](/{{ page.lang }}/starter/basic-routing.html).

Definisci il routing usando metodi dell'oggetto `app` Express che corrispondono ai metodi HTTP;
per esempio, `app. et()` per gestire le richieste GET e `app.post` per gestire le richieste POST. Per una lista completa,
vedi [app.METHOD](/{{ page.lang }}/5x/api.html#app.METHOD). Puoi anche usare [app.all()](/{{ page.lang }}/5x/api.html#app.all) per gestire tutti i metodi HTTP e [app.use()](/{{ page.lang }}/5x/api.html#app. se) a
specificare middleware come funzione callback (Vedi [Using middleware](/{{ page.lang }}/guide/using-middleware.html) per i dettagli).

Questi metodi di routing specificano una funzione di callback (a volte chiamata "funzioni di handler") chiamata quando l'applicazione riceve una richiesta al percorso specificato (endpoint) e il metodo HTTP. In altre parole, l'applicazione "ascolta" per le richieste che corrispondono ai percorsi e ai metodi specificati, e quando rileva una corrispondenza, chiama la funzione di callback specificata.

Infatti, i metodi di routing possono avere più di una funzione di callback come argomenti.
Con funzioni di callback multiple, è importante fornire `next` come argomento alla funzione di callback e poi chiamare `next()` all'interno del corpo della funzione per consegnare il controllo
al prossimo callback.

Il seguente codice è un esempio di un percorso molto basilare.

```js
const express = require('express')
const app = express()

// respond with "hello world" when a GET request is made to the homepage
app.get('/', (req, res) => {
  res.send('hello world')
})
```

<h2 id="route-methods">Metodi percorso</h2>

Un metodo di percorso è derivato da uno dei metodi HTTP ed è collegato ad un'istanza della classe `express`.

Il seguente codice è un esempio di percorsi definiti per il `GET` e i metodi `POST` nella root dell'app.

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

Express supporta metodi che corrispondono a tutti i metodi di richiesta HTTP: `get`, `post`, e così via.
Per una lista completa, vedere [app.METHOD](/{{ page.lang }}/5x/api.html#app.METHOD).

C'è un metodo di routing speciale, `app.all()`, utilizzato per caricare le funzioni middleware in un percorso per _tutti_ i metodi di richiesta HTTP. Ad esempio, il seguente gestore viene eseguito per le richieste al percorso `"/secret"` se si utilizza `GET`, `POST`, `PUT`, `DELETE`, o qualsiasi altro metodo di richiesta HTTP supportato nel [modulo http](https://nodejs.org/api/http.html#http_http_methods).

```js
app.all('/secret', (req, res, next) => {
  console.log('Accessing the secret section ...')
  next() // pass control to the next handler
})
```

<h2 id="route-paths">Percorsi di rotta</h2>

Percorsi di percorso, in combinazione con un metodo di richiesta, definire gli endpoint in cui le richieste possono essere fatte. I tracciati del percorso possono essere stringhe, motivi di stringa o espressioni regolari.

{% capture caution-character %} In express 5, i caratteri `? , `+`, `\*`, `[]`, e `()\` sono gestiti in modo diverso rispetto alla versione 4, si prega di rivedere la [guida alla migrazione](/{{ page.lang }}/guide/migrating-5. tml#path-syntax) per ulteriori informazioni.{% endcapture %}

{% include admonitions/caution.html content=caution-character %}

{% capture note-dollar-character %}In express 4, i caratteri di espressione regolare come `$` devono essere fuggiti con un `\`.
{% endcapture %}

{% include admonitions/caution.html content=note-dollar-character %}

{% capture note-path-to-regexp %}
Express utilizza [path-to-regexp](https://www.npmjs.com/package/path-to-regexp) per abbinare i percorsi del percorso; vedere la documentazione path-to-regexp per tutte le possibilità di definire i percorsi del percorso. [Express Playground Router](https://bjohansebas.github.io/playground-router/) è uno strumento utile per testare le rotte Express di base, anche se non supporta la corrispondenza dei modelli.
{% endcapture %}

{% include admonitions/note.html content=note-path-to-regexp %}

{% include admonitions/warning.html content="Le stringhe di query non fanno parte del percorso del percorso." %}

### Percorsi di percorso basati su stringhe

Questo percorso corrisponderà alle richieste del percorso root, `/`.

```js
app.get('/', (req, res) => {
  res.send('root')
})
```

Questo percorso corrisponderà alle richieste di `/about`.

```js
app.get('/about', (req, res) => {
  res.send('about')
})
```

Questo percorso corrisponderà alle richieste a `/random.text`.

```js
app.get('/random.text', (req, res) => {
  res.send('random.text')
})
```

### Percorsi del percorso in base ai motivi delle stringhe

{% capture caution-string-patterns %} I modelli di stringhe in Express 5 non funzionano più. Per maggiori informazioni fare riferimento alla [guida alla migrazione](/{{ page.lang }}/guide/migrating-5.html#path-syntax).{% endcapture %}

{% include admonitions/caution.html content=caution-string-patterns %}

Questo percorso corrisponde a `acd` e `abcd`.

```js
app.get('/ab?cd', (req, res) => {
  res.send('ab?cd')
})
```

Questo percorso corrisponderà a `abcd`, `abbcd`, `abbbcd`, e così via.

```js
app.get('/ab+cd', (req, res) => {
  res.send('ab+cd')
})
```

Questo percorso corrisponde a `abcd`, `abxcd`, `abRANDOMcd`, `ab123cd`, e così via.

```js
app.get('/ab*cd', (req, res) => {
  res.send('ab*cd')
})
```

Questo percorso corrisponde a `/abe` e `/abcde`.

```js
app.get('/ab(cd)?e', (req, res) => {
  res.send('ab(cd)?e')
})
```

### Percorsi di percorso basati su espressioni regolari

Questo percorso corrisponderà a qualsiasi cosa con una "a" in esso.

```js
app.get(/a/, (req, res) => {
  res.send('/a/')
})
```

Questo percorso corrisponde a `butterfly` e `dragonfly`, ma non a `butterflyman`, `dragonflyman`, e così via.

```js
app.get(/.*fly$/, (req, res) => {
  res.send('/.*fly$/')
})
```

<h2 id="route-parameters">Parametri percorso</h2>

I parametri del percorso sono denominati segmenti di URL che vengono utilizzati per catturare i valori specificati nella loro posizione nell'URL. I valori catturati sono popolati nell'oggetto `req.params`, con il nome del parametro route specificato nel percorso come loro rispettive chiavi.

```
Route path: /users/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userId": "34", "bookId": "8989" }
```

Per definire i percorsi con i parametri del percorso, è sufficiente specificare i parametri del percorso nel percorso come mostrato di seguito.

```js
app.get('/users/:userId/books/:bookId', (req, res) => {
  res.send(req.params)
})
```

<div class="doc-box doc-notice" markdown="1">
Il nome dei parametri del percorso deve essere composto da "caratteri di parola" ([A-Za-z0-9_]).
</div>

Poiché il trattino (`-`) e il punto (`.`) sono interpretati letteralmente, possono essere utilizzati insieme ai parametri del percorso per scopi utili.

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
Nell'espresso 5, i caratteri Regexp non sono supportati nei percorsi percorso, per ulteriori informazioni si prega di fare riferimento alla [guida alla migrazione](/{{ page.lang }}/guide/migrating-5.html#path-syntax).{% endcapture %}

{% include admonitions/caution.html content=warning-regexp %}

Per avere più controllo sulla stringa esatta che può essere abbinata a un parametro del percorso, puoi aggiungere un'espressione regolare tra parentesi (`()`):

```
Route path: /user/:userId(\d+)
Request URL: http://localhost:3000/user/42
req.params: {"userId": "42"}
```

{% include ammonizioni/avvertimento. tml content="Poiché l'espressione regolare è solitamente parte di una stringa letterale, assicurati di sfuggire a qualsiasi carattere `\` con un backslash aggiuntivo, ad esempio `\\d+`." %}

{% capture warning-version %}
In Express 4.x, <a href="https://github.com/expressjs/express/issues/2495">il carattere `*` nelle espressioni regolari non viene interpretato nel modo usuale</a>. Come soluzione puoi usare `{0,}` invece di `*`. Questo sarà probabilmente fissato in Express 5.
{% endcapture %}

{% include admonitions/warning.html content=warning-version %}

<h2 id="route-handlers">Gestori del percorso</h2>

Puoi fornire più funzioni di callback che si comportano come [middleware](/{{ page.lang }}/guide/using-middleware.html) per gestire una richiesta. L'unica eccezione è che questi callback potrebbero invocare `next('route')` per bypassare i rimanenti callback del percorso. È possibile utilizzare questo meccanismo per imporre condizioni preliminari su un percorso, poi passare il controllo ai percorsi successivi se non c'è motivo di procedere con il percorso corrente.

I gestori del percorso possono essere nella forma di una funzione, una serie di funzioni, o combinazioni di entrambi, come mostrato negli esempi seguenti.

Una singola funzione di callback può gestire un percorso. Per esempio:

```js
app.get('/example/a', (req, res) => {
  res.send('Hello from A!')
})
```

Più di una funzione di callback può gestire un percorso (assicurati di specificare l'oggetto `next`). Per esempio:

```js
app.get('/example/b', (req, res, next) => {
  console.log('the response will be sent by the next function ...')
  next()
}, (req, res) => {
  res.send('Hello from B!')
})
```

Un array di funzioni di callback può gestire un percorso. Per esempio:

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

Una combinazione di funzioni indipendenti e matrici di funzioni può gestire un percorso. Per esempio:

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

<h2 id="response-methods">Metodi di risposta</h2>

I metodi sull'oggetto di risposta (`res`) nella tabella seguente possono inviare una risposta al client e terminare il ciclo di richiesta-risposta. Se nessuno di questi metodi è chiamato da un gestore del percorso, la richiesta del cliente sarà sospesa.

| Metodo                                                                                                                                                                                                                    | Descrizione                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| [res.download()](/{{ page.lang }}/5x/api.html#res.download)     | Avverte un file da scaricare.                                                                                      |
| [res.end()](/{{ page.lang }}/5x/api.html#res.end)               | Termina il processo di risposta.                                                                                   |
| [res.json()](/{{ page.lang }}/5x/api.html#res.json)             | Invia una risposta JSON.                                                                                           |
| [res.jsonp()](/{{ page.lang }}/5x/api.html#res.jsonp)           | Invia una risposta JSON con il supporto JSONP.                                                                     |
| [res.redirect()](/{{ page.lang }}/5x/api.html#res.redirect)     | Reindirizza una richiesta.                                                                                         |
| [res.render()](/{{ page.lang }}/5x/api.html#res.render)         | Render un modello di visualizzazione.                                                                              |
| [res.send()](/{{ page.lang }}/5x/api.html#res.send)             | Invia una risposta di vari tipi.                                                                                   |
| [res.sendFile()](/{{ page.lang }}/5x/api.html#res.sendFile)     | Invia un file come un flusso di otte.                                                                              |
| [res.sendStatus()](/{{ page.lang }}/5x/api.html#res.sendStatus) | Imposta il codice di stato della risposta e invia la sua rappresentazione della stringa come corpo della risposta. |

<h2 id="app-route">app.route()</h2>

È possibile creare i gestori di rotte per un percorso utilizzando `app.route()`.
Poiché il percorso è specificato in una singola posizione, è utile creare percorsi modulari, così come ridurre la ridondanza e pneumatici. Per ulteriori informazioni sulle rotte, si veda: [Router() documentation](/{{ page.lang }}/5x/api.html#router).

Ecco un esempio di router incatenati che sono definiti utilizzando `app.route()`.

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

<h2 id="express-router">express.Router</h2>

Usa la classe `express.Router` per creare i gestori modulari e montabili. Un'istanza `Router` è un sistema di routing e middleware completo; per questo motivo è spesso chiamata "mini-app".

L'esempio seguente crea un router come modulo, carica una funzione middleware in esso, definisce alcuni percorsi e monta il modulo del router su un percorso nell'app principale.

Crea un file router chiamato `birds.js` nella directory delle app, con il seguente contenuto:

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

Quindi, caricare il modulo router nell'app:

```js
const birds = require('./birds')

// ...

app.use('/birds', birds)
```

L'app sarà ora in grado di gestire le richieste di `/birds` e `/birds/about`, oltre a chiamare la funzione middleware `timeLog` che è specifica per il percorso.

Ma se il percorso principale `/birds` ha parametri di percorso, non sarà accessibile per impostazione predefinita dai sotto-percorsi. Per renderlo accessibile, dovrai passare l'opzione `mergeParams` al costruttore Router [reference](/{{ page.lang }}/5x/api.html#app.use).

```js
const router = express.Router({ mergeParams: true })
```
