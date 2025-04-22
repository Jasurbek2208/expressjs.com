---
layout: page
title: Instradamento di base espresso
description: Impara i fondamenti del routing nelle applicazioni Express.js, tra cui come definire i percorsi, gestire i metodi HTTP e creare gestori del percorso per il tuo server web.
menu: starter
lang: it
redirect_from: ""
---

# Instradamento base

_Routing_ si riferisce alla determinazione di come un'applicazione risponde a una richiesta di client a un determinato endpoint, che è un URI (o percorso) e un metodo di richiesta HTTP specifico (GET, POST, e così via).

Ogni percorso può avere una o più funzioni di gestore, che vengono eseguite quando il percorso è abbinato.

La definizione del percorso assume la seguente struttura:

```js
app.METHOD(PATH, HANDLER)
```

Dove:

- `app` è un'istanza di `express`.
- `METHOD` è un [metodo di richiesta HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods), in minuscolo.
- `PATH` è un percorso sul server.
- `HANDLER` è la funzione eseguita quando il percorso è corrispondente.

<div class="doc-box doc-notice" markdown="1">
Questo tutorial presuppone che venga creata un'istanza di `express` chiamata `app` e che il server sia in esecuzione. Se non hai familiarità con la creazione di un'app e l'avvio, vedi l'esempio [Ciao mondo](/{{ page.lang }}/starter/hello-world.html).
</div>

Gli esempi che seguono illustrano la definizione di itinerari semplici.

Rispondi con `Ciao Mondo!` nella homepage:

```js
app.get('/', (req, res) => {
  res.send('Hello World!')
})
```

Rispondi alla richiesta POST sul percorso radice (`/`), la home page dell'applicazione:

```js
app.post('/', (req, res) => {
  res.send('Got a POST request')
})
```

Rispondi a una richiesta PUT al percorso `/user`:

```js
app.put('/user', (req, res) => {
  res.send('Got a PUT request at /user')
})
```

Rispondi a una richiesta DELETE al percorso `/user`:

```js
app.delete('/user', (req, res) => {
  res.send('Got a DELETE request at /user')
})
```

Per maggiori dettagli sul routing, vedere la [guida di routing](/{{ page.lang }}/guide/routing.html).

### [Previous: Express application generator ](/{{ page.lang }}/starter/generator.html)&nbsp;&nbsp;&nbsp;&nbsp;[Next: Servire file statici in Express ](/{{ page.lang }}/starter/static-files.html)