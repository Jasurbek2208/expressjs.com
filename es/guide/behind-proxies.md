---
layout: page
title: Express detrás de proxies
description: Aprenda cómo configurar las aplicaciones Express.js para que funcionen correctamente detrás de los proxies inversos, incluyendo el uso de la configuración del proxy de confianza para manejar las direcciones IP del cliente.
menu: guide
lang: es
redirect_from: ""
---

# Express detrás de proxies

Cuando se ejecuta una aplicación Express detrás de un proxy inverso, algunas de las APIs Express pueden devolver valores diferentes de los esperados. Para ajustarse a esto, la configuración de la aplicación `trust proxy` puede utilizarse para exponer la información proporcionada por el proxy inverso en las APIs Express. El problema más común son las APIs expresas que exponen la dirección IP del cliente pueden mostrar una dirección IP interna del proxy inverso.

<div class="doc-box doc-info" markdown="1">
Cuando se configura la configuración del `proxy de confianza`, es importante entender la configuración exacta del proxy inverso. Dado que esta configuración confiará en los valores proporcionados en la solicitud, es importante que la combinación de la configuración en Express coincida con el funcionamiento del proxy inverso.
</div>

El ajuste de la aplicación `proxy de confianza` puede establecerse en uno de los valores listados en la siguiente tabla.

<table class="doctable" border="1" markdown="1">
  <thead><tr><th>Tipo</th><th>Valor</th></tr></thead>
  <tbody>
    <tr>
      <td>Boolean</td>
<td markdown="1">
Si es `true`, la dirección IP del cliente se entiende como la entrada más a la izquierda en la cabecera `X-Forwarded-For`.

Si es `false`, la aplicación se entiende como directamente frente al cliente y la dirección IP del cliente se deriva de `req.socket.remoteAddress`. Esta es la configuración por defecto.

<div class="doc-box doc-warn" markdown="1">
When setting to `true`, it is important to ensure that the last reverse proxy trusted is removing/overwriting all of the following HTTP headers: `X-Forwarded-For`, `X-Forwarded-Host`, and `X-Forwarded-Proto`, otherwise it may be possible for the client to provide any value.
</div>
</td>
    </tr>
    <tr>
      <td>IP addresses</td>
<td markdown="1">
An IP address, subnet, or an array of IP addresses and subnets to trust as being a reverse proxy. The following list shows the pre-configured subnet names:

- bucle atrás - `127.0.0.1/8`, `::1/128`
- linklocal - `169.254.0.0/16`, `fe80::/10`
- uniquelocal - `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, `fc00::/7`

Puede establecer direcciones IP de cualquiera de las siguientes maneras:

```js
app.set('trust proxy', 'loopback') // specify a single subnet
app.set('trust proxy', 'loopback, 123.123.123.123') // specify a subnet and an address
app.set('trust proxy', 'loopback, linklocal, uniquelocal') // specify multiple subnets as CSV
app.set('trust proxy', ['loopback', 'linklocal', 'uniquelocal']) // specify multiple subnets as an array
```

Cuando se especifica, las direcciones IP o las subredes están excluidas del proceso de determinación de direcciones, y la dirección IP no confiable más cercana al servidor de aplicaciones se determina como la dirección IP del cliente. Esto funciona comprobando si `req.socket.remoteAddress` es de confianza. Si es así, entonces cada dirección en `X-Forwarded-For` se marca de derecha a izquierda hasta la primera dirección no confiable.

</td>
    </tr>
    <tr>
      <td>Número</td>
<td markdown="1">
Utilice la dirección que es como máximo el número de saltos `n` de la aplicación Express. `req.socket.remoteAddress` es la primera salida, y el resto son buscados en la cabecera `X-Forwarded-For` de derecha a izquierda. Un valor de `0` significa que la primera dirección no confiable sería `req.socket.remoteAddress`, es decir, no hay proxy inverso.

<div class="doc-box doc-warn" markdown="1">
When using this setting, it is important to ensure there are not multiple, different-length paths to the Express application such that the client can be less than the configured number of hops away, otherwise it may be possible for the client to provide any value.
</div>
</td>
    </tr>
    <tr>
      <td>Function</td>
<td markdown="1">
Custom trust implementation.

```js
app.set('trust proxy', (ip) => {
  if (ip === '127.0.0.1' || ip === '123.123.123.123') return true // trusted IPs
  else return false
})
```

</td>
    </tr>
  </tbody>
</table>

Habilitar `proxy de confianza` tendrá el siguiente impacto:

<ul>
  <li markdown="1">El valor de [req.hostname](/{{ page.lang }}/api.html#req.hostname) se obtiene del valor definido en la cabecera `X-Forwarded-Host`, que puede estar establecido por el cliente o el proxy.
  </li>
  <li markdown="1">`X-Forwarded-Proto` puede ser establecido por el proxy inverso para decirle a la aplicación si es `https` o `http` o incluso un nombre no válido. Este valor se refleja en [req.protocol](/{{ page.lang }}/api.html#req.protocol).
  </li>
  <li markdown="1">El [req.ip](/{{ page.lang }}/api.html#req.ip) y [req.ips](/{{ page.lang }}/api.html#req. ps) son poblados basándose en la dirección del socket y en el encabezado `X-Forwarded-For`, comenzando en la primera dirección no confiable.
  </li>
</ul>

La configuración `trust proxy` se implementa usando el paquete [proxy-addr](https://www.npmjs.com/package/proxy-addr). Para obtener más información, consulte su documentación.
