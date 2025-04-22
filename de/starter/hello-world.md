---
layout: page
title: Express "Hallo Welt" Beispiel
description: Beginnen Sie mit Express.js, indem Sie eine einfache 'Hallo World'-Anwendung erstellen, die die Grundeinstellung und die Servererstellung für Anfänger demonstriert.
menu: starter
lang: de
redirect_from: ""
---

# Hallo Weltbeispiel

<div class="doc-box doc-info" markdown="1">
Eingebettet unten ist im Wesentlichen die einfachste Express-App, die Sie erstellen können. Es ist eine einzelne Datei-App &mdash; _not_ was Sie bekommen würden, wenn Sie den [Express-Generator](/{{ page.lang }}/starter/generator. tml), das das Gerüst für eine vollständige Anwendung mit zahlreichen JavaScript-Dateien, Jade-Vorlagen und Unterverzeichnissen für verschiedene Zwecke erstellt.
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

Diese App startet einen Server und lauscht auf Port 3000 für Verbindungen. Die Anwendung antwortet mit "Hello World!" auf Anforderungen zur Stamm-URL (`/`) oder zu _route_. Für jeden anderen Pfad wird es mit einem **404 Nicht gefunden** antworten.

### Lokal laufen

Erstelle zuerst ein Verzeichnis namens `myapp`, ändere es und führe `npm init` aus. Installieren Sie dann `Expres` als Abhängigkeit, wie im [Installationsanleitung](/{{ page.lang }}/starter/installing.html).

Erstelle im `myapp` Verzeichnis eine Datei namens `app.js` und kopiere den Code aus dem obigen Beispiel.

<div class="doc-box doc-notice" markdown="1">
Die `req` (Anfrage) und `res` (Antwort) sind genau die gleichen Objekte, die Node anbietet, so dass du
`req aufrufen kannst. ipe()`, `req.on('data', callback)` und alles andere, was Sie ohne Express tun würden.
</div>

Führen Sie die App mit dem folgenden Befehl aus:

```bash
$ node app.js
```

Lade dann `http://localhost:3000/` in einem Browser, um die Ausgabe zu sehen.

### [Vorherig: Installation ](/{{ page.lang }}/starter/installing.html)&nbsp;&nbsp;&nbsp;&nbsp;[Weiter: Express Generator ](/{{ page.lang }}/starter/generator.html)
