---
layout: page
title: Migration zu Express 5
description: Eine umfassende Anleitung zur Migration Ihrer Express.js-Anwendungen von Version 4 auf 5, die aufwändige Änderungen, veraltete Methoden und neue Verbesserungen enthält.
menu: guide
lang: de
redirect_from: ""
---

# Umzug nach Express 5

<h2 id="overview">Übersicht</h2>

Express 5 unterscheidet sich nicht sehr von Express 4; obwohl es die gleiche grundlegende API hat, gibt es immer noch Änderungen, die die Kompatibilität mit der vorherigen Version stören. Daher könnte eine Anwendung mit Express 4 nicht funktionieren, wenn Sie sie auf Express 5 aktualisieren.

Um diese Version zu installieren, benötigen Sie eine Node.js Version 18 oder höher. Führen Sie dann den folgenden Befehl in Ihrem Anwendungsverzeichnis aus:

```sh
npm install "express@5"
```

Sie können dann Ihre automatisierten Tests durchführen, um zu sehen, was fehlschlägt, und Probleme gemäß den unten aufgeführten Updates beheben. Nach dem Beheben von Testfehlern führen Sie Ihre App aus, um zu sehen, welche Fehler auftreten. Sie werden sofort erfahren, ob die App Methoden oder Eigenschaften verwendet, die nicht unterstützt werden.

## Express 5 Codemoden

Um Ihnen zu helfen, Ihren Expressserver zu migrieren Wir haben eine Reihe von Codemods erstellt, die Ihnen helfen, Ihren Code automatisch auf die neueste Version von Express zu aktualisieren.

Führen Sie den folgenden Befehl aus, um alle verfügbaren Codemods auszuführen:

```sh
npx @expressjs/codemod upgrade
```

Wenn du eine bestimmte Codemod ausführen möchtest, kannst du folgenden Befehl ausführen:

```sh
npx @expressjs/codemod name-of-the-codemod
```

Du findest die Liste der verfügbaren Codemoden [here](https://github.com/expressjs/codemod?tab=readme-ov-file#available-codemods).

<h2 id="changes">Änderungen in Express 5</h2>

**Entfernte Methoden und Eigenschaften**

<ul class="doclist">
  <li><a href="#app.del">app.del()</a></li>
  <li><a href="#app.param">app.param(fn)</a></li>
  <li><a href="#plural">Pluralisierte Methodennamen</a></li>
  <li><a href="#leading">Führe Doppelpunkt im Namensargument zu app.param(name, fn)</a></li>
  <li><a href="#req.param">req.param(name)</a></li>
  <li><a href="#res.json">res.json(obj, status)</a></li>
  <li><a href="#res.jsonp">res.jsonp(obj, status)</a></li>
  <li><a href="#magic-redirect">res.redirect('back') und res.location('back')</a></li>  
  <li><a href="#res.redirect">res.redirect(url, status)</a></li>
  <li><a href="#res.send.body">res.send(Körper, Status)</a></li>
  <li><a href="#res.send.status">res.send(status)</a></li>
  <li><a href="#res.sendfile">res.sendfile()</a></li>
  <li><a href="#express.static.mime">express.static.mime</a></li>
  <li><a href="#express:router-debug-logs">Express:Router Debug Logs</a></li>
</ul>

**Geändert**

<ul class="doclist">
  <li><a href="#path-syntax">Pfad-Routenpassender Syntax</a></li>
  <li><a href="#rejected-promises">abgelehnte Versprechungen von Middleware und Handler</a></li>
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

**Verbesserungen**

<ul class="doclist">
  <li><a href="#res.render">res.render()</a></li>
  <li><a href="#brotli-support">Brotli Kodierungsunterstützung</a></li>
</ul>

### Entfernte Methoden und Eigenschaften

Wenn du eine dieser Methoden oder Eigenschaften in deiner App verwendest, stürzt sie ab. Also müssen Sie Ihre App nach dem Update auf Version 5 ändern.

<h4 id="app.del">app.del()</h4>

Express 5 unterstützt nicht mehr die `app.del()` Funktion. Wenn Sie diese Funktion verwenden, wird ein Fehler geworfen. Um HTTP DELETE Routen zu registrieren, benutze stattdessen die `app.delete()` Funktion.

Anfangs wurde `del` anstelle von `delete` verwendet, da `delete` ein reserviertes Schlüsselwort in JavaScript ist. Jedoch können ECMAScript 6, `delete` und andere reservierte Schlüsselwörter legal als Eigenschaftsnamen verwendet werden.

{% capture codemod-deprecated-signatures %}
Sie können die veralteten Signaturen durch folgenden Befehl ersetzen:

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

Die Signatur `app.param(fn)` wurde verwendet, um das Verhalten der `app.param(name, fn)` Funktion zu ändern. Es ist seit v4.11.0 veraltet und Express 5 unterstützt es überhaupt nicht mehr.

<h4 id="plural">Pluralisierte Methodennamen</h4>

Die folgenden Methodennamen wurden pluralisiert. In Express 4 führte die Verwendung der alten Methoden zu einer Deprecation Warnung. Express 5 unterstützt sie nicht mehr:

`req.acceptsCharset()` wird durch `req.acceptsCharsets()` ersetzt.

`req.acceptsEncoding()` wird durch `req.acceptsEncodings()` ersetzt.

`req.acceptsLanguage()` wird durch `req.acceptsLanguages()` ersetzt.

{% capture codemod-pluralized-methods %}
Sie können die veralteten Signaturen durch folgenden Befehl ersetzen:

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

<h4 id="leading">Führender Doppelpunkt (:) im Namen von app.param(name, fn)</h4>

Ein führendes Doppelzeichen (:) im Namen der `app. aram(name, fn)` Funktion ist ein Überbleibsel von Express 3, und um der Abwärtskompatibilität willen hat Express 4 sie mit einer Veraltungsmeldung unterstützt. Express 5 ignoriert es stillschweigend und verwendet den Namensparameter, ohne ihn mit einem Doppelpunkt zu präfixieren.

Dies sollte Ihren Code nicht beeinflussen, wenn Sie die Express 4 Dokumentation von [app.param](/{{ page.lang }}/4x/api. tml#app.param), da es keine Erwähnung des führenden Doppelpunkts gibt.

<h4 id="req.param">req.param(Name)</h4>

Diese potenziell verwirrende und gefährliche Methode zum Abrufen von Formulardaten wurde entfernt. Sie müssen nun gezielt nach dem übermittelten Parameternamen im `req.params`, `req.body` oder `req.query` Objekt suchen.

{% capture codemod-req-param %}
Sie können die veralteten Signaturen durch folgenden Befehl ersetzen:

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

<h4 id="res.json">res.json(obj, Status)</h4>

Express 5 unterstützt nicht mehr die Signatur `res.json(obj, status)`. Setze stattdessen den Status und verkette ihn auf die Methode `res.json()` wie folgt: `res.status(status).json(obj)`.

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

Express 5 unterstützt nicht mehr die Signatur `res.jsonp(obj, status)`. Setze stattdessen den Status und verkette ihn auf die `res.jsonp()` Methode wie folgt: `res.status(status).jsonp(obj)`.

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

<h4 id="res.redirect">res.redirect(url, Status)</h4>

Express 5 unterstützt nicht mehr die Signatur `res.redirect(url, status)`. Verwenden Sie stattdessen die folgende Signatur: `res.redirect(status, url)`.

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

<h4 id="magic-redirect">res.redirect('back') und res.location('back')</h4>

Express 5 unterstützt nicht mehr den magischen String `back` in den Methoden `res.redirect()` und `res.location()`. Verwenden Sie stattdessen den `req.get('Referrer') || '/'` Wert, um zurück zur vorherigen Seite zu leiten. In Express 4 wurden die Methoden res.`redirect('back')` und `res.location('back')` veraltet.

{% capture codemod-magic-redirect %}
Sie können die veralteten Signaturen durch folgenden Befehl ersetzen:

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

<h4 id="res.send.body">res.send(Körper, Status)</h4>

Express 5 unterstützt die Signatur `res.send(obj, status)` nicht mehr. Stattdessen müssen Sie den Status festlegen und diesen dann mit `res.send()`-Methoden wie  dieser verketten: `res.status(status).send(obj)`.

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

<h4 id="res.send.status">res.send(Status)</h4>

Express 5 unterstützt nicht mehr die Signatur `res.send(status)`, wobei `status` eine Zahl ist. Verwenden Sie stattdessen die `res. endStatus(statusCode)` Funktion, die den HTTP-Antwort-Header-Statuscode setzt und die Textversion des Codes sendet: "Nicht gefunden", "Interner Server-Fehler", und so weiter.
Wenn Sie eine Nummer mit Hilfe der `res senden müssen. end()` Funktion, zitiert die Zahl, um sie in einen String zu konvertieren, so dass Express es nicht als Versuch interpretiert, die nicht unterstützte alte Signatur zu verwenden.

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

Die `res.sendfile()` Funktion wurde durch eine camel-cased Version `res.sendFile()` in Express 5 ersetzt.

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

In Express 5 ist `mime` nicht mehr eine exportierte Eigenschaft des `static` Feldes.
Benutze das [`mime-types` package](https://github.com/jshttp/mime-types), um mit MIME Werte zu arbeiten.

```js
// v4
express.static.mime.lookup('json')

// v5
const mime = require('mime-types')
mime.lookup('json')
```

<h4 id="express:router-debug-logs">express:router Debug-Logs</h4>

In Express 5 wird die Router-Handhabungslogik durch eine Abhängigkeit ausgeführt. Daher sind die
Debug-Logs für den Router nicht mehr unter dem `express :` Namensraum verfügbar.
In v4 waren die Protokolle unter den Namensräumen `express:router`, `express:router:layer`,
und `express:router:route` verfügbar. Alle diese wurden unter den Namensraum `express:*` aufgenommen.
In v5.1+ sind die Logs unter den Namensräumen `router`, `router:layer` und `router:route` verfügbar.
Die Logs von `router:layer` und `router:route` sind im Namensraum `router:*` enthalten.
Um das selbe Detail der Debug-Protokollierung mit `express:*` in v4 zu erreichen, benutze eine Verbindung von
`express:*`, `router` und `router:*`.

```sh
# v4
DEBUG=express:* node index.js

# v5
DEBUG=express:*,router,router:* node index.js
```

<h3>Geändert</h3>

<h4 id="path-syntax">Pfad Route übereinstimmende Syntax</h4>

Syntax für Pfadrouten ist, wenn als erster Parameter `app.all()`, `app.use()`, `app.METHOD()`, `router.all()`, `router.METHOD()` und `router.use()` APIs angegeben wird. Die folgenden Änderungen wurden vorgenommen, wie der Pfad-String auf eine eingehende Anfrage abgestimmt wird:

- Das Platzhalter `*` muss einen Namen haben, passend zum Verhalten der Parameter `:`, verwende `/*splat` statt `/*`

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
`*splat` passt zu jedem Pfad ohne den Wurzelpfad. Wenn du den Wurzelpfad auch `/` anpassen musst, kannst du `/{*splat}` verwenden, indem du den Platzhalter in Klammern verpackst.

```js
// v5
app.get('/{*splat}', async (req, res) => {
  res.send('ok')
})
```

{% endcapture %}
{% include admonitions/note.html content=note_wildcard %}

- Das optionale Zeichen `?` wird nicht mehr unterstützt, verwende stattdessen Klammern.

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

- Regexp Zeichen werden nicht unterstützt. Zum Beispiel:

```js
app.get('/[discussion|page]/:slug', async (req, res) => {
  res.status(200).send('ok')
})
```

sollte geändert werden:

```js
app.get(['/discussion/:slug', '/page/:slug'], async (req, res) => {
  res.status(200).send('ok')
})
```

- Einige Zeichen wurden reserviert, um Verwirrung während des Upgrades zu vermeiden (`()[]?+!`), verwenden Sie `\` um sie zu maskieren.
- Parameternamen unterstützen nun gültige JavaScript-Identifikatoren oder zitiert wie `:"this`.

<h4 id="rejected-promises">Abgelehnte Versprechen von Middleware und Handlern</h4>

Fordern Sie Middleware und Handler an, die abgelehnte Versprechungen zurückgeben, werden nun durch die Weiterleitung des zurückgewiesenen Wertes als `Error` an die Fehlerbehandlung Middleware behandelt. Das bedeutet, dass die Verwendung von `async` Funktionen als Middleware und Handler einfacher ist als je zuvor. Wenn ein Fehler in einer `async`-Funktion oder einem abgewiesenen Versprechen geworfen wird, wird `erwartet in einer async-Funktion, diese Fehler werden an den Fehlerhandler übergeben, als ob `next(err)\` aufgerufen würde.

Details darüber, wie Express mit Fehlern umgeht, finden Sie in der [Dokumentation zur Fehlerbehandlung](/en/guide/error-handling.html).

<h4 id="express.urlencoded">express.urlencoded</h4>

Die `express.urlencoded` Methode erzeugt standardmäßig die `extended` Option `false`.

<h4 id="app.listen">app.hören</h4>

In Express 5 ruft die `app.listen` Methode die vom Benutzer zur Verfügung gestellte Callback-Funktion auf, wenn der Server ein Fehlerereignis erhält. In Express 4 würden solche Fehler aufgeworfen. Diese Änderung verlagert die Verantwortung für die Fehlerbehandlung auf die Callback-Funktion in Express 5. Wenn ein Fehler auftritt, wird er als Argument an den Callback übergeben.
Zum Beispiel:

```js
const server = app.listen(8080, '0.0.0.0', (error) => {
  if (error) {
    throw error // e.g. EADDRINUSE
  }
  console.log(`Listening on ${JSON.stringify(server.address())}`)
})
```

<h4 id="app.router">app.router</h4>

Das `app.router` Objekt, das in Express 4 entfernt wurde, hat ein Comeback in Express 5 gemacht. In der neuen Version ist dieses Objekt nur eine Referenz auf den Basis-Express-Router, im Gegensatz zu Express 3, wo eine App sie explizit laden musste.

<h4 id="req.body">req.body</h4> 

Die Eigenschaft `req.body` gibt `undefined` zurück, wenn der Body nicht analysiert wurde. In Express 4 gibt es standardmäßig `{}` zurück.

<h4 id="req.host">req.host</h4>

In Express 4 hat die `req.host` Funktion die Portnummer falsch entfernt, wenn sie vorhanden war. In Express 5 wird die Portnummer beibehalten.

<h4 id="req.query">req.query</h4>

Die Eigenschaft `req.query` ist keine beschreibbare Eigenschaft mehr und ist stattdessen ein Getter. Der Standard-Query-Parser wurde von "extended" auf "simple" geändert.

<h4 id="res.clearCookie">res.clearCookie</h4>

Die Methode `res.clearCookie` ignoriert die vom Benutzer bereitgestellten `maxAge` und `expires` Optionen.

<h4 id="res.status">res.status</h4>

Die `res.status` Methode akzeptiert nur ganze Zahlen im Bereich `100` bis `999`, gefolgt von dem von Knoten definierten Verhalten. , und gibt einen Fehler zurück, wenn der Statuscode keine Ganzzahl ist.

<h4 id="res.query">res.variieren</h4>

Das `res.vary` wirft einen Fehler auf, wenn das `field` Argument fehlt. In Express 4, wenn das Argument weggelassen wurde, gab es eine Warnung in der Konsole

### Verbesserungen

<h4 id="res.render">res.render()</h4>

Diese Methode erzwingt jetzt asynchrones Verhalten für alle View Engines, Fehler zu vermeiden, die von View Engines verursacht wurden, die eine synchrone Implementierung hatten und die gegen die empfohlene Schnittstelle verstoßen.

<h4 id="brotli-support">Unterstützung für Brotli Kodierung</h4>

Express 5 unterstützt die Kodierung von Brotli für Anfragen von Kunden, die es unterstützen.
