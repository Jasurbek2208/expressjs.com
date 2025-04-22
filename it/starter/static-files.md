---
layout: page
title: Servire file statici in Express
description: Comprendi come servire file statici come immagini, CSS e JavaScript nelle applicazioni Express.js utilizzando il middleware 'static' integrato.
menu: starter
lang: it
redirect_from: ""
---

# Servire file statici in Express

Per servire file statici come immagini, file CSS e file JavaScript, utilizzare la funzione middleware integrata `express.static` in Express.

La firma della funzione è:

```js
express.static(root, [options])
```

L'argomento `root` specifica la directory radice da cui servire le risorse statiche.
Per ulteriori informazioni sull'argomento `options`, vedere [express.static](/{{page.lang}}/4x/api.html#express.static).

Per esempio, utilizzare il seguente codice per servire immagini, file CSS e file JavaScript in una directory chiamata `public`:

```js
app.use(express.static('public'))
```

Ora, puoi caricare i file che sono nella directory `public`:

```text
http://localhost:3000/images/kitten.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/images/bg.png
http://localhost:3000/hello.html
```

<div class="doc-box doc-info">
Express cerca i file relativi alla directory statica, quindi il nome della directory statica non fa parte dell'URL.
</div>

Per utilizzare più directory di asset statici, chiama la funzione middleware `express.static`:

```js
app.use(express.static('public'))
app.use(express.static('files'))
```

Express cerca i file nell'ordine in cui si impostano le directory statiche con la funzione middleware `express.static`.

{% capture alert_content %}
Per ottenere risultati migliori, [utilizza un proxy inverso](/{{page.lang}}/advanced/best-practice-performance.html#use-a-reverse-proxy) cache per migliorare le prestazioni delle risorse statiche servite.
{% endcapture %}
{% include admonitions/note.html content=alert_content %}

Per creare un prefisso di percorso virtuale (dove il percorso non esiste effettivamente nel file system) per i file serviti dal `express. funzione tatic`, [specify a mount path](/{{ page.lang }}/4x/api.html#app.use) per la directory statica, come mostrato di seguito:

```js
app.use('/static', express.static('public'))
```

Ora puoi caricare i file che sono nella directory `public` dal prefisso del percorso `/static`.

```text
http://localhost:3000/static/images/kitten.jpg
http://localhost:3000/static/css/style.css
http://localhost:3000/static/js/app.js
http://localhost:3000/static/images/bg.png
http://localhost:3000/static/hello.html
```

Tuttavia, il percorso che fornisci alla funzione `express.static` è relativo alla directory da cui avvii il processo `node`. Se si esegue l'app express da un'altra directory, è più sicuro utilizzare il percorso assoluto della directory che si desidera servire:

```js
const path = require('path')
app.use('/static', express.static(path.join(__dirname, 'public')))
```

Per maggiori dettagli sulla funzione `serve-static` e sulle sue opzioni, vedere  [serve-static](/resources/middleware/serve-static.html).

### [Precedente: Basic Routing ](/{{ page.lang }}/starter/basic-routing.html)&nbsp;&nbsp;&nbsp;&nbsp;[Successivo: Altri esempi ](/{{ page.lang }}/starter/examples.html)
