---
layout: page
title: Template-Engines mit Express verwenden
description: Entdecken Sie, wie Sie Template-Engines wie Pug, Handlebars und EJS mit Express.js integrieren und nutzen können, um dynamische HTML-Seiten effizient zu machen.
menu: guide
lang: de
redirect_from: ""
---

# Template-Engines mit Express verwenden

Eine _template engine_ ermöglicht es Ihnen, statische Template-Dateien in Ihrer Anwendung zu verwenden. Zur Laufzeit ersetzt die Template-Engine
Variablen in einer Template-Datei mit aktuellen Werten und verwandelt die Vorlage in eine HTML-Datei, die an den Client gesendet wird.
Dieser Ansatz erleichtert die Gestaltung einer HTML-Seite.

Der [Express Application Generator](/{{ page.lang }}/starter/generator. tml) verwendet [Pug](https://pugjs.org/api/getting-started.html) als Standardwert, aber es unterstützt auch [Handlebars](https://www.npmjs.com/package/handlebars), und [EJS](https://www.npmjs.com/package/ejs), unter anderem.

Um Template-Dateien zu rendern, setze folgende [Eigenschaften der Anwendungseinstellung](/{{ page.lang }}/4x/api.html#app.set), in der Standardeinstellung `app.js` des Generators:

- `views`, das Verzeichnis, in dem sich die Template-Dateien befinden. Eg: `app.set('views', './views')`.
  Dies ist standardmäßig im Verzeichnis `views` im Root-Verzeichnis der Anwendung.
- `view engine`, die zu verwendende Template-Engine. Um zum Beispiel die Mückenvorlagen-Engine zu verwenden: `app.set('view engine', 'pug')`.

Installieren Sie dann das entsprechende Template Engine npm Paket; zum Beispiel um Pug:

```bash
$ npm install pug --save
```

<div class="doc-box doc-notice" markdown="1">
Express-konforme Template-Engines wie MUG exportieren eine Funktion namens `__express(filePath, options, callback)`,
welche `res.render()` aufruft, um den Template-Code zu rendern.

Einige Template-Engines folgen nicht dieser Konvention. Die [@ladjs/consolidate](https://www.npmjs.com/package/@ladjs/consolidate)
Bibliothek folgt dieser Konvention, indem sie alle populären Template-Engines von Node.js abbildet, und arbeitet daher nahtlos in Express.

</div>

Nachdem die View Engine gesetzt ist, müssen Sie nicht die Engine angeben oder das Template Engine Modul in Ihrer App laden;
Express lädt das Modul intern, zum Beispiel:

```js
app.set('view engine', 'pug')
```

Erstelle dann eine Pug Template Datei namens `index.pug` im `views` Verzeichnis mit folgendem Inhalt:

```pug
html
  head
    title= title
  body
    h1= message
```

Erstelle eine Route um die `index.pug` Datei zu rendern. Wenn die `view engine` Eigenschaft nicht gesetzt ist,
musst du die Erweiterung der `view` Datei angeben. Andernfalls können Sie es auslassen.

```js
app.get('/', (req, res) => {
  res.render('index', { title: 'Hey', message: 'Hello there!' })
})
```

Wenn du eine Anfrage an die Startseite stellt, wird die `index.pug` Datei als HTML dargestellt.

Der View Engine-Cache speichert nicht den Inhalt der Templateausgabe, sondern nur die zugrunde liegende Vorlage selbst. Die Ansicht wird noch mit jeder Anfrage neu gerendert, auch wenn der Cache eingeschaltet ist.
