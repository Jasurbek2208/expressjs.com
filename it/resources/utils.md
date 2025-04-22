---
layout: page
title: Utilità Express
description: Scopri i moduli di utilità relativi a Express.js e Node.js, inclusi strumenti per cookie, protezione CSRF, analisi URL, routing e molto altro per migliorare le tue applicazioni.
menu: resources
lang: it
redirect_from: ""
---

## Funzioni di utilità Express

L'organizzazione [pillarjs](https://github.com/pillarjs) GitHub contiene una serie di moduli
per funzioni di utilità che possono essere generalmente utili.

| Moduli di utilità                                              | Descrizione                                                                                                                                                                                                                                                   |
| -------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [cookies](https://www.npmjs.com/package/cookies)               | Ottieni e imposta i cookie HTTP(S) che possono essere firmati per evitare manomissioni, utilizzando Keygrip. Può essere utilizzato con la libreria HTTP Node.js o come middleware Express. |
| [csrf](https://www.npmjs.com/package/csrf)                     | Contiene la logica dietro la creazione e la verifica del token CSRF.  Usa questo modulo per creare middleware CSRF personalizzato.                                                                                            |
| [finalhandler](https://www.npmjs.com/package/finalhandler)     | Funzione di invocare come passo finale per rispondere alla richiesta HTTP.                                                                                                                                                                    |
| [parseurl](https://www.npmjs.com/package/parseurl)             | Analizza un URL con la cache.                                                                                                                                                                                                                 |
| [path-match](https://www.npmjs.com/package/path-match)         | Sottile wrapper intorno a [path-to-regexp](https://github.com/component/path-to-regexp) per rendere più facile l'estrazione dei nomi dei parametri.                                                                                           |
| [path-to-regexp](https://www.npmjs.com/package/path-to-regexp) | Trasforma una stringa di percorso in stile Express, come \`\`/user/:name\` in un'espressione regolare.                                                                                                                        |
| [resolve-path](https://www.npmjs.com/package/resolve-path)     | Risolve un percorso relativo contro un percorso radice con convalida.                                                                                                                                                                         |
| [router](https://www.npmjs.com/package/router)                 | Semplice router in stile middleware.                                                                                                                                                                                                          |
| [routington](https://www.npmjs.com/package/routington)         | Router URL basato su tre per definire e abbinare gli URL.                                                                                                                                                                                     |
| [send](https://www.npmjs.com/package/send)                     | Libreria per lo streaming di file come risposta HTTP, con supporto per risposte parziali (intervalli), negoziazione condizionale-GET ed eventi granulari.                                                                  |
| [templation](https://www.npmjs.com/package/templation)         | Visualizza sistema simile a `res.render()` ispirato a [co-views](https://github.com/visionmedia/co-views) e [consolidate.js](https://github.com/visionmedia/consolidate.js/).                                                 |

Per ulteriori moduli correlati all'HTTP di basso livello, vedere [jshttp](http://jshttp.github.io/).
