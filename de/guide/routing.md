---
layout: page
title: Express-Routing
description: Lernen Sie, wie Sie Routen in Express.js Anwendungen definieren und nutzen können, einschließlich Routenmethoden, Routenpfaden, Parameter und Router für modulare Route.
menu: guide
lang: de
redirect_from: ""
---

# Routing

_Routing_ bezieht sich darauf, wie die Endpunkte einer Anwendung (URIs) auf Kundenanfragen reagieren.
Für eine Einführung in das Routing siehe [Basic routing](/{{ page.lang }}/starter/basic-routing.html).

Du definierst Routing, indem du Methoden des Express `app` Objekts verwendest, die den HTTP-Methoden entsprechen;
zum Beispiel, `app. et()` um GET-Anfragen und `app.post` zu behandeln, um POST-Anfragen zu bearbeiten. For a full list,
see [app.METHOD](/{{ page.lang }}/5x/api.html#app.METHOD). Du kannst auch [app.all()](/{{ page.lang }}/5x/api.html#app.all) verwenden, um alle HTTP-Methoden und [app.use()](/{{ page.lang }}/5x/api.html#app. se) zu
Middleware als Callback-Funktion angeben (Siehe [Middleware](/{{ page.lang }}/guide/using-middleware.html) für Details).

Diese Routing-Methoden geben eine Callback-Funktion (manchmal auch "handler functions") an, die aufgerufen wird, wenn die Anwendung eine Anfrage an die angegebene Route (Endpunkt) und die HTTP-Methode erhält. Mit anderen Worten, die Anwendung "lauscht" für Anforderungen, die mit der angegebenen Route(s) und Methode(n) übereinstimmen und wenn es ein Spiel erkennt, ruft es die angegebene Callback-Funktion auf.

In der Tat können die Routing-Methoden mehr als eine Callback-Funktion als Argumente haben.
Mit mehreren Callback-Funktionen, es ist wichtig, `next` als Argument für die Callback-Funktion zur Verfügung zu stellen und dann `next()` im Körper der Funktion aufzurufen, um die Steuerung
an den nächsten Callback zu übergeben.

Der folgende Code ist ein Beispiel für eine sehr einfache Route.

```js
const express = require('express')
const app = express()

// respond with "hello world" when a GET request is made to the homepage
app.get('/', (req, res) => {
  res.send('hello world')
})
```

<h2 id="route-methods">Routenmethoden</h2>

Eine Route-Methode wird von einer der HTTP-Methoden abgeleitet und an eine Instanz der Klasse \`express angehängt.

Der folgende Code ist ein Beispiel für Routen, die für die `GET` und die `POST` Methoden im Root der App definiert sind.

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

Express unterstützt Methoden, die allen HTTP-Anfragemethoden entsprechen: `get`, `post` und so weiter.
Für eine vollständige Liste siehe [app.METHOD](/{{ page.lang }}/5x/api.html#app.METHOD).

Es gibt eine spezielle Routing-Methode, `app.all()`, die benutzt wird, um Middleware-Funktionen an einem Pfad für _all_ HTTP-Requestmethoden zu laden. Zum Beispiel wird der folgende Handler für Anfragen an die Route `"/secret"` ausgeführt, ob `GET` verwendet wird, `POST`, `PUT`, `DELETE`, oder jede andere HTTP-Anfragemethode, die im [http module]unterstützt wird (https://nodejs.org/api/http.html#http_http_methods).

```js
app.all('/secret', (req, res, next) => {
  console.log('Accessing the secret section ...')
  next() // pass control to the next handler
})
```

<h2 id="route-paths">Routenpfade</h2>

Routenpfade in Kombination mit einer Anfragemethode definieren die Endpunkte, an denen Anfragen gestellt werden können. Routenpfade können Zeichenketten, Zeichenkettenmuster oder reguläre Ausdrücke sein.

{% capture caution-character %} Im Ausdruck 5, die Zeichen "? , `+`, `*`, `[]` und `()` werden anders behandelt als in Version 4, bitte lesen Sie die [Migrationsanleitung](/{{ page.lang }}/guide/migrating-5. tml#path-syntax) für weitere Informationen.{% endcapture %}

{% include admonitions/caution.html content=caution-character %}

{% capture note-dollar-character %}In express 4 müssen reguläre Ausdrücke wie `$` mit einem `\` maskiert werden.
{% endcapture %}

{% include admonitions/caution.html content=note-dollar-Zeichen %}

{% capture note-path-to-regexp %}
Express verwendet [path-to-regexp](https://www.npmjs.com/package/path-to-regexp) um die Routenpfade zu finden; lesen Sie die Dokumentation zu regexp für alle Möglichkeiten bei der Definition von Routenpfaden. [Express Playground Router](https://bjohansebas.github.io/playground-router/) ist ein praktisches Werkzeug zum Testen grundlegender Express-Routen, obwohl es kein Muster-Matching unterstützt.
{% endcapture %}

{% include admonitions/note.html content=note-path-to-regexp %}

{% include admonitions/warning.html content="Query strings are not part of the route path." %}

### Routenpfade basierend auf Zeichenketten

Dieser Routenpfad wird den Anfragen an die Root-Route `/` entsprechen.

```js
app.get('/', (req, res) => {
  res.send('root')
})
```

Dieser Routenpfad wird den Anfragen auf `/about` entsprechen.

```js
app.get('/about', (req, res) => {
  res.send('about')
})
```

Dieser Routenpfad entspricht den Anfragen zu `/random.text`.

```js
app.get('/random.text', (req, res) => {
  res.send('random.text')
})
```

### Routenpfade basierend auf Stringmustern

{% capture caution-string-patterns %} Die Zeichenkettenmuster in Express 5 funktionieren nicht mehr. Bitte konsultieren Sie die [Migrationsanleitung](/{{ page.lang }}/guide/migrating-5.html#path-syntax) für weitere Informationen.{% endcapture %}

{% include admonitions/caution.html content=caution-string-pattern %}

Dieser Routenpfad stimmt mit `acd` und `abcd` überein.

```js
app.get('/ab?cd', (req, res) => {
  res.send('ab?cd')
})
```

Dieser Routenpfad stimmt mit `abcd`, `abbcd`, `abbbcd` usw. überein.

```js
app.get('/ab+cd', (req, res) => {
  res.send('ab+cd')
})
```

Dieser Routenpfad stimmt mit `abcd`, `abxcd`, `abRANDOMcd`, `ab123cd` usw. überein.

```js
app.get('/ab*cd', (req, res) => {
  res.send('ab*cd')
})
```

Dieser Routenpfad stimmt mit `/abe` und `/abcde` überein.

```js
app.get('/ab(cd)?e', (req, res) => {
  res.send('ab(cd)?e')
})
```

### Routenpfade basierend auf regulären Ausdrücken

Dieser Routenpfad stimmt mit einem "a" darin überein.

```js
app.get(/a/, (req, res) => {
  res.send('/a/')
})
```

Dieser Routenpfad stimmt mit 'butterfly' und 'Drachenfly' überein, aber nicht mit 'butterflyman', 'Drachenflyman' und so weiter.

```js
app.get(/.*fly$/, (req, res) => {
  res.send('/.*fly$/')
})
```

<h2 id="route-parameters">Routenparameter</h2>

Routenparameter sind URL-Segmente, die zur Erfassung der an ihrer Position in der URL angegebenen Werte verwendet werden. Die erfassten Werte werden im Objekt `req.params` gefüllt, wobei der Name des im Pfad angegebenen Routenparameter als ihre jeweiligen Schlüssel angegeben ist.

```
Route path: /users/:userId/books/:bookId
Request URL: http://localhost:3000/users/34/books/8989
req.params: { "userId": "34", "bookId": "8989" }
```

Um Routen mit Routenparametern zu definieren, geben Sie einfach die Routenparameter im Pfad der Route, wie unten gezeigt, an.

```js
app.get('/users/:userId/books/:bookId', (req, res) => {
  res.send(req.params)
})
```

<div class="doc-box doc-notice" markdown="1">
Der Name der Routenparameter muss aus "Wortzeichen" ([A-Za-z0-9_]) bestehen.
</div>

Da die Bindestriche (`-`) und der Punkt (`.`) wörtlich interpretiert werden, können sie zusammen mit Routenparametern für nützliche Zwecke verwendet werden.

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
In express 5 werden Regexp Zeichen in Routenpfaden nicht unterstützt, für weitere Informationen lesen Sie bitte die [Migrationsanleitung](/{{ page.lang }}/guide/migrating-5.html#path-syntax).{% endcapture %}

{% include admonitions/caution.html content=warning-regexp %}

Um mehr Kontrolle über den exakten String zu haben, der mit einem Route-Parameter übereinstimmen kann, können Sie einen regulären Ausdruck in Klammern (`()`) anhängen:

```
Route path: /user/:userId(\d+)
Request URL: http://localhost:3000/user/42
req.params: {"userId": "42"}
```

{% enthalten Ermahnungen/Warnung. tml content="Da der reguläre Ausdruck normalerweise Teil eines literalen Strings ist, stelle sicher, dass du `\` Zeichen mit einem zusätzlichen Backslash maskierst, zum Beispiel `\d+`." %}

{% capture warning-version %}
In Express 4.x, <a href="https://github.com/expressjs/express/issues/2495">wird das `*` Zeichen in regulären Ausdrücken nicht auf die übliche Weise</a> interpretiert. Benutze `{0,}` anstelle von `*`. Dies wird wahrscheinlich in Express 5 behoben.
{% endcapture %}

{% include admonitions/warning.html content=warning-version %}

<h2 id="route-handlers">Routenhandler</h2>

Sie können mehrere Callback-Funktionen bereitstellen, die sich wie [middleware]verhalten (/{{ page.lang }}/guide/using-middleware.html) um eine Anfrage zu bearbeiten. Die einzige Ausnahme ist, dass diese Callbacks `next('route')` aufrufen könnten, um die restlichen Rufnummern zu umgehen. Sie können diesen Mechanismus nutzen, um Vorbedingungen auf einer Route aufzuerlegen, dann die Kontrolle an die nachfolgenden Routen übergeben, wenn es keinen Grund gibt, mit der aktuellen Route fortzufahren.

Routenhandler können in Form einer Funktion, eines Arrays von Funktionen oder Kombinationen beider sein, wie in den folgenden Beispielen gezeigt.

Eine einzelne Callback-Funktion kann eine Route handhaben. Zum Beispiel:

```js
app.get('/example/a', (req, res) => {
  res.send('Hello from A!')
})
```

Mehr als eine Callback-Funktion kann eine Route handhaben (stelle sicher, dass du das `next` Objekt angibst). Zum Beispiel:

```js
app.get('/example/b', (req, res, next) => {
  console.log('the response will be sent by the next function ...')
  next()
}, (req, res) => {
  res.send('Hello from B!')
})
```

Ein Array von Callback-Funktionen kann eine Route handhaben. Zum Beispiel:

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

Eine Kombination aus unabhängigen Funktionen und Arrays von Funktionen kann eine Route handhaben. Zum Beispiel:

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

<h2 id="response-methods">Antwortmethoden</h2>

Die Methoden auf dem Antwortobjekt (`res`) in der folgenden Tabelle können eine Antwort an den Client senden und den Request-Antwort-Zyklus beenden. Wenn keine dieser Methoden von einem Routenhandler aufgerufen wird, bleibt die Client-Anfrage hängen.

| Methode                                                                                                                                                                                                                   | Beschreibung                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| [res.download()](/{{ page.lang }}/5x/api.html#res.download)     | Fordern Sie eine Datei zum Download an.                                                                   |
| [res.end()](/{{ page.lang }}/5x/api.html#res.end)               | Beenden Sie den Antwort-Prozess.                                                                          |
| [res.json()](/{{ page.lang }}/5x/api.html#res.json)             | Sende eine JSON-Antwort.                                                                                  |
| [res.jsonp()](/{{ page.lang }}/5x/api.html#res.jsonp)           | Senden Sie eine JSON-Antwort mit JSONP-Unterstützung.                                                     |
| [res.redirect()](/{{ page.lang }}/5x/api.html#res.redirect)     | Anfrage umleiten.                                                                                         |
| [res.render()](/{{ page.lang }}/5x/api.html#res.render)         | Ansichtsvorlage ausblenden.                                                                               |
| [res.send()](/{{ page.lang }}/5x/api.html#res.send)             | Senden Sie eine Antwort von verschiedenen Typen.                                                          |
| [res.sendFile()](/{{ page.lang }}/5x/api.html#res.sendFile)     | Senden Sie eine Datei als octet-Stream.                                                                   |
| [res.sendStatus()](/{{ page.lang }}/5x/api.html#res.sendStatus) | Legen Sie den Antwort-Statuscode fest und senden Sie seine Zeichenfolge Repräsentation als Antwortkörper. |

<h2 id="app-route">app.route()</h2>

Sie können verkettende Routenhandler für einen Routenpfad erstellen, indem Sie `app.route()` verwenden.
Da der Weg an einem einzigen Ort angegeben wird, ist die Schaffung modularer Routen hilfreich, ebenso wie die Reduzierung von Redundanz und Typos. Für weitere Informationen über Routen siehe: [Router() documentation](/{{ page.lang }}/5x/api.html#router).

Hier ist ein Beispiel für verkettete Routenhandler, die mit `app.route()` definiert werden.

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

Verwende die Klasse `express.Router`, um modulare mountbare Routenhandler zu erstellen. Eine `Router`-Instanz ist ein komplettes Middleware- und Routing-System; aus diesem Grund wird sie oft als "Mini-App" bezeichnet.

Das folgende Beispiel erzeugt einen Router als Modul, lädt eine Middleware-Funktion darin definiert einige Routen und mountet das Router-Modul auf einem Pfad in der Hauptanwendung.

Erstelle eine Router-Datei namens `birds.js` im App-Verzeichnis, mit folgendem Inhalt:

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

Laden Sie dann das Router-Modul in der App:

```js
const birds = require('./birds')

// ...

app.use('/birds', birds)
```

Die App wird nun in der Lage sein, Anfragen an `/birds` und `/birds/about` zu bearbeiten, aufrufen sowie die Middleware-Funktion `timeLog` aufrufen, die spezifisch für die Route ist.

Aber wenn die übergeordnete Route `/birds` Pfadparameter hat, wird sie standardmäßig nicht von den Unterrouten aus erreichbar sein. Um es zugänglich zu machen, müssen Sie die Option `mergeParams` an den Router-Konstruktor [reference](/{{ page.lang }}/5x/api.html#app.use) übergeben.

```js
const router = express.Router({ mergeParams: true })
```
