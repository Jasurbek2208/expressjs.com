---
layout: page
title: Express-Änderungsprotokoll
description: Bleiben Sie auf dem Laufenden mit dem Release-Changelog für Express.js, das neue Features, Fehlerbehebungen und wichtige Änderungen in verschiedenen Versionen.
lang: de
sitemap: false
redirect_from:
  - ""
  - ""
---

<nav aria-label="sidebar-heading">
  <div class="toc-container">
    <h3 id="sidebar-heading" class="toc-heading"><em>Versionen</em></h3><button id="menu-toggle" title="show express versions">Versionen <span>►</span></button>
    <ul id="menu">
      {% capture readme %}{% include changelog/menu.md %}{% endcapture %}
      <li>
        {{ readme | markdownify }}
      </li>
    </ul>
  </div>
</nav>

<div markdown="1" id="page-doc">

# Änderungsprotokoll freigeben

Alle neuesten Updates, Verbesserungen und Korrekturen an Express

## Express v5

{: id="5.x"}

### 5.1.0 - Veröffentlichungsdatum: 2025-03-31

{: id="5.0.1"}

Die kleine Version 5.1.0 enthält einige neue Funktionen und Verbesserungen:

- Unterstützung für das Senden von Antworten als Uint8Array
- Unterstützung für ETag Option in `res.sendFile()` hinzugefügt
- Unterstützung für das Hinzufügen mehrerer Links mit dem gleichen Rel mit `res.links()` hinzugefügt
- Performance: Benutze Schleife für Akzeptanzparameter
- [Körper-parser@2.2.0](https://github.com/expressjs/body-parser/releases/tag/v2.2.0)
  - Entferne alte node.js Unterstützungsprüfungen für Brotli & `AsyncLocalStorage`
  - Entferne `unpipe` & `destroy`
- [router@2.2.0](https://github.com/pillarjs/router/releases/tag/v2.2.0)
  - Restore `debug`. Jetzt mit dem »router«-Bereich anstelle von »Express«.
  - Legacy node.js Support Checks für `setImmediate` entfernen
  - Nicht-native Versprechungsunterstützung veraltet
  - Entferne `after`, `safe-buffer`, `array-flatten`, `setprotoypeof`, `methods`, `utils-merge`
- [finalhandler@2.1.0](https://github.com/pillarjs/finalhandler/releases/tag/v2.1.0)
  - Entferne alte node.js Unterstützungsprüfungen für `headersSent`, `setImmediate`, & http2 Unterstützung
  - Entferne `unpipe`
- Überstellt alle verbleibenden Abhängigkeiten um `^` Bereiche anstelle von gesperrten Versionen zu verwenden
- Füge package.json Förderfeld hinzu, um unser OpenCollective hervorzuheben
- Siehe [Changelog v5.1.0](https://github.com/expressjs/express/releases/tag/v5.1.0)

### 5.0.1 - Veröffentlichungsdatum: 2024-10-08

{: id="5.0.1"}

Der Patch 5.0.1 enthält eine Sicherheitshinweise:

- Aktualisiere [jshttps/cookie](https://www.npmjs.com/package/cookie), um eine [vulnerability](https://github.com/advisories/GHSA-pxg6-pf52-xh8x).

### 5.0.0 - Veröffentlichungsdatum: 2024-09-09

{: id="5.0.0"}

Überprüfen Sie die [Migrationsanleitung](/{{page.lang}}/guide/migrating-5.html) mit allen Änderungen in dieser neuen Version von Express.

## Express v4

{: id="4.x"}

### 4.21.2 - Veröffentlichungsdatum: 2024-11-06

{: id="4.21.2"}

Die Patchversion 4.21.2 enthält eine Sicherheitshinweise:

- Aktualisiere [pillajs/path-to-regexp](https://www.npmjs.com/package/path-to-regexp), um eine [vulnerability](https://github.com/advisories/GHSA-rhx6-c78j-4q9w).

### 4.21.1 - Veröffentlichungsdatum: 2024-10-08

{: id="4.21.1"}

Die Patchversion 4.21.1 enthält eine Sicherheitshinweise:

- Aktualisiere [jshttps/cookie](https://www.npmjs.com/package/cookie), um eine [vulnerability](https://github.com/advisories/GHSA-pxg6-pf52-xh8x).

### 4.21.0 - Veröffentlichungsdatum: 2024-09-11

{: id="4.21.0"}

Die Version 4.21.0 enthält eine neue Funktion:

- Veraltete `res.location("back")` und `res.redirect("back")` magische Zeichenkette

### 4.20.0 - Veröffentlichungsdatum: 2024-09-10

{: id="4.20.0"}

Die kleine 4.20.0 Version enthält Fehlerbehebungen und einige neue Features, einschließlich:

- Die [`res.clearCookie()` Methode](/{{ page.lang }}/4x/api.html#res.clearCookie) veraltet die Optionen `options.maxAge` und `options.expires`.
- Die [`res.redirect()` Methode](/{{ page.lang }}/4x/api.html#res.redirect) entfernt die HTML-Link-Rendering.
- Die [`express.urlencoded()` Methode](/{{ page.lang }}/4x/api.html#express.urlencoded) Methode hat nun eine Tiefenstufe von `32`, wohingegen sie zuvor `Infinity` war.
- Fügt mithilfe eines Regex Unterstützung für benannte übereinstimmende Gruppen in den Routen hinzu
- Entfernt die Kodierung von `\`, `|` und `^` um sich besser mit der URL-Spezifikation auseinander zu setzen

Für eine vollständige Liste der Änderungen in dieser Version siehe [History.md](https://github.com/expressjs/express/blob/master/History.md#4200--2024-09-10)

### 4.19.2 - Veröffentlichungsdatum: 2024-03-25

{: id="4.19.2"}

- Verbesserte Korrektur für die Umgehung der Liste durch offene Weiterleitung

Für eine vollständige Liste der Änderungen in dieser Version siehe [History.md](https://github.com/expressjs/express/blob/master/History.md#4192--2024-03-25)

### 4.19.1 - Veröffentlichungsdatum: 2024-03-20

{: id="4.19.1"}

- Erlaube das Übergeben von Nicht-Zeichenketten an res.location mit neuen Kodierungsüberprüfungen

Für eine vollständige Liste der Änderungen in dieser Version siehe [History.md](https://github.com/expressjs/express/blob/master/History.md#4191--2024-03-20)

### 4.19.0 - Veröffentlichungsdatum: 2024-03-20

{: id="4.19.0"}

- Verhindere die Umgehung der Liste durch Encodeurl
- deps: cookie@0.6.0

Für eine vollständige Liste der Änderungen in dieser Version siehe [History.md](https://github.com/expressjs/express/blob/master/History.md#4190--2024-03-20)

### 4.18.3 - Veröffentlichungsdatum: 2024-02-29

{: id="4.18.3"}

Das 4.18.3 Patch Release enthält folgende Fehlerbehebung:

<ul>
  <li markdown="1" class="changelog-item">
  Routing Requests ohne Methode beheben. ([commit](https://github.com/expressjs/express/commit/74beeac0718c928b4ba249aba3652c52fbe32ca8))  
</li>
</ul>

Für eine vollständige Liste der Änderungen in dieser Version siehe [History.md](https://github.com/expressjs/express/blob/master/History.md#4183--2024-02-26)

### 4.18.2 - Veröffentlichungsdatum: 2022-10-08

{: id="4.18.2"}

Das 4.18.2 Patch Release enthält folgende Fehlerbehebung:

<ul>
  <li markdown="1" class="changelog-item">
  Fix Regression Routing eines großen Stacks in einer einzigen Route. ([commit](https://github.com/expressjs/express/commit/7ec5dd2b3c5e7379f68086dae72859f5573c8b9b))  
</li>
</ul>

Für eine vollständige Liste der Änderungen in dieser Version siehe [History.md](https://github.com/expressjs/express/blob/master/History.md#4182--2022-10-08)

### 4.18.1 - Veröffentlichungsdatum: 2022-04-29

{: id="4.18.1"}

Der Patch 4.18.1 enthält folgende Fehlerbehebung:

<ul>
  <li markdown="1" class="changelog-item">
  Repariere die Bedingung, in der wenn eine Express-Anwendung mit einem sehr großen Stapel von Routen erstellt wird, und alle diese Routen sind synchron (Aufruf `next()` synchronisiert), dann kann die Anfragebearbeitung hängen.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4181--2022-04-29).

### 4.18.0 - Veröffentlichungsdatum: 2022-04-25

{: id="4.18.0"}

Die kleine 4.18.0 Version enthält Fehlerbehebungen und einige neue Features, einschließlich:

<ul>
  <li markdown="1" class="changelog-item">
  Die [`app.get()` Methode](/{{ page.lang }}/4x/api.html#app.get) und die [`app.set()` Methode](/{{ page.lang }}/4x/api.html#app.set) ignorieren nun Eigenschaften direkt auf `Object.prototype` wenn sie einen Wert erhalten.
  </li>

  <li markdown="1" class="changelog-item">
  Die [`res.cookie()` Methode](/{{ page.lang }}/4x/api.html#res.cookie) akzeptiert nun eine "Priorität" Option, um das Prioritäts-Attribut im Set-Cookie Antwort-Header zu setzen.
  </li>

  <li markdown="1" class="changelog-item">
  Die [`res.cookie()` Methode](/{{ page.lang }}/4x/api.html#res.cookie) lehnt nun ein ungültiges Datumsobjekt ab, das als "expires" Option angegeben wird.
  </li>

  <li markdown="1" class="changelog-item">
  Die [`res.cookie()` Methode](/{{ page.lang }}/4x/api.html#res.cookie) funktioniert jetzt, wenn `null` oder `undefined` explizit als "maxAge"-Argument angegeben wird.
  </li>

  <li markdown="1" class="changelog-item">
  Ab dieser Version unterstützt Express Node.js 18.x.
  </li>

  <li markdown="1" class="changelog-item">
  Die [`res.download()` Methode](/{{ page.lang }}/4x/api.html#res.download) akzeptiert nun eine "Root"-Option, um [`res.sendFile()`](/{{ page.lang }}/4x/api.html#res.sendFile).
  </li>

  <li markdown="1" class="changelog-item">
  Die [`res.download()` Methode](/{{ page.lang }}/4x/api.html#res. ownload) kann mit einem `options` Objekt geliefert werden, ohne ein `filename` Argument anzugeben. Dies vereinfacht Aufrufe, wenn der Standard-`filename` gewünscht wird.
  </li>

  <li markdown="1" class="changelog-item">
  Die [`res.format()` Methode](/{{ page.lang }}/4x/api.html#res.format) ruft nun den angegebenen "default" Handler mit den gleichen Argumenten wie die Typ-Handler (`req`, `res` und `next`) auf.
  </li>

  <li markdown="1" class="changelog-item">
  Die [`res.send()` Methode](/{{ page.lang }}/4x/api.html#res.send) wird nicht versuchen, einen Antworttext zu senden, wenn der Antwortcode auf 205 gesetzt ist.
  </li>

  <li markdown="1" class="changelog-item">
  Der Standard-Fehlerbehandler wird nun bestimmte Antwort-Header entfernen, die die Fehlerreaktionsdarstellung zerstören, wenn sie zuvor gesetzt wurden.
  </li>

  <li markdown="1" class="changelog-item">
  Der Statuscode 425 wird jetzt als Standard "Zu früher" anstelle von "Ungeordnete Sammlung" dargestellt.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4180--2022-04-25).

### 4.17.3 - Veröffentlichungsdatum: 2022-02-16

{: id="4.17.3"}

Das 4.17.3 Patch Release enthält eine Fehlerbehebung:

<ul>
  <li markdown="1" class="changelog-item">
  Update auf [qs module](https://www.npmjs.com/package/qs) für eine Korrektur um `__proto__` Eigenschaften zu parsen.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4173--2022-02-16).

### 4.17.2 - Veröffentlichungsdatum: 2021-12-16

{: id="4.17.2"}

Der Patch 4.17.2 enthält folgende Fehlerbehebungen:

<ul>
  <li markdown="1" class="changelog-item">
  Fix Behandlung von `undefined` in `res.jsonp` wenn ein Callback angegeben ist.
  </li>

  <li markdown="1" class="changelog-item">
  Fix Umgang mit `undefined` in `res.json` und `res.jsonp` wenn `"json escape"` aktiviert ist.
  </li>

  <li markdown="1" class="changelog-item">
  Fehlerbehebung ungültiger Werte mit der Option `maxAge` von `res.cookie()`.
  </li>

  <li markdown="1" class="changelog-item">
  Update auf [jshttp/proxy-addr module](https://www.npmjs.com/package/proxy-addr), um `req.socket` über veraltete `req.connection` zu verwenden.
  </li>

  <li markdown="1" class="changelog-item">
  Ab dieser Version unterstützt Express Node.js 14.x.
  </li>

</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4172--2021-12-16).

### 4.17.1 - Veröffentlichungsdatum: 2019-05-25

{: id="4.17.1"}

Der Patch 4.17.1 enthält eine Fehlerbehebung:

<ul>
  <li markdown="1" class="changelog-item">
  Die Änderung der `res.status()` API wurde rückgängig gemacht, da sie in bestehenden Express 4 Anwendungen Regressionen verursacht.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4171--2019-05-25).

### 4.17.0 - Veröffentlichungsdatum: 2019-05-16

{: id="4.17.0"}

Die kleine Version 4.17.0 enthält Fehlerbehebungen und einige neue Features, einschließlich:

<ul>
  <li markdown="1" class="changelog-item">
  Die Middleware `express.raw()` und `express.text()` wurden hinzugefügt, um Request-Body für weitere Roh-Payloads zu parsen. Dies verwendet das untere Modul [express js/body-parser] (https://www.npmjs.com/package/body-parser), so dass Apps, die das Modul derzeit separat benötigen, zu den eingebauten Parsern wechseln können.
  </li>

  <li markdown="1" class="changelog-item">
  Die `res.cookie()` API unterstützt nun den `"none"` Wert für die `sameSite` Option.
  </li>

  <li markdown="1" class="changelog-item">
  Wenn die `"trust proxy"` Einstellung aktiviert ist, unterstützt der `req.hostname` nun mehrere `X-Forwarded-For`-Header.
  </li>

  <li markdown="1" class="changelog-item">
  Ab dieser Version unterstützt Express Node.js 10.x und 12.x.
  </li>

  <li markdown="1" class="changelog-item">
  Die API `res.sendFile()` bietet jetzt und leichter zu verstehen Fehler, wenn ein Nicht-String als Argument `path` übergeben wird.
  </li>

  <li markdown="1" class="changelog-item">
  Die `res.status()` API bietet jetzt und schneller und leichter zu verstehen Fehler, wenn `null` oder `undefined` als Argument übergeben wird.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4170--2019-05-16).

### 4.16.4 - Veröffentlichungsdatum: 2018-10-10

{: id="4.16.4"}

Das 4.16.4 Patch Release enthält verschiedene Fehlerbehebungen:

<ul>
  <li markdown="1" class="changelog-item">
  Beheben des Problems, bei dem `"Request abgebrochen"` in `res.sendfile` eingeloggt werden kann.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4164--2018-10-10).

### 4.16.3 - Veröffentlichungsdatum: 2018-03-12

{: id="4.16.3"}

Das 4.16.3 Patch Release enthält verschiedene Fehlerbehebungen:

<ul>
  <li markdown="1" class="changelog-item">
  Beheben Sie ein Problem, wo ein einfacher `%` am Ende der Url in den `res. ocation` Methode oder die `res.redirect` Methode würde nicht als `%25` kodiert werden.
  </li>

  <li markdown="1" class="changelog-item">
  Behebt ein Problem, bei dem ein leerer `req.url` Wert zu einem Auswurffehler innerhalb der Standardbehandlung 404 führen kann.
  </li>

  <li markdown="1" class="changelog-item">
  Fix das generierte HTML-Dokument für `express.static` redirect Antworten auf korrekt einfügen `</html>`.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4163--2018-03-12).

### 4.16.2 - Veröffentlichungsdatum: 2017-10-09

{: id="4.16.2"}

Das 4.16.2 Patch Release enthält eine Regressionsfehlerbehebung:

<ul>
  <li markdown="1" class="changelog-item">
  Fix einen `TypeError` der in der `res.send` Methode auftreten kann, wenn ein `Buffer` an `res übergeben wird. end` und der `ETag` Header ist bereits auf der Antwort festgelegt.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4162--2017-10-09).

### 4.16.1 - Veröffentlichungsdatum: 2017-09-29

{: id="4.16.1"}

Der Patch 4.16.1 enthält einen Fehler in Regression:

<ul>
  <li markdown="1" class="changelog-item">
  Aktualisiere auf [pillarjs/send module](https://www.npmjs.com/package/send), um eine rückläufige Fallszenario Regression zu beheben, die bestimmte Benutzer von `express.static` betroffen hat.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4161--2017-09-29).

### 4.16.0 - Veröffentlichungsdatum: 2017-09-28

{: id="4.16.0"}

Die kleine 4.16.0 Version enthält Sicherheitsaktualisierungen, Fehlerbehebungen, Leistungsverbesserungen und einige neue Features, einschließlich:

<ul>
  <li markdown="1" class="changelog-item">
  Aktualisiere auf [jshttp/forwarded module](https://www.npmjs.com/package/forwarded), um eine [vulnerability](https://npmjs.com/advisories/527). Dies kann Ihre Anwendung beeinflussen, wenn die folgenden APIs verwendet werden: `req.host`, `req.hostname`, `req.ip`, `req.ips`, `req.protocol`.
  </li>

  <li markdown="1" class="changelog-item">
  Aktualisiere eine Abhängigkeit von [pillarjs/send module](https://www.npmjs.com/package/send), um eine [vulnerability](https://npmjs.com/advisories/535) in der `mime`-Abhängigkeit zu adressieren. Dies kann Ihre Anwendung beeinflussen, wenn nicht vertrauenswürdige Zeichenketteneingabe an die folgende APIs übergeben wird: `res.type()`.
  </li>

  <li markdown="1" class="changelog-item">
  Das [pillarjs/send module](https://www.npmjs.com/package/send) hat einen Schutz gegen die Node.js 8.5.0 [vulnerability](https://nodejs.org/en/blog/vulnerability/september-2017-path-validation/ ) implementiert. Die Verwendung einer früheren Version von Express mit Node.js 8.5.0 (dieser speziellen Node.js Version) wird folgende APIs verwundbar machen: `express.static`, `res.sendfile` und `res.sendFile`.
  </li>

  <li markdown="1" class="changelog-item">
  Ab dieser Version unterstützt Express Node.js 8.x.
  </li>

  <li markdown="1" class="changelog-item">
  Die neue Einstellung `"json escape"` kann aktiviert werden, um Zeichen in `res.json()`, `res.jsonp()` und `res. end()` Antworten, die Clients dazu veranlassen können, die Antwort als HTML zu schnüffeln, anstatt das `Content-Type` zu ehren. Dies kann helfen, eine Express-App vor einer Klasse persistenter XSS-basierter Angriffe zu schützen.
  </li>

  <li markdown="1" class="changelog-item">
  Die [`res.download()` Methode](/{{ page.lang }}/4x/api.html#res.download) akzeptiert nun ein optionales `options` Objekt.
  </li>

  <li markdown="1" class="changelog-item">
  Die Middleware `express.json()` und `express.urlencoded()` wurden hinzugefügt. Dies verwendet das untere Modul [express js/body-parser] (https://www.npmjs.com/package/body-parser), so dass Apps, die das Modul derzeit separat benötigen, zu den eingebauten Parsern wechseln können.
  </li>

  <li markdown="1" class="changelog-item">
  Die [`express.static()` middleware](/{{ page.lang }}/4x/api.html#express.static) und [`res.sendFile()` Methode](/{{ page.lang }}/4x/api.html#res.sendFile) unterstützen nun das Setzen der `immutable` Direktive auf dem `Cache-Control` Header. Wenn Sie diesen Header mit einem passenden `maxAge` einstellen, wird verhindert, dass Web-Browser jede Anfrage an den Server senden, wenn die Datei noch in ihrem Cache liegt.
  </li>

  <li markdown="1" class="changelog-item">
  Das [pillarjs/send module](https://www.npmjs.com/package/send) hat eine aktualisierte Liste von MIME-Typen, um das `Content-Type` von mehr Dateien besser zu setzen. Es gibt 70 neue Typen für Dateierweiterungen.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4160--2017-09-28).

### 4.15.5 - Veröffentlichungsdatum: 2017-09-24

{: id="4.15.5"}

Das 4.15.5 Patch Release beinhaltet Sicherheitsupdates, einige kleinere Leistungsverbesserungen und eine Fehlerbehebung:

<ul>
  <li markdown="1" class="changelog-item">
  Aktualisiere auf [Debug-Modul](https://www.npmjs.com/package/debug), um eine [vulnerability](https://snyk.io/vuln/npm:debug:20170905), aber dieses Problem wirkt sich nicht auf Express aus.
  </li>

  <li markdown="1" class="changelog-item">
  Aktualisiere auf [jshttp/fresh module](https://www.npmjs.com/package/fresh) um eine [vulnerability](https://npmjs.com/advisories/526). Dies wird deine Anwendung beeinflussen, wenn die folgenden APIs verwendet werden: `express.static`, `req.fresh`, `res.json`, `res.jsonp`, `res.send`, `res.sendfile` `res.sendFile`, `res.sendStatus`.
  </li>

  <li markdown="1" class="changelog-item">
  Update to [jshttp/fresh module](https://www.npmjs.com/package/fresh) fixes handling of modified headers with invalid dates and makes parsing conditional headers (like `If-None-Match`) faster.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4155--2017-09-24).

### 4.15.4 - Veröffentlichungsdatum: 2017-08-06

{: id="4.15.4"}

Das 4.15.4 Patch Release enthält einige kleinere Bugfixes:

<ul>
  <li markdown="1" class="changelog-item">
  Fix array wird für den Wert `"trust proxy"` gesetzt, der unter bestimmten Bedingungen manipuliert wird.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4154--2017-08-06).

### 4.15.3 - Veröffentlichungsdatum: 2017-05-16

{: id="4.15.3"}

Das 4.15.3 Patch Release enthält ein Sicherheitsupdate und einige kleinere Fehlerbehebungen:

<ul>
  <li markdown="1" class="changelog-item">
  Aktualisiere eine Abhängigkeit von [pillarjs/send module](https://www.npmjs.com/package/send), um eine [vulnerability](https://snyk.io/vuln/npm:ms:20170412). Dies kann Ihre Anwendung beeinflussen, wenn die nicht vertrauenswürdige Eingabe an die Option `maxAge` in der folgenden APIs übergeben wird: `express.static`, `res.sendfile` und `res.sendFile`.
  </li>

  <li markdown="1" class="changelog-item">
  Fehler behoben, wenn `res.set` den Zeichensatz `Content-Type` nicht hinzufügen kann.
  </li>

  <li markdown="1" class="changelog-item">
  Fix missing `</html>` in HTML Dokument.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4153--2017-05-16).

### 4.15.2 - Veröffentlichungsdatum: 2017-03-06

{: id="4.15.2"}

Das 4.15.2 Patch Release enthält eine kleine Fehlerbehebung:

<ul>
  <li markdown="1" class="changelog-item">
  Fix Regression Parsing-Schlüssel beginnend mit `[` im erweiterten (Standard) Abfrage-Parser.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4152--2017-03-06).

### 4.15.1 - Veröffentlichungsdatum: 2017-03-05

{: id="4.15.1"}

Die Patchversion 4.15.1 enthält eine kleine Fehlerbehebung:

<ul>
  <li markdown="1" class="changelog-item">
  Beheben Sie Kompatibilitätsprobleme, wenn Sie die datejs 1.x Bibliothek verwenden, in der die [`express.static()` middleware](/{{ page.lang }}/4x/api.html#express. tatic) und [`res.sendFile()` Methode](/{{ page.lang }}/4x/api.html#res.sendFile) würden falsch mit 412 Voraussetzungen reagieren fehlgeschlagen.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4151--2017-03-05).

### 4.15.0 - Veröffentlichungsdatum: 2017-03-01

{: id="4.15.0"}

Die kleine 4.15.0 Version enthält Fehlerkorrekturen, Leistungsverbesserungen und weitere kleinere Features, einschließlich:

<ul>
  <li markdown="1" class="changelog-item">
  Ab dieser Version unterstützt Express Node.js 7.x.
  </li>

  <li markdown="1" class="changelog-item">
  Die [`express.static()` Middleware](/{{ page.lang }}/4x/api.html#express.static) und [`res.sendFile()` Methode](/{{ page.lang }}/4x/api.html#res.sendFile) unterstützen nun die `If-Match` und `If-Unmodified-Since` Anfrage-Header.
  </li>

  <li markdown="1" class="changelog-item">
  Aktualisiere auf [jshttp/etag module](https://www.npmjs.com/package/etag) um die Standard-ETags für Antworten zu generieren, die funktionieren, wenn Node.js [FIPS-konforme Krypto aktiviert](https://nodejs.org/dist/latest/docs/api/cli.html#cli_enable_fips).
  </li>

  <li markdown="1" class="changelog-item">
  Verschiedene automatisch generierte HTML-Antworten wie die Standardeinstellung nicht gefunden und Fehlerbehandler werden mit kompletten HTML-5-Dokumenten und zusätzlichen Sicherheitskopien antworten.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4150--2017-03-01).

### 4.14.1 - Veröffentlichungsdatum: 2017-01-28

{: id="4.14.1"}

Das 4.14.1 Patch Release enthält Fehlerkorrekturen und Leistungsverbesserungen, einschließlich:

<ul>
  <li markdown="1" class="changelog-item">
  Update auf [pillarjs/finalhandler module](https://www.npmjs.com/package/finalhandler) behebt eine Ausnahme, wenn Express ein `Error` Objekt behandelt, das eine `headers` Eigenschaft hat, die kein Objekt ist.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4141--2017-01-28).

### 4.14.0 - Veröffentlichungsdatum: 2016-06-16

{: id="4.14.0"}

Die Version 4.14.0 enthält Fehlerkorrekturen, Sicherheitsupdates, Leistungsverbesserungen und weitere kleinere Features, einschließlich:

<ul>
  <li markdown="1" class="changelog-item">
  Ab dieser Version unterstützt Express Node.js 6.x.
  </li>

  <li markdown="1" class="changelog-item">
  Update auf [jshttp/negotiator module](https://www.npmjs.com/package/negotiator) behebt eine [reguläre Ausdruck Denial of Service Verwundbarkeit](https://npmjs.com/advisories/106).
  </li>

  <li markdown="1" class="changelog-item">
  Die [`res.sendFile()` Methode](/{{ page.lang }}/4x/api.html#res.sendFile) akzeptiert nun zwei neue Optionen: `acceptRanges` und `cacheControl`.

- `acceptRanges` (defaut is `true`), aktiviert oder deaktiviert das Akzeptieren von Distanzanfragen. Wenn deaktiviert, sendet die Antwort nicht den `Accept-Ranges` Header und ignoriert den Inhalt des `Range` Request-Headers.

- `cacheControl`, (Standard ist `true`), aktiviert oder deaktiviert den `Cache-Control` Response-Header. Deaktivieren wird die `maxAge` Option ignorieren.

- `res.sendFile` wurde ebenfalls aktualisiert, um `Range` Header und Umleitungen besser zu handhaben.

  </li>

  <li markdown="1" class="changelog-item">
  Die [`res.location()` Methode](/{{ page.lang }}/4x/api.html#res.location) und [`res.redirect()` Methode](/{{ page.lang }}/4x/api.html#res.redirect) werden nun den URL-String kodieren, falls er nicht bereits kodiert ist.
  </li>

  <li markdown="1" class="changelog-item">
  Die Leistung der [`res.json()` Methode](/{{ page.lang }}/4x/api.html#res.json) und [`res.jsonp()` Methode](/{{ page.lang }}/4x/api.html#res.jsonp) wurden in den gebräuchlichen Fällen verbessert.
  </li>

  <li markdown="1" class="changelog-item">
  Das [jshttp/cookie Modul](https://www.npmjs.com/package/cookie) (zusätzlich zu einer Reihe anderer Verbesserungen) wurde aktualisiert und nun die [`res. ookie()` Methode](/{{ page.lang }}/4x/api.html#res.cookie) unterstützt die `sameSite` Option um das [SameSite Cookie Attribut ]anzugeben (https://tools.ietf.org/html/draft-west-first-party-cookies-07).  

{% include admonitions/note.html content="Dieses Attribut ist noch nicht vollständig standardisiert, kann sich in der Zukunft ändern und viele Clients können es ignorieren." %}

Der mögliche Wert für die Option `sameSite` ist:

- `true`, welches das `SameSite`-Attribut auf `Strict` setzt, um dieselbe Site-Durchsetzung strikt durchzuführen.
- `false`, welches nicht das `SameSite`-Attribut setzt.
- `'lax'`, welches das `SameSite`-Attribut auf `Lax` für die lax gleiche Site-Durchsetzung setzt.
- `'strict`, was das `SameSite`-Attribut auf `Strict` setzt, um dieselbe Site-Durchsetzung strikt durchzuführen.

  </li>

  <li markdown="1" class="changelog-item">
  Absolute Pfadprüfung unter Windows, die in einigen Fällen falsch war, wurde behoben.
  </li>

  <li markdown="1" class="changelog-item">Die Auflösung der 
  IP-Adresse mit Proxies wurde erheblich verbessert.
  </li>

  <li markdown="1" class="changelog-item">
  Die [`req.range()` Methode](/{{ page.lang }}/4x/api.html#req. angezeigt) Optionsobjekt unterstützt nun eine `combine` Option (`false` standardmäßig), was bedeutet, wenn `true`, kombiniert überlappende und benachbarte Bereiche und gibt sie als ob sie auf diese Weise im Header angegeben worden wären.
  </li>
</ul>

Eine vollständige Liste der Änderungen in dieser Version finden Sie unter [History.md](https://github.com/expressjs/express/blob/master/History.md#4140--2016-06-16).

</div>
