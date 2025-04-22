---
layout: page
title: Express-Basis-Routing
description: Lernen Sie die Grundlagen des Routings in Express.js Anwendungen kennen, wie Sie Routen definieren, HTTP-Methoden handhaben und Routenhandler für Ihren Webserver erstellen.
menu: starter
lang: de
redirect_from: ""
---

# Basisrouting

_Routing_ bezieht sich darauf, wie eine Anwendung auf einen bestimmten Endpunkt antwortet , die eine URI (oder Pfad) und eine bestimmte HTTP-Request-Methode (GET, POST usw.) ist.

Jede Route kann eine oder mehrere Handler-Funktionen haben, die ausgeführt werden, wenn die Route übereinstimmt.

Die Routendefinition nimmt folgende Struktur ein:

```js
app.METHOD(PATH, HANDLER)
```

Wo:

- `app` ist eine Instanz von `express `.
- `METHOD` ist eine [HTTP-Anfrage-Methode](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods), in Kleinbuchstaben.
- `PATH` ist ein Pfad auf dem Server.
- `HANDLER` ist die Funktion, die ausgeführt wird, wenn die Route übereinstimmt.

<div class="doc-box doc-notice" markdown="1">
Dieses Tutorial setzt voraus, dass eine Instanz von `express ` namens `app` erstellt wird und der Server läuft. Wenn du nicht mit dem Erstellen einer App vertraut bist und sie startest, schau dir das [Hallo Welt Beispiel](/{{ page.lang }}/starter/hello-world.html).
</div>

Die folgenden Beispiele veranschaulichen die Definition einfacher Routen.

Antworte mit `Hallo World!` auf der Homepage:

```js
app.get('/', (req, res) => {
  res.send('Hello World!')
})
```

Antwort auf POST-Anfrage auf der Root-Route (`/`), der Startseite der Anwendung:

```js
app.post('/', (req, res) => {
  res.send('Got a POST request')
})
```

Antworte auf eine PUT-Anfrage auf die `/user`-Route:

```js
app.put('/user', (req, res) => {
  res.send('Got a PUT request at /user')
})
```

Antworte auf eine LÖSCHE Anfrage auf die `/user`-Route:

```js
app.delete('/user', (req, res) => {
  res.send('Got a DELETE request at /user')
})
```

Weitere Details zum Routen finden Sie im [Routing Guide](/{{ page.lang }}/guide/routing.html).

### [Vorherig: Express-Anwendungsgenerator ](/{{ page.lang }}/starter/generator.html)&nbsp;&nbsp;&nbsp;&nbsp;[Weiter: Servieren statischer Dateien in Express ](/{{ page.lang }}/starter/static-files.html)