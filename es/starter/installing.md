---
layout: page
title: Instalando Express
description: Aprenda cómo instalar Express.js en su entorno Node.js, incluyendo la configuración del directorio de su proyecto y la gestión de dependencias con npm.
menu: starter
lang: es
redirect_from: ""
---

# Instalando

Suponiendo que ya has instalado [Node.js](https://nodejs.org/), crea un directorio para mantener tu aplicación y haz ese directorio de trabajo.

- [Express 4.x](/{{ page.lang }}/4x/api.html) requiere 0.10 o superior de Node.js.
- [Express 5.x](/{{ page.lang }}/5x/api.html) requiere Node.js 18 o superior.

```bash
$ mkdir myapp
$ cd myapp
```

Usa el comando `npm init` para crear un archivo `package.json` para tu aplicación.
Para más información sobre el funcionamiento de `package.json`, consulta [Especificaciones del manejo de package.json de npm](https://docs.npmjs.com/files/package.json).

```bash
$ npm init
```

Este comando te pide varias cosas, como el nombre y la versión de tu aplicación.
Por ahora, puede simplemente pulsar RETURN para aceptar los valores predeterminados para la mayoría de ellos, con la siguiente excepción:

```
entry point: (index.js)
```

Introduzca `app.js`, o lo que quiera que sea el nombre del archivo principal. Si desea que sea `index.js`, pulse RETURN para aceptar el nombre de archivo predeterminado sugerido.

Ahora, instale Express en el directorio `myapp` y guárdelo en la lista de dependencias. Por ejemplo:

```bash
$ npm install express
```

Para instalar Express temporalmente y no añadirlo a la lista de dependencias:

```bash
$ npm install express --no-save
```

<div class="doc-box doc-info" markdown="1">
Por defecto con la versión npm 5.0+, `npm install` añade el módulo a la lista de `dependencies` en el `paquete. archivo son`; con versiones anteriores de npm, debe especificar explícitamente la opción `--save`. Después, ejecutar `npm install` en el directorio de aplicaciones instalará automáticamente los módulos en la lista de dependencias.
</div>

### [Siguiente: Hola Mundo](/{{ page.lang }}/starter/hello-world.html)