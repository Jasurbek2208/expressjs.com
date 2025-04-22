---
layout: page
title: Schreibe Middleware für die Verwendung in Express-Apps
description: Erfahren Sie, wie Sie benutzerdefinierte Middleware-Funktionen für Express.js-Anwendungen schreiben, einschließlich Beispielen und Best Practices zur Verbesserung der Request- und Response-Behandlung.
menu: guide
lang: de
redirect_from: ""
---

# Schreibe Middleware für die Verwendung in Express-Apps

<h2>Übersicht</h2>

_Middleware_ Funktionen sind Funktionen, die Zugriff auf das [Anfrageobjekt](/{{ page.lang }}/4x/api. tml#req) (`req`), das [Antwort-Objekt](/{{ page.lang }}/4x/api.html#res) (`res`) und die `next` Funktion im Request-Antwort-Zyklus der Anwendung. Die `next`-Funktion ist eine Funktion im Express-Router, der beim Aufruf die Middleware ausführt, die die aktuelle Middleware abfolgt.

Middleware-Funktionen können folgende Aufgaben ausführen:

- Führe jeden Code aus.
- Änderungen an der Anfrage und den Antwort-Objekten vornehmen.
- Beende den Request-Antwort-Zyklus.
- Rufen Sie die nächste Middleware im Stapel auf.

Wenn die aktuelle Middleware-Funktion den Request-Antwort-Zyklus nicht beendet, muss sie `next()` aufrufen, um die Kontrolle an die nächste Middleware-Funktion zu übergeben. Andernfalls bleibt die Anfrage hängen.

Die folgende Abbildung zeigt die Elemente eines Middleware-Funktionsaufrufs:

<table id="mw-fig">
<tbody><tr><td id="mw-fig-imgcell">
<img src="/images/express-mw.png" alt="Elements of a middleware function call" id="mw-fig-img" />
</td>
<td class="mw-fig-callouts">
<div class="callout" id="callout1">HTTP-Methode, auf die die Middleware-Funktion zutrifft.</div></tbody>

<div class="callout" id="callout2">Pfad (Route), für den die Middleware-Funktion gilt.</div>

<div class="callout" id="callout3">Die Middleware-Funktion.</div>

<div class="callout" id="callout4">Callback-Argument an die Middleware-Funktion, genannt "Next" durch Konvention.</div>

<div class="callout" id="callout5">HTTP <a href="/{{ page.lang }}/4x/api.html#res">Antwort</a> Argument auf die Middleware-Funktion, genannt "res" durch Konvention.</div>

<div class="callout" id="callout6">HTTP <a href="/{{ page.lang }}/4x/api.html#req">Request</a> Argument für die Middleware-Funktion, genannt "req" durch Konvention.</div>
</td></tr>
</table>

Beginnend mit Express 5 ruft Middleware-Funktionen, die ein Versprechen zurückgeben, `next(value)` auf, wenn sie einen Fehler ablehnen oder werfen. `next` wird entweder mit dem abgelehnten Wert oder mit dem Wurffehler aufgerufen.

<h2>Beispiel</h2>

Hier ist ein Beispiel für eine einfache "Hallo World"-Express-Anwendung.
Der Rest dieses Artikels definiert und fügt der Anwendung drei Middleware-Funktionen hinzu:
eine mit dem Namen `myLogger`, die eine einfache Logmeldung ausgibt, einen namens `requestTime`, der
den Zeitstempel der HTTP-Anfrage anzeigt und einen, der `validateCookies` genannt wird, der eingehende Cookies validiert.

```js
const express = require('express')
const app = express()

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(3000)
```

<h3>Middleware-Funktion myLogger</h3>
Hier ist ein einfaches Beispiel für eine Middleware-Funktion namens "myLogger". Diese Funktion druckt einfach "LOGGED", wenn eine Anfrage an die App durchläuft. Die Middleware-Funktion wird einer Variable mit dem Namen `myLogger` zugewiesen.

```js
const myLogger = function (req, res, next) {
  console.log('LOGGED')
  next()
}
```

<div class="doc-box doc-notice" markdown="1">
Beachten Sie den obigen Aufruf zu `next()`. Beim Aufruf dieser Funktion wird die nächste Middleware-Funktion in der App aufgerufen.
Die `next()` Funktion ist nicht Teil der Node.js oder Express-API, sondern das dritte Argument, das an die Middleware-Funktion übergeben wird. Die `next()` Funktion konnte überhaupt benannt werden, aber nach der Konvention wird sie immer als "next()" bezeichnet.
Um Verwirrung zu vermeiden, verwenden Sie immer dieses Übereinkommen.
</div>

Um die Middleware-Funktion zu laden, rufen Sie `app.use()` auf, indem Sie die Middleware-Funktion angeben.
Zum Beispiel lädt der folgende Code die `myLogger` Middleware-Funktion vor der Route zum Root-Pfad (/).

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

Jedes Mal, wenn die App eine Anfrage erhält, gibt sie die Nachricht "LOGGED" auf das Terminal aus.

Die Reihenfolge des Laden von Middleware ist wichtig: Middleware-Funktionen, die zuerst geladen werden, werden auch zuerst ausgeführt.

Wenn `myLogger` nach der Route zum Wurzelpfad geladen wird, erreicht die Anfrage nie und die App druckt nicht "LOGGED", da der Route-Handler des Root-Pfades den Request-Antwort-Zyklus beendet.

Die Middleware-Funktion `myLogger` druckt einfach eine Nachricht, übergibt dann die Anfrage an die nächste Middleware-Funktion im Stack durch Aufruf der `next()` Funktion.

<h3>Middleware-Funktionsanfragezeit</h3>

Als nächstes erstellen wir eine Middleware-Funktion namens "requestTime" und fügen eine Eigenschaft namens `requestTime`
dem Anfrageobjekt hinzu.

```js
const requestTime = function (req, res, next) {
  req.requestTime = Date.now()
  next()
}
```

Die App verwendet nun die „requestTime“-Middleware-Funktion. Auch die Callback-Funktion der Root-Pfadroute verwendet die Eigenschaft, die die Middleware-Funktion zu `req` hinzufügt (das Anfrageobjekt).

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

Wenn Sie eine Anfrage an das Stammverzeichnis der App stellen, zeigt die App nun den Zeitstempel Ihrer Anfrage im Browser an.

<h3>Middleware-Funktion validateCookies</h3>

Schließlich erstellen wir eine Middleware-Funktion, die eingehende Cookies validiert und eine 400 Antwort schickt, wenn Cookies ungültig sind.

Hier ist eine Beispielfunktion, die Cookies mit einem externen Asynchrondienst überprüft.

```js
async function cookieValidator (cookies) {
  try {
    await externallyValidateCookie(cookies.testCookie)
  } catch {
    throw new Error('Invalid cookies')
  }
}
```

Hier verwenden wir die [`cookie-parser`](/resources/middleware/cookie-parser.html) Middleware, um eingehende Cookies vom `req` Objekt zu analysieren und sie an unsere `cookieValidator` Funktion zu übergeben. Die `validateCookies` Middleware gibt ein Versprechen zurück, das bei Ablehnung automatisch unseren Fehlerhandler auslöst.

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
Beachte, wie `next()` nach `wait cookieValidator(req.cookies)` aufgerufen wird. Dies stellt sicher, dass, wenn `cookieValidator` aufgelöst wird, die nächste Middleware im Stack aufgerufen wird. Wenn Sie Übergaben an die Funktion `next()` vornehmen (außer die Zeichenfolge `'route'`), sieht Express die aktuelle Anforderung als Fehler an und überspringt alle verbleibenden fehlerfreien Behandlungsroutinen und Middlewarefunktionen.
</div>

Weil Sie Zugriff auf das Anfrageobjekt, das Antwortobjekt, die nächste Middleware-Funktion im Stapel und den gesamten Knoten haben. s API, die Möglichkeiten mit Middleware-Funktionen sind endlos.

Für weitere Informationen über Express Middleware siehe: [Express Middleware](/{{ page.lang }}/guide/using-middleware.html).

<h2>Konfigurierbare Middleware</h2>

Wenn Sie Ihre Middleware konfigurieren müssen, exportieren Sie eine Funktion, die ein Optionsobjekt oder andere Parameter akzeptiert, , die dann die Middleware-Implementierung basierend auf den Eingabeparametern zurückgibt.

Datei: `my-middleware.js`

```js
module.exports = function (options) {
  return function (req, res, next) {
    // Implement the middleware function based on the options object
    next()
  }
}
```

Die Middleware kann nun wie unten gezeigt verwendet werden.

```js
const mw = require('./my-middleware.js')

app.use(mw({ option1: '1', option2: '2' }))
```

Siehe [cookie-session](https://github.com/expressjs/cookie-session) und [compression](https://github.com/expressjs/compression) für Beispiele konfigurierbarer Middleware.
