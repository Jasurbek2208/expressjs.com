---
layout: page
title: Ruta básica Express
description: Aprenda los fundamentos de la enrutamiento en aplicaciones Express.js, incluyendo cómo definir rutas, manejar métodos HTTP y crear manejadores de rutas para su servidor web.
menu: starter
lang: es
redirect_from: ""
---

# Ruta básica

_Enrutamiento_ se refiere a determinar cómo responde una aplicación a una solicitud de cliente a un punto final en particular, que es una URI (o ruta) y un método específico de petición HTTP (GET, POST, etc.).

Cada ruta puede tener una o más funciones manejadoras, que se ejecutan cuando la ruta es igualada.

La definición de ruta tiene la siguiente estructura:

```js
app.METHOD(PATH, HANDLER)
```

Donde:

- `app` es una instancia de `express`.
- `METHOD` es un [método de solicitud HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods), en minúsculas.
- `PATH` es una ruta en el servidor.
- `HANDLER` es la función ejecutada cuando la ruta es coincidente.

<div class="doc-box doc-notice" markdown="1">
Este tutorial asume que se crea una instancia de `express` llamada `app` y el servidor se está ejecutando. Si no estás familiarizado con la creación de una aplicación y iniciarla, consulta el [Hola ejemplo del mundo](/{{ page.lang }}/starter/hello-world.html).
</div>

Los siguientes ejemplos ilustran la definición de rutas simples.

Responder con `¡Hola Mundo!` en la página principal:

```js
app.get('/', (req, res) => {
  res.send('Hello World!')
})
```

Respuesta a la solicitud POST en la ruta raíz (`/`), la página de inicio de la aplicación:

```js
app.post('/', (req, res) => {
  res.send('Got a POST request')
})
```

Responder a una solicitud PUT a la ruta `/user`:

```js
app.put('/user', (req, res) => {
  res.send('Got a PUT request at /user')
})
```

Responder a una solicitud DELETE a la ruta `/user`:

```js
app.delete('/user', (req, res) => {
  res.send('Got a DELETE request at /user')
})
```

Para más detalles sobre enrutamiento, consulta la [guía de ruta](/{{ page.lang }}/guide/routing.html).

### [Anterior: generador de aplicaciones exprés ](/{{ page.lang }}/starter/generator.html)&nbsp;&nbsp;&nbsp;&nbsp;[Siguiente: expandiendo archivos estáticos en Express ](/{{ page.lang }}/starter/static-files.html)