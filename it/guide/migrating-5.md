---
layout: page
title: Migrazione a Express 5
description: Una guida completa per la migrazione delle applicazioni Express.js dalla versione 4 alla 5, che descrive in dettaglio i cambiamenti di rottura, i metodi deprecati e i nuovi miglioramenti.
menu: guide
lang: it
redirect_from: ""
---

# Passaggio a Express 5

<h2 id="overview">Panoramica</h2>

Express 5 non è molto diverso da Express 4; anche se mantiene la stessa API di base, ci sono ancora cambiamenti che rompono la compatibilità con la versione precedente. Pertanto, un'applicazione costruita con Express 4 potrebbe non funzionare se lo si aggiorna per utilizzare Express 5.

Per installare questa versione, è necessario avere una versione 18 o superiore. Quindi, esegui il seguente comando nella directory dell'applicazione:

```sh
npm install "express@5"
```

È quindi possibile eseguire i test automatici per vedere cosa non funziona, e risolvere i problemi in base agli aggiornamenti elencati di seguito. Dopo aver affrontato i fallimenti di test, eseguire l'app per vedere quali errori si verificano. Scoprirai subito se l'app utilizza metodi o proprietà che non sono supportati.

## Express 5 Codemods

Per aiutarti a migrare il tuo server espresso, abbiamo creato un set di codemods che ti aiuterà ad aggiornare automaticamente il tuo codice all'ultima versione di Express.

Eseguire il seguente comando per eseguire tutte le codemods disponibili:

```sh
npx @expressjs/codemod upgrade
```

Se si desidera eseguire un codice specifico, è possibile eseguire il seguente comando:

```sh
npx @expressjs/codemod name-of-the-codemod
```

Puoi trovare la lista dei codici disponibili [here](https://github.com/expressjs/codemod?tab=readme-ov-file#available-codemods).

<h2 id="changes">Modifiche in Express 5</h2>

**Metodi e proprietà rimosse**

<ul class="doclist">
  <li><a href="#app.del">app.del()</a></li>
  <li><a href="#app.param">app.param(fn)</a></li>
  <li><a href="#plural">Nomi metodo pluralizzato</a></li>
  <li><a href="#leading">Leading colon in name argument to app.param(name, fn)</a></li>
  <li><a href="#req.param">req.param(nome)</a></li>
  <li><a href="#res.json">res.json(obj, status)</a></li>
  <li><a href="#res.jsonp">res.jsonp(obj, status)</a></li>
  <li><a href="#magic-redirect">res.redirect('back') and res.location('back')</a></li>  
  <li><a href="#res.redirect">res.redirect(url, status)</a></li>
  <li><a href="#res.send.body">res.send(body, status)</a></li>
  <li><a href="#res.send.status">res.send(status)</a></li>
  <li><a href="#res.sendfile">res.sendfile()</a></li>
  <li><a href="#express.static.mime">express.static.mime</a></li>
  <li><a href="#express:router-debug-logs">express:log di debug router</a></li>
</ul>

**Modificato**

<ul class="doclist">
  <li><a href="#path-syntax">Percorso percorso corrispondente alla sintassi</a></li>
  <li><a href="#rejected-promises">Promesse respinte gestite da middleware e gestori</a></li>
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

**Miglioramenti**

<ul class="doclist">
  <li><a href="#res.render">res.render()</a></li>
  <li>Supporto di codifica <a href="#brotli-support">Brotli</a></li>
</ul>

### Metodi e proprietà rimossi

Se si utilizza uno qualsiasi di questi metodi o proprietà nella tua app, si bloccherà. Quindi, avrai bisogno di cambiare la tua app dopo l'aggiornamento alla versione 5.

<h4 id="app.del">app.del()</h4>

Express 5 non supporta più la funzione `app.del()`. Se si utilizza questa funzione, viene generato un errore. Per registrare i percorsi HTTP DELETE, utilizza invece la funzione `app.delete()`.

Inizialmente, `del` è stato usato invece di `delete`, perché `delete` è una parola chiave riservata in JavaScript. Tuttavia, come ECMAScript 6, `delete` e altre parole chiave riservate possono essere legalmente utilizzati come nomi di proprietà.

{% capture codemod-deprecated-signatures %}
Puoi sostituire le firme deprecate con il seguente comando:

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

La firma `app.param(fn)` è stata usata per modificare il comportamento della funzione `app.param(name, fn)`. È stato deprecato dal v4.11.0, e Express 5 non lo supporta più.

<h4 id="plural">Nomi dei metodi pluralizzati</h4>

I seguenti nomi di metodo sono stati pluralizzati. In Express 4, utilizzando i vecchi metodi ha prodotto un avvertimento di deprecazione. Express 5 non li supporta più:

`req.acceptsCharset()` è sostituito da `req.acceptsCharsets()`.

`req.acceptsEncoding()` è sostituito da `req.acceptsEncodings()`.

`req.acceptsLanguage()` è sostituito da `req.acceptsLanguages()`.

{% capture codemod-pluralized-methods %}
Puoi sostituire le firme deprecate con il seguente comando:

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

<h4 id="leading">Colon iniziale (:) nel nome di app.param(name, fn)</h4>

Un carattere principale (:) nel nome della `app. aram(name, fn)` function is a remnant of Express 3, and for the sake of backwards compatity, Express 4 supported it with a deprecation notice. Express 5 lo ignorerà silenziosamente e userà il parametro del nome senza prefissarlo con un colon.

Questo non dovrebbe influenzare il tuo codice se segui la documentazione Express 4 di [app.param](/{{ page.lang }}/4x/api. tml#app.param), in quanto non fa menzione del colon principale.

<h4 id="req.param">req.param(nome)</h4>

Questo metodo potenzialmente confuso e pericoloso di recupero dei dati del modulo è stato rimosso. Ora dovrai cercare in modo specifico il nome del parametro inviato nell'oggetto `req.params`, `req.body`, o `req.query`.

{% capture codemod-req-param %}
Puoi sostituire le firme deprecate con il seguente comando:

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

<h4 id="res.json">res.json(obj, status)</h4>

Express 5 non supporta più la firma `res.json(obj, status)`. Invece, impostare lo stato e poi catena il metodo `res.json()` così: `res.status(status).json(obj)`.

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

Express 5 non supporta più la firma `res.jsonp(obj, status)`. Invece, impostare lo stato e poi catena il metodo `res.jsonp()` così: `res.status(status).jsonp(obj)`.

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

<h4 id="res.redirect">res.redirect(url, status)</h4>

Express 5 non supporta più la firma `res.redirect(url, status)`. Invece, utilizzare la seguente firma: `res.redirect(status, url)`.

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

<h4 id="magic-redirect">res.redirect('back') e res.location('back')</h4>

Express 5 non supporta più la stringa magica `back` nei metodi `res.redirect()` e `res.location()`. Usa invece il valore `req.get('Referrer') <unk> <unk> '/'` per reindirizzare alla pagina precedente. In Express 4, i metodi res.`redirect('back')` e `res.location('back')` sono stati deprecati.

{% capture codemod-magic-redirect %}
Puoi sostituire le firme deprecate con il seguente comando:

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

<h4 id="res.send.body">res.send(body, status)</h4>

Express 5 non supporta più la firma `res.send(obj, status)`. Al contrario, impostare lo stato e successivamente associarlo al metodo `res.send()` come segue: `res.status(status).send(obj)`.

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

<h4 id="res.send.status">res.send(status)</h4>

Express 5 non supporta più la firma `res.send(status)`, dove `status` è un numero. Invece, utilizzare `res. endStatus(statusCode)` funzione, che imposta il codice di stato dell'intestazione della risposta HTTP e invia la versione del testo del codice: "Not Found", "Errore interno del server", e così via.
Se è necessario inviare un numero utilizzando `res. la funzione end()`, cita il numero per convertirlo in una stringa, in modo che Express non lo interpreti come un tentativo di utilizzare la vecchia firma non supportata.

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

La funzione `res.sendfile()` è stata sostituita da una versione a cassa in camme `res.sendFile()` in Express 5.

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

In Express 5, `mime` non è più una proprietà esportata del campo `static`.
Usa il pacchetto [`mime-types`](https://github.com/jshttp/mime-types) per lavorare con i valori del tipo MIME.

```js
// v4
express.static.mime.lookup('json')

// v5
const mime = require('mime-types')
mime.lookup('json')
```

<h4 id="express:router-debug-logs">express:router debug log</h4>

In Express 5, la logica di gestione del router viene eseguita da una dipendenza. Pertanto, i log di debug
per il router non sono più disponibili sotto lo spazio dei nomi `express:`.
In v4, i log erano disponibili sotto i namespace `express:router`, `express:router:layer`,
e `express:router:route`. Tutti questi sono stati inclusi nel namespace `express:*`.
In v5.1+, i log sono disponibili sotto i namespace `router`, `router:layer`, e `router:route`.
I log di `router:layer` e `router:route` sono inclusi nel namespace `router:*`.
Per ottenere lo stesso dettaglio di debug quando si utilizza `express:*` in v4, utilizzare una combinazione di
`express:*`, `router`, e `router:*`.

```sh
# v4
DEBUG=express:* node index.js

# v5
DEBUG=express:*,router,router:* node index.js
```

<h3>Modificato</h3>

<h4 id="path-syntax">Sintassi percorso corrispondente</h4>

Il percorso percorso corrispondente alla sintassi è quando una stringa viene fornita come primo parametro alle API `app.all()`, `app.use()`, `app.METHOD()`, `router.all()`, `router.METHOD()`, e `router.use()`. Sono state apportate le seguenti modifiche a come la stringa del percorso è abbinata a una richiesta in ingresso:

- Il carattere jolly `*` deve avere un nome, corrispondente al comportamento dei parametri `:`, usa `/*splat` invece di `/*`

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
`*splat` corrisponde a qualsiasi percorso senza il percorso root. Se hai bisogno di abbinare anche il percorso radice `/`, puoi usare `/{*splat}`, avvolgendo il carattere jolly nelle graffe.

```js
// v5
app.get('/{*splat}', async (req, res) => {
  res.send('ok')
})
```

{% endcapture %}
{% include admonitions/note.html content=note_wildcard %}

- Il carattere opzionale `?` non è più supportato, utilizza invece le graffe.

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

- I caratteri Regexp non sono supportati. Per esempio:

```js
app.get('/[discussion|page]/:slug', async (req, res) => {
  res.status(200).send('ok')
})
```

dovrebbe essere modificato in:

```js
app.get(['/discussion/:slug', '/page/:slug'], async (req, res) => {
  res.status(200).send('ok')
})
```

- Alcuni caratteri sono stati riservati per evitare confusione durante l'aggiornamento (`()[]?+!`), usa `\` per sfuggire a loro.
- I nomi dei parametri ora supportano identificativi JavaScript validi, o citati come `:"this"`.

<h4 id="rejected-promises">Promesse respinte gestite da middleware e gestori</h4>

Richiedi middleware e gestori che restituiscono le promesse rifiutate sono ora gestiti inoltrando il valore rifiutato come `Error` alla gestione degli errori middleware. Ciò significa che usare le funzioni `async` come middleware e manipolatori sono più facili che mai. Quando un errore viene lanciato in una funzione `async` o una promessa rifiutata è `await`ed all'interno di una funzione asincrona, questi errori verranno passati al gestore degli errori come se chiamasse `next(err)`.

Dettagli su come Express gestisce gli errori sono coperti nella [documentazione relativa alla gestione degli errori](/en/guide/error-handling.html).

<h4 id="express.urlencoded">express.urlencoded</h4>

Il metodo `express.urlencoded` rende l'opzione `extended` `false` per impostazione predefinita.

<h4 id="app.listen">app.listen</h4>

In Express 5, il metodo `app.listen` richiamerà la funzione di callback fornita dall'utente (se fornita) quando il server riceve un evento di errore. In Express 4, tali errori verrebbero lanciati. Questa modifica sposta la responsabilità di gestione degli errori alla funzione di callback in Express 5. Se c'è un errore, verrà passato al callback come argomento.
Per esempio:

```js
const server = app.listen(8080, '0.0.0.0', (error) => {
  if (error) {
    throw error // e.g. EADDRINUSE
  }
  console.log(`Listening on ${JSON.stringify(server.address())}`)
})
```

<h4 id="app.router">app.router</h4>

L'oggetto `app.router`, che è stato rimosso in Express 4, ha fatto una rimonta in Express 5. Nella nuova versione, questo oggetto è solo un riferimento al router base Express, a differenza di Express 3, dove un'app ha dovuto caricarla esplicitamente.

<h4 id="req.body">req.body</h4> 

La proprietà `req.body` restituisce `undefined` quando il corpo non è stato analizzato. In Express 4, restituisce `{}` per impostazione predefinita.

<h4 id="req.host">req.host</h4>

In Express 4, la funzione `req.host` è stata eliminata in modo errato dal numero di porta se era presente. In Express 5, il numero di porta è mantenuto.

<h4 id="req.query">req.query</h4>

La proprietà `req.query` non è più una proprietà scrivibile ed è invece un getter. Il parser di query predefinito è stato cambiato da "esteso" a "semplice".

<h4 id="res.clearCookie">res.clearCookie</h4>

Il metodo `res.clearCookie` ignora le opzioni `maxAge` e `expires` fornite dall'utente.

<h4 id="res.status">res.status</h4>

Il metodo `res.status` accetta solo interi nell'intervallo da `100` a `999`, seguendo il comportamento definito da Node. s, e restituisce un errore quando il codice di stato non è un numero intero.

<h4 id="res.query">res.vary</h4>

Il file `res.vary` lancia un errore quando manca l'argomento `field`. In Express 4, se l'argomento è stato omesso, ha dato un avviso nella console

### Miglioramenti

<h4 id="res.render">res.render()</h4>

Questo metodo ora forza il comportamento asincrono per tutti i motori di visualizzazione, evitando bug causati da motori di visualizzazione che avevano un'implementazione sincrona e che violavano l'interfaccia raccomandata.

<h4 id="brotli-support">Supporto codifica Brotli</h4>

Express 5 supporta la codifica Brotli per le richieste ricevute dai clienti che la supportano.
