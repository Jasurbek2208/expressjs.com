---
layout: page
title: Serviere statische Dateien in Express
description: Verstehen Sie, wie Sie statische Dateien wie Bilder, CSS und JavaScript in Express.js Anwendungen mit der integrierten 'static' Middleware bedienen können.
menu: starter
lang: de
redirect_from: ""
---

# Serviere statische Dateien in Express

Um statische Dateien wie Bilder, CSS-Dateien und JavaScript-Dateien bereitzustellen, verwenden Sie die in Express integrierte Middleware-Funktion `express.static`.

Die Funktionssignatur ist:

```js
express.static(root, [options])
```

Das `root` Argument gibt das Wurzelverzeichnis an, von dem aus statische Assets ausgeliefert werden sollen.
Für weitere Informationen zum Argument `options` siehe [express.static](/{{page.lang}}/4x/api.html#express.static).

Verwenden Sie zum Beispiel den folgenden Code, um Bilder, CSS-Dateien und JavaScript-Dateien in einem Verzeichnis mit dem Namen `public` auszugeben:

```js
app.use(express.static('public'))
```

Jetzt kannst du die Dateien im `public` Verzeichnis laden:

```text
http://localhost:3000/images/kitten.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/images/bg.png
http://localhost:3000/hello.html
```

<div class="doc-box doc-info">
Express sucht die Dateien relativ zum statischen Verzeichnis auf, so dass der Name des statischen Verzeichnisses nicht Teil der URL ist.
</div>

Um mehrere statische Asset-Verzeichnisse zu verwenden, rufen Sie die `express.static` Middleware-Funktion mehrmals auf:

```js
app.use(express.static('public'))
app.use(express.static('files'))
```

Express sucht die Dateien in der Reihenfolge, in der du die statischen Verzeichnisse mit der Middleware-Funktion `express.static` gesetzt hast.

{% capture alert_content %}
Für beste Ergebnisse [Benutze einen Reverse Proxy](/{{page.lang}}/advanced/best-practice-performance.html#use-a-reverse-proxy) Cache, um die Leistung des Dienstes statischer Assets zu verbessern.
{% endcapture %}
{% include admonitions/note.html content=alert_content %}

Um einen virtuellen Pfad-Präfix zu erstellen (wo der Pfad existiert eigentlich nicht im Dateisystem) für Dateien, die durch die `express. tatic` Funktion, [einen Mount-Pfad angeben](/{{ page.lang }}/4x/api.html#app.use) für das statische Verzeichnis, wie unten angezeigt:

```js
app.use('/static', express.static('public'))
```

Nun kannst du die Dateien, die sich im `public` Verzeichnis befinden, aus dem `/static` Pfadpräfix laden.

```text
http://localhost:3000/static/images/kitten.jpg
http://localhost:3000/static/css/style.css
http://localhost:3000/static/js/app.js
http://localhost:3000/static/images/bg.png
http://localhost:3000/static/hello.html
```

Der Pfad, den du der `express.static` Funktion zur Verfügung stellst, ist jedoch relativ zu dem Verzeichnis, von dem aus du deinen `node` Prozess startest. Wenn Sie die Express-App aus einem anderen Verzeichnis ausführen, ist es sicherer, den absoluten Pfad des Verzeichnisses zu verwenden, das Sie verwenden möchten:

```js
const path = require('path')
app.use('/static', express.static(path.join(__dirname, 'public')))
```

Weitere Informationen über die `serve-static` Funktion und ihre Optionen finden Sie unter  [serve-static](/resources/middleware/serve-static.html).

### [Vorherig: Einfaches Routen ](/{{ page.lang }}/starter/basic-routing.html)&nbsp;&nbsp;&nbsp;&nbsp;[Weiter: Weitere Beispiele ](/{{ page.lang }}/starter/examples.html)
