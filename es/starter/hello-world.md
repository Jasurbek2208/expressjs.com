---
layout: page
title: Ejemplo exprés "Hola Mundo"
description: Comienza con Express.js construyendo una sencilla aplicación 'Hola Mundo', demostrando la configuración básica y la creación de servidores para principiantes.
menu: starter
lang: es
redirect_from: ""
---

# Hola ejemplo de mundo

<div class="doc-box doc-info" markdown="1">
Incrustado a continuación es esencialmente la aplicación Express más simple que puede crear. Es una aplicación de archivo única &mdash; _no_ lo que obtendrías si utilizas el [generador Express](/{{ page.lang }}/starter/generator. tml), que crea el scaffolding para una aplicación completa con numerosos archivos JavaScript, plantillas de Jade y subdirectorios para varios propósitos.
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

Esta aplicación inicia un servidor y escucha en el puerto 3000 para las conexiones. La aplicación responde con "¡Hola Mundo!" para las solicitudes
a la URL raíz (`/`) o _route_. Por cada otro camino, responderá con un **404 No Encontrado**.

### Ejecutar localmente

Primero cree un directorio llamado `myapp`, cámbielo y ejecute `npm init`. Luego, instala `express` como una dependencia, según la [guía de instalación](/{{ page.lang }}/starter/installing.html).

En el directorio `myapp`, crea un archivo llamado `app.js` y copia el código del ejemplo anterior.

<div class="doc-box doc-notice" markdown="1">
`req` (solicitud) y `res` (respuesta) son exactamente los mismos objetos que proporciona Node, por lo que puede invocar `req.pipe()`, `req.on('data', callback)` y cualquier otro objeto que invocaría sin estar Express implicado.
</div>

Ejecutar la aplicación con el siguiente comando:

```bash
$ node app.js
```

Luego, carga `http://localhost:3000/` en un navegador para ver la salida.

### [Anterior: Instalar ](/{{ page.lang }}/starter/installing.html)&nbsp;&nbsp;&nbsp;&nbsp;[Siguiente: Express Generator ](/{{ page.lang }}/starter/generator.html)
