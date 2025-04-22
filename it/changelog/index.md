---
layout: page
title: Cambio rapido
description: Rimani aggiornato con il changelog di rilascio per Express.js, dettagliando nuove funzionalità, correzioni di bug e modifiche importanti nelle versioni.
lang: it
sitemap: false
redirect_from:
  - ""
  - ""
---

<nav aria-label="sidebar-heading">
  <div class="toc-container">
    <h3 id="sidebar-heading" class="toc-heading"><em>Versioni</em></h3><button id="menu-toggle" title="show express versions">Versioni <span>►</span></button>
    <ul id="menu">
      {% capture readme %}{% include changelog/menu.md %}{% endcapture %}
      <li>
        {{ readme | markdownify }}
      </li>
    </ul>
  </div>
</nav>

<div markdown="1" id="page-doc">

# Rilascia changelog

Tutti gli ultimi aggiornamenti, miglioramenti e correzioni per Express

## Express v5

{: id="5.x"}

### 5.1.0 - Data di uscita: 2025-03-31

{: id="5.0.1"}

La versione minore 5.1.0 include alcune nuove funzionalità e miglioramenti:

- Supporto per l'invio di risposte come Uint8Array
- Aggiunto il supporto per l'opzione ETag in `res.sendFile()`
- Aggiunto il supporto per l'aggiunta di più link con lo stesso rel con `res.links()`
- Prestazioni: Utilizzare loop per acceptParams
- [body-parser@2.2.0](https://github.com/expressjs/body-parser/releases/tag/v2.2.0)
  - Rimuovere i controlli di supporto legacy node.js per Brotli & `AsyncLocalStorage`
  - Rimuovi `unpipe` & `destroy`
- [router@2.2.0](https://github.com/pillarjs/router/releases/tag/v2.2.0)
  - Restore `debug`. Ora con l'ambito `router` invece di `express`.
  - Rimuovere i controlli di supporto legacy node.js per `setImmediate`
  - Depreca il supporto promessa non nativo
  - Rimuovi `after`, `safe-buffer`, `array-flatten`, `setprotoypeof`, `methods`, `utils-merge`
- [finalhandler@2.1.0](https://github.com/pillarjs/finalhandler/releases/tag/v2.1.0)
  - Rimuovere i controlli di supporto legacy node.js per il supporto `headersSent`, `setImmediate`, & http2
  - Rimuovi `unpipe`
- Trascinò tutte le dipendenze rimanenti per usare gli intervalli `^` invece delle versioni bloccate
- Aggiungi il campo di finanziamento package.json per evidenziare il nostro OpenCollective
- Vedi [Changelog v5.1.0](https://github.com/expressjs/express/releases/tag/v5.1.0)

### 5.0.1 - Data di uscita: 2024-10-08

{: id="5.0.1"}

Il rilascio del cerotto 5.0.1 comprende un dispositivo di sicurezza:

- Aggiorna [jshttps/cookie](https://www.npmjs.com/package/cookie) per indirizzare un [vulnerability](https://github.com/advisories/GHSA-pxg6-pf52-xh8x).

### 5.0.0 - Data di uscita: 2024-09-09

{: id="5.0.0"}

Controlla la [guida alla migrazione](/{{page.lang}}/guide/migrating-5.html) con tutte le modifiche in questa nuova versione di Express.

## Express v4

{: id="4.x"}

### 4.21.2 - Data di uscita: 2024-11-06

{: id="4.21.2"}

Il rilascio del cerotto 4.21.2 comprende un dispositivo di sicurezza:

- Aggiorna [pillajs/path-to-regexp](https://www.npmjs.com/package/path-to-regexp) per indirizzare un [vulnerability](https://github.com/advisories/GHSA-rhx6-c78j-4q9w).

### 4.21.1 - Data di uscita: 2024-10-08

{: id="4.21.1"}

Il rilascio del cerotto 4.21.1 comprende un dispositivo di sicurezza:

- Aggiorna [jshttps/cookie](https://www.npmjs.com/package/cookie) per indirizzare un [vulnerability](https://github.com/advisories/GHSA-pxg6-pf52-xh8x).

### 4.21.0 - Data di uscita: 2024-09-11

{: id="4.21.0"}

La versione minore 4.21.0 include una nuova caratteristica:

- Deprecate `res.location("back")` e `res.redirect("back")` la stringa magica

### 4.20.0 - Data di uscita: 2024-09-10

{: id="4.20.0"}

La versione minore 4.20.0 include correzioni di bug e alcune nuove funzionalità, tra cui:

- Il metodo [`res.clearCookie()`](/{{ page.lang }}/4x/api.html#res.clearCookie) depreviene le opzioni `options.maxAge` e `options.expires`.
- Il metodo [`res.redirect()`](/{{ page.lang }}/4x/api.html#res.redirect) rimuove il rendering dei collegamenti HTML.
- Il metodo [`express.urlencoded()`](/{{ page.lang }}/4x/api.html#express.urlencoded) ha ora un livello di profondità di `32`, mentre in precedenza era `Infinity`.
- Aggiunge il supporto per i gruppi corrispondenti con nome negli itinerari usando un regex
- Rimuove la codifica di `\`, `<unk> `, e `^` per allineare meglio con la specifica URL

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4200--2024-09-10)

### 4.19.2 - Data di uscita: 2024-03-25

{: id="4.19.2"}

- Correzione migliorata per aprire il bypass della lista dei permessi di reindirizzamento

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4192--2024-03-25)

### 4.19.1 - Data di uscita: 2024-03-20

{: id="4.19.1"}

- Consenti di passare senza stringhe a res.location con nuovi controlli di gestione della codifica

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4191--2024-03-20)

### 4.19.0 - Data di uscita: 2024-03-20

{: id="4.19.0"}

- Impedisci il bypass dell'elenco aperto di reindirizzamento a causa di encodeurl
- deps: cookie@0.6.0

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4190--2024-03-20)

### 4.18.3 - Data di uscita: 2024-02-29

{: id="4.18.3"}

La versione della patch 4.18.3 include la seguente correzione di bug:

<ul>
  <li markdown="1" class="changelog-item">
  Correggi le richieste di routing senza metodo. ([commit](https://github.com/expressjs/express/commit/74beeac0718c928b4ba249aba3652c52fbe32ca8))  
</li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4183--2024-02-26)

### 4.18.2 - Data di uscita: 2022-10-08

{: id="4.18.2"}

La versione della patch 4.18.2 include la seguente correzione di bug:

<ul>
  <li markdown="1" class="changelog-item">
  Correggere la regressione instradando una grande pila in un unico percorso. ([commit](https://github.com/expressjs/express/commit/7ec5dd2b3c5e7379f68086dae72859f5573c8b9b))  
</li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4182--2022-10-08)

### 4.18.1 - Data di uscita: 2022-04-29

{: id="4.18.1"}

La versione della patch 4.18.1 include la seguente correzione di bug:

<ul>
  <li markdown="1" class="changelog-item">
  Fissare la condizione in cui se un'applicazione Express viene creata con una pila di percorsi molto grande, e tutti questi percorsi sono sincronizzati (call `next()` in modo sincrono), quindi l'elaborazione della richiesta può bloccare.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4181--2022-04-29).

### 4.18.0 - Data di uscita: 2022-04-25

{: id="4.18.0"}

La versione minore 4.18.0 include correzioni di bug e alcune nuove funzionalità, tra cui:

<ul>
  <li markdown="1" class="changelog-item">
  Il metodo [`app.get()`](/{{ page.lang }}/4x/api.html#app.get) e il metodo [`app.set()`](/{{ page.lang }}/4x/api.html#app.set) ora ignorano le proprietà direttamente su `Object.prototype` quando si ottiene un valore impostazione.
  </li>

  <li markdown="1" class="changelog-item">
  Il metodo [`res.cookie()`](/{{ page.lang }}/4x/api.html#res.cookie) accetta ora un'opzione "priorità" per impostare l'attributo Priorità sull'intestazione della risposta Set-Cookie.
  </li>

  <li markdown="1" class="changelog-item">
  Il metodo [`res.cookie()`](/{{ page.lang }}/4x/api.html#res.cookie) ora rifiuta un oggetto Data non valido fornito come l'opzione "expires".
  </li>

  <li markdown="1" class="changelog-item">
  Il metodo [`res.cookie()`](/{{ page.lang }}/4x/api.html#res.cookie) funziona ora quando `null` o `undefined` è esplicitamente fornito come argomento "maxAge".
  </li>

  <li markdown="1" class="changelog-item">
  A partire da questa versione, Express supporta Node.js 18.x.
  </li>

  <li markdown="1" class="changelog-item">
  Il metodo [`res.download()`](/{{ page.lang }}/4x/api.html#res.download) accetta ora l'opzione "root" per abbinare [`res.sendFile()`](/{{ page.lang }}/4x/api.html#res.sendFile).
  </li>

  <li markdown="1" class="changelog-item">
  Il metodo [`res.download()`](/{{ page.lang }}/4x/api.html#res. ● ad) può essere fornito con un oggetto `options` senza fornire un argomento `filename`, semplificando le chiamate quando il nome `file` predefinito è desiderato.
  </li>

  <li markdown="1" class="changelog-item">
  Il metodo [`res.format()`](/{{ page.lang }}/4x/api.html#res.format) ora invoca il gestore "default" fornito con gli stessi argomenti dei gestori di tipo (`req`, `res`, and `next`).
  </li>

  <li markdown="1" class="changelog-item">
  Il metodo [`res.send()`](/{{ page.lang }}/4x/api.html#res.send) non tenterà di inviare un corpo di risposta quando il codice di risposta è impostato a 205.
  </li>

  <li markdown="1" class="changelog-item">
  Il gestore degli errori predefinito rimuoverà ora alcune intestazioni di risposta che interromperanno il rendering delle risposte agli errori, se impostate in precedenza.
  </li>

  <li markdown="1" class="changelog-item">
  Il codice di stato 425 è ora rappresentato come lo standard "Too Early" invece di "Unordered Collection".
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4180--2022-04-25).

### 4.17.3 - Data di uscita: 2022-02-16

{: id="4.17.3"}

La versione della patch 4.17.3 include una correzione di bug:

<ul>
  <li markdown="1" class="changelog-item">
  Aggiorna a [qs module](https://www.npmjs.com/package/qs) per correggere le proprietà di analisi `__proto__`.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4173--2022-02-16).

### 4.17.2 - Data di uscita: 2021-12-16

{: id="4.17.2"}

La versione della patch 4.17.2 include le seguenti correzioni di bug:

<ul>
  <li markdown="1" class="changelog-item">
  Risolta la gestione di `undefined` in `res.jsonp` quando viene fornito un callback.
  </li>

  <li markdown="1" class="changelog-item">
  Risolta la gestione di `undefined` in `res.json` e `res.jsonp` quando `"json escape"` è abilitato.
  </li>

  <li markdown="1" class="changelog-item">
  Corregge la gestione dei valori non validi all'opzione `maxAge` di `res.cookie()`.
  </li>

  <li markdown="1" class="changelog-item">
  Aggiorna a [jshttp/proxy-addr module](https://www.npmjs.com/package/proxy-addr) per usare `req.socket` sopra il file `req.connection`.
  </li>

  <li markdown="1" class="changelog-item">
  A partire da questa versione, Express supporta Node.js 14.x.
  </li>

</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4172--2021-12-16).

### 4.17.1 - Data di uscita: 2019-05-25

{: id="4.17.1"}

La versione della patch 4.17.1 include una correzione di bug:

<ul>
  <li markdown="1" class="changelog-item">
  La modifica all'API `res.status()` è stata ripristinata a causa della regressione nelle applicazioni Express 4 esistenti.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4171--2019-05-25).

### 4.17.0 - Data di uscita: 2019-05-16

{: id="4.17.0"}

La versione minore 4.17.0 include correzioni di bug e alcune nuove funzionalità, tra cui:

<ul>
  <li markdown="1" class="changelog-item">
  I file `express.raw()` e `express.text()` middleware sono stati aggiunti per fornire la richiesta di analisi del corpo per ulteriori richieste di payloads. Questo utilizza il modulo [expressjs/body-parser module](https://www.npmjs.com/package/body-parser) sottostante, in modo che le applicazioni che attualmente richiedono il modulo separatamente possono passare ai analizzatori integrati.
  </li>

  <li markdown="1" class="changelog-item">
  L'API `res.cookie()` ora supporta il valore `"none"` per l'opzione `sameSite`.
  </li>

  <li markdown="1" class="changelog-item">
  Quando l'impostazione `"trust proxy"` è abilitata, il `req.hostname` ora supporta più intestazioni `X-Forwarded-For` in una richiesta.
  </li>

  <li markdown="1" class="changelog-item">
  A partire da questa versione, Express supporta Node.js 10.x e 12.x.
  </li>

  <li markdown="1" class="changelog-item">
  L'API `res.sendFile()` fornisce ora e più immediata e più facile da capire l'errore quando una non stringa viene passata come argomento `path`.
  </li>

  <li markdown="1" class="changelog-item">
  L'API `res.status()` ora fornisce e più immediata e più facile da capire l'errore quando `null` o `undefined` viene passato come argomento.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4170--2019-05-16).

### 4.16.4 - Data di uscita: 2018-10-10

{: id="4.16.4"}

La versione della patch 4.16.4 include varie correzioni di bug:

<ul>
  <li markdown="1" class="changelog-item">
  Risolto il problema in cui `"Request aborted"` potrebbe essere loggato in `res.sendfile`.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4164--2018-10-10).

### 4.16.3 - Data di uscita: 2018-03-12

{: id="4.16.3"}

La versione della patch 4.16.3 include varie correzioni di bug:

<ul>
  <li markdown="1" class="changelog-item">
  Risolve il problema dove un semplice `%` alla fine dell'url nel `res. il metodo ocation` o il metodo `res.redirect` non verrebbero codificati come `%25`.
  </li>

  <li markdown="1" class="changelog-item">
  Risolto il problema in cui un valore `req.url` vuoto può causare un errore generato all'interno della gestione 404 predefinita.
  </li>

  <li markdown="1" class="changelog-item">
  Corregge il documento HTML generato per le risposte di reindirizzamento `express.static` per includere correttamente `</html>`.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4163--2018-03-12).

### 4.16.2 - Data di uscita: 2017-10-09

{: id="4.16.2"}

La versione della patch 4.16.2 include una correzione di bug di regressione:

<ul>
  <li markdown="1" class="changelog-item">
  Corregge un `TypeError` che può verificarsi nel metodo `res.send` quando un `Buffer` viene passato a `res. end` e l'intestazione `ETag` è già impostata sulla risposta.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4162--2017-10-09).

### 4.16.1 - Data di uscita: 2017-09-29

{: id="4.16.1"}

La versione della patch 4.16.1 include una correzione di bug regressione:

<ul>
  <li markdown="1" class="changelog-item">
  Aggiorna a [pillarjs/send module](https://www.npmjs.com/package/send) per correggere una regressione di scenario di bordo che ha colpito alcuni utenti di `express.static`.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4161--2017-09-29).

### 4.16.0 - Data di uscita: 2017-09-28

{: id="4.16.0"}

La versione minore 4.16.0 include aggiornamenti di sicurezza, correzioni di bug, miglioramenti delle prestazioni e alcune nuove funzionalità, tra cui:

<ul>
  <li markdown="1" class="changelog-item">
  Aggiorna a [jshttp/forwarded module](https://www.npmjs.com/package/forwarded) per indirizzare un [vulnerability](https://npmjs.com/advisories/527). Questo può influenzare la tua applicazione se vengono utilizzate le seguenti API: `req.host`, `req.hostname`, `req.ip`, `req.ips`, `req.protocol`.
  </li>

  <li markdown="1" class="changelog-item">
  Aggiorna una dipendenza del [pillarjs/send module](https://www.npmjs.com/package/send) per indirizzare una [vulnerability](https://npmjs.com/advisories/535) nella dipendenza `mime`. Questo può influenzare la tua applicazione se l'input di stringa non attendibile viene passato alle seguenti API: `res.type()`.
  </li>

  <li markdown="1" class="changelog-item">
  Il modulo [pillarjs/send module](https://www.npmjs.com/package/send) ha implementato una protezione contro Node.js 8.5.0 [vulnerability](https://nodejs.org/en/blog/vulnerability/september-2017-path-validation/). L'utilizzo di qualsiasi versione precedente di Express con Node.js 8.5.0 (quella specifica versione di Node.js) renderà vulnerabili le seguenti API: `express.static`, `res.sendfile`, e `res.sendFile`.
  </li>

  <li markdown="1" class="changelog-item">
  A partire da questa versione, Express supporta Node.js 8.x.
  </li>

  <li markdown="1" class="changelog-item">
  La nuova impostazione `"json escape"` può essere abilitata per sfuggire ai caratteri `res.json()`, `res.jsonp()` e `res. end()` risposte che possono innescare client per annidare la risposta come HTML invece di onorare il `Content-Type`. Questo può aiutare a proteggere un'app Express da una classe di attacchi persistenti basati su XSS.
  </li>

  <li markdown="1" class="changelog-item">
  Il metodo [`res.download()`](/{{ page.lang }}/4x/api.html#res.download) accetta ora un oggetto opzionale `options`.
  </li>

  <li markdown="1" class="changelog-item">
  Il middleware `express.json()` e `express.urlencoded()` sono stati aggiunti per fornire il supporto di analisi del corpo della richiesta fuori dalla scatola. Questo utilizza il modulo [expressjs/body-parser module](https://www.npmjs.com/package/body-parser) sottostante, in modo che le applicazioni che attualmente richiedono il modulo separatamente possono passare ai analizzatori integrati.
  </li>

  <li markdown="1" class="changelog-item">
  Il metodo [`express.static()` middleware](/{{ page.lang }}/4x/api.html#express.static) e [`res.sendFile()`](/{{ page.lang }}/4x/api.html#res.sendFile) ora supporta l'impostazione della direttiva `immutable` nell'intestazione `Cache-Control`. Impostare questa intestazione con un `maxAge` appropriato impedirà ai browser web di inviare qualsiasi richiesta al server quando il file è ancora nella loro cache.
  </li>

  <li markdown="1" class="changelog-item">
  Il modulo [pillarjs/send module](https://www.npmjs.com/package/send) ha un elenco aggiornato di tipi MIME per impostare meglio il file `Content-Type` di altri file. Ci sono 70 nuovi tipi per le estensioni di file.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4160--2017-09-28).

### 4.15.5 - Data di uscita: 2017-09-24

{: id="4.15.5"}

Il 4.15.5 patch release include aggiornamenti di sicurezza, alcuni miglioramenti di prestazioni minori e una correzione di bug:

<ul>
  <li markdown="1" class="changelog-item">
  Aggiorna al [modulo di debug](https://www.npmjs.com/package/debug) per indirizzare un [vulnerability](https://snyk.io/vuln/npm:debug:20170905), ma questo problema non influisce su Express.
  </li>

  <li markdown="1" class="changelog-item">
  Aggiorna a [jshttp/fresh module](https://www.npmjs.com/package/fresh) per indirizzare un [vulnerability](https://npmjs.com/advisories/526). Questo influenzerà la tua applicazione se vengono utilizzate le seguenti API: `express.static`, `req.fresh`, `res.json`, `res.jsonp`, `res.send`, `res.sendfile` `res.sendFile`, `res.sendStatus`.
  </li>

  <li markdown="1" class="changelog-item">
  Aggiorna a [jshttp/fresh module](https://www.npmjs.com/package/fresh) corregge la gestione delle intestazioni modificate con date non valide e rende più veloce l'analisi delle intestazioni condizionali (come `If-None-Match`).
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4155--2017-09-24).

### 4.15.4 - Data di uscita: 2017-08-06

{: id="4.15.4"}

La versione della patch 4.15.4 include alcune correzioni di bug minori:

<ul>
  <li markdown="1" class="changelog-item">
  Fissa l'array per il valore `"trust proxy"` manipolato in determinate condizioni.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4154--2017-08-06).

### 4.15.3 - Data di uscita: 2017-05-16

{: id="4.15.3"}

Il 4.15.3 patch release include un aggiornamento di sicurezza e alcune correzioni di bug minori:

<ul>
  <li markdown="1" class="changelog-item">
  Aggiorna una dipendenza di [pillarjs/send module](https://www.npmjs.com/package/send) per indirizzare un [vulnerability](https://snyk.io/vuln/npm:ms:20170412). Questo può influenzare la tua applicazione se l'input di stringa non attendibile viene passato all'opzione `maxAge` nelle seguenti API: `express.static`, `res.sendfile`, e `res.sendFile`.
  </li>

  <li markdown="1" class="changelog-item">
  Correggi l'errore quando `res.set` non può aggiungere charset a `Content-Type`.
  </li>

  <li markdown="1" class="changelog-item">
  Corregge la mancanza di `</html>` nel documento HTML.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4153--2017-05-16).

### 4.15.2 - Data di uscita: 2017-03-06

{: id="4.15.2"}

La versione della patch 4.15.2 include una correzione di bug minore:

<ul>
  <li markdown="1" class="changelog-item">
  Correggi le chiavi di analisi della regressione che iniziano con `[` nel parser di query esteso (predefinito).
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4152--2017-03-06).

### 4.15.1 - Data di uscita: 2017-03-05

{: id="4.15.1"}

La versione della patch 4.15.1 include una correzione di bug minore:

<ul>
  <li markdown="1" class="changelog-item">
  Risolve il problema di compatibilità quando si utilizza la libreria datejs 1.x dove [`express.static()` middleware](/{{ page.lang }}/4x/api.html#express. tatic) e [`res.sendFile()` method](/{{ page.lang }}/4x/api.html#res.sendFile) risponderebbero in modo errato con 412 Precondizione fallita.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4151--2017-03-05).

### 4.15.0 - Data di uscita: 2017-03-01

{: id="4.15.0"}

La versione minore 4.15.0 include correzioni di bug, miglioramenti delle prestazioni e altre funzionalità minori aggiunte, tra cui:

<ul>
  <li markdown="1" class="changelog-item">
  A partire da questa versione, Express supporta Node.js 7.x.
  </li>

  <li markdown="1" class="changelog-item">
  Il metodo [`express.static()` middleware](/{{ page.lang }}/4x/api.html#express.static) e [`res.sendFile()`](/{{ page.lang }}/4x/api.html#res.sendFile) ora supporta le intestazioni della richiesta `If-Match` e `If-Unmodified-Since`.
  </li>

  <li markdown="1" class="changelog-item">
  Update to [jshttp/etag module](https://www.npmjs.com/package/etag) to generate the default ETags for responses which work when Node.js has [FIPS-compliant crypto enabled](https://nodejs.org/dist/latest/docs/api/cli.html#cli_enable_fips).
  </li>

  <li markdown="1" class="changelog-item">
  Varie risposte HTML generate automaticamente, come il default non trovato e i gestori degli errori risponderanno con documenti HTML 5 completi e intestazioni di sicurezza aggiuntive.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4150--2017-03-01).

### 4.14.1 - Data di uscita: 2017-01-28

{: id="4.14.1"}

La patch release 4.14.1 include correzioni di bug e miglioramenti delle prestazioni, tra cui:

<ul>
  <li markdown="1" class="changelog-item">
  Aggiorna a [modulo pillarjs/finalhandler](https://www.npmjs.com/package/finalhandler) corregge un'eccezione quando Express gestisce un oggetto `Error` che ha una proprietà `headers` che non è un oggetto.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4141--2017-01-28).

### 4.14.0 - Data di uscita: 2016-06-16

{: id="4.14.0"}

La versione minore 4.14.0 include correzioni di bug, aggiornamenti di sicurezza, miglioramenti delle prestazioni e altre funzionalità minori aggiunte, tra cui:

<ul>
  <li markdown="1" class="changelog-item">
  A partire da questa versione, Express supporta Node.js 6.x.
  </li>

  <li markdown="1" class="changelog-item">
  Update to [jshttp/negotiator module](https://www.npmjs.com/package/negotiator) fix a [regular expression denial of service vulnerability](https://npmjs.com/advisories/106).
  </li>

  <li markdown="1" class="changelog-item">
  Il metodo [`res.sendFile()`](/{{ page.lang }}/4x/api.html#res.sendFile) ora accetta due nuove opzioni: `acceptRanges` e `cacheControl`.

- `acceptRanges` (defaut is `true`), abilita o disabilita l'accettazione di richieste a distanza. Se disabilitata, la risposta non invia l'intestazione `Accept-Ranges` e ignora il contenuto dell'intestazione della richiesta `Range`.

- `cacheControl`, (predefinito è `true`), abilita o disabilita l'intestazione della risposta `Cache-Control`. Disabilitandolo ignorerà l'opzione `maxAge`.

- `res.sendFile` è stato anche aggiornato per gestire meglio l'intestazione `Range` e i reindirizzamenti.

  </li>

  <li markdown="1" class="changelog-item">
  Il metodo [`res.location()`](/{{ page.lang }}/4x/api.html#res.location) e [`res.redirect()` method](/{{ page.lang }}/4x/api.html#res.redirect) ora URL-encode la stringa URL, se non è già codificata.
  </li>

  <li markdown="1" class="changelog-item">
  Le prestazioni del metodo [`res.json()`](/{{ page.lang }}/4x/api.html#res.json) e [`res.jsonp()` method](/{{ page.lang }}/4x/api.html#res.jsonp) sono state migliorate nei casi comuni.
  </li>

  <li markdown="1" class="changelog-item">
  Il [modulo jshttp/cookie](https://www.npmjs.com/package/cookie) (in aggiunta a una serie di altri miglioramenti) è stato aggiornato e ora [`res. ookie()` method](/{{ page.lang }}/4x/api.html#res.cookie) supporta l'opzione `sameSite` per consentirti di specificare l'attributo [SameSite cookie attribute](https://tools.ietf.org/html/draft-west-first-party-cookies-07).  

{% include admonitions/note.html content="Questo attributo non è ancora stato completamente standardizzato, potrebbe cambiare in futuro, e molti client potrebbero ignorarlo." %}

Il valore possibile per l'opzione `sameSite` sono:

- `true`, che imposta l'attributo `SameSite` a `Strict` per una rigorosa applicazione dello stesso sito.
- `false`, che non imposta l'attributo `SameSite`.
- `'lax'`, che imposta l'attributo `SameSite` a `Lax` per la stessa applicazione lax dello stesso sito.
- `'strict'`, che imposta l'attributo `SameSite` a `Strict` per una rigorosa applicazione dello stesso sito.

  </li>

  <li markdown="1" class="changelog-item">
  Il controllo del percorso assoluto su Windows, che per alcuni casi era errato, è stato corretto.
  </li>

  <li markdown="1" class="changelog-item">La risoluzione 
  indirizzo IP con proxy è stata notevolmente migliorata.
  </li>

  <li markdown="1" class="changelog-item">
  Il metodo [`req.range()`](/{{ page.lang }}/4x/api.html#req. ange) options object ora supporta l'opzione `combine` (`false` per impostazione predefinita), che quando `true`, combina gli intervalli sovrapposti e adiacenti e li restituisce come se fossero specificati in questo modo nell'intestazione.
  </li>
</ul>

Per un elenco completo delle modifiche a questa versione, vedere [History.md](https://github.com/expressjs/express/blob/master/History.md#4140--2016-06-16).

</div>
