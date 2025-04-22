---
layout: page
title: Exprimez derrière les mandataires
description: Apprenez à configurer les applications Express.js pour qu'elles fonctionnent correctement derrière les mandataires inversés, y compris en utilisant le paramètre proxy de confiance pour gérer les adresses IP du client.
menu: guide
lang: fr
redirect_from: ""
---

# Exprimez derrière les mandataires

Lorsque vous exécutez une application Express derrière un proxy inverse, certaines des API Express peuvent retourner des valeurs différentes de celles attendues. Pour ajuster pour cela, le paramètre `trust proxy` de l'application peut être utilisé pour exposer des informations fournies par le proxy inverse dans les API Express. Le problème le plus courant est les API express qui exposent l'adresse IP du client peut à la place afficher une adresse IP interne du proxy inverse.

<div class="doc-box doc-info" markdown="1">
Lors de la configuration du paramètre `trust proxy`, il est important de comprendre la configuration exacte du proxy inverse. Puisque ce paramètre fera confiance aux valeurs fournies dans la requête, il est important que la combinaison du paramètre dans Express corresponde au fonctionnement du mandataire inverse.
</div>

Le paramètre de l'application `trust proxy` peut être défini à l'une des valeurs listées dans la table suivante.

<table class="doctable" border="1" markdown="1">
  <thead><tr><th>Type de texte</th><th>Valeur</th></tr></thead>
  <tbody>
    <tr>
      <td>Boolean</td>
<td markdown="1">
Si `true`, l'adresse IP du client est comprise comme l'entrée la plus à gauche dans l'en-tête `X-Forwarded-For`.

Si `false`, l'application est comprise comme faisant directement face au client et l'adresse IP du client est dérivée de `req.socket.remoteAddress`. Ceci est le paramètre par défaut.

<div class="doc-box doc-warn" markdown="1">
Lorsque vous définissez sur `true`, il est important de s'assurer que le dernier reverse proxy fiable est de supprimer/écraser tous les en-têtes HTTP suivants : `X-Forwarded-For`, `X-Forwarded-Host`, et `X-Forwarded-Proto`, sinon il sera possible pour le client de fournir n'importe quelle valeur.
</div>
</td>
    </tr>
    <tr>
      <td>IP addresses</td>
<td markdown="1">
An IP address, subnet, or an array of IP addresses and subnets to trust as being a reverse proxy. The following list shows the pre-configured subnet names:

- loopback - `127.0.0.1/8`, `::1/128`
- linklocal - `169.254.0.0/16`, `fe80::/10`
- uniquelocal - `10.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, `fc00::/7`

Vous pouvez définir les adresses IP de l'une des façons suivantes :

```js
app.set('trust proxy', 'loopback') // specify a single subnet
app.set('trust proxy', 'loopback, 123.123.123.123') // specify a subnet and an address
app.set('trust proxy', 'loopback, linklocal, uniquelocal') // specify multiple subnets as CSV
app.set('trust proxy', ['loopback', 'linklocal', 'uniquelocal']) // specify multiple subnets as an array
```

Lorsqu'il est spécifié, les adresses IP ou les sous-réseaux sont exclus du processus de détermination de l'adresse, et l'adresse IP non fiable la plus proche du serveur d'application est déterminée comme l'adresse IP du client. Cela fonctionne en vérifiant si `req.socket.remoteAddress` est fiable. Si c'est le cas, alors chaque adresse dans `X-Forwarded-For` est vérifiée de droite à gauche jusqu'à la première adresse non fiable.

</td>
    </tr>
    <tr>
      <td>Numéros</td>
<td markdown="1">
Utilisez l'adresse qui est au plus `n` nombre de sauts loin de l'application Express. `req.socket.remoteAddress` est le premier saut, et le reste est recherché dans l'en-tête `X-Forwarded-For` de droite à gauche. Une valeur de `0` signifie que la première adresse non fiable serait `req.socket.remoteAddress`, c'est-à-dire qu'il n'y a pas de proxy inverse.

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

Activer `trust proxy` aura l'impact suivant :

<ul>
  <li markdown="1">La valeur de [req.hostname](/{{ page.lang }}/api.html#req. ostname) est dérivé de la valeur définie dans l'en-tête `X-Forwarded-Host`, qui peut être définie par le client ou par le proxy.
  </li>
  <li markdown="1">`X-Forwarded-Proto` peut être défini par le proxy inverse pour dire à l'application si c'est `https` ou `http` ou même un nom invalide. Cette valeur est reflétée par [req.protocol](/{{ page.lang }}/api.html#req.protocol).
  </li>
  <li markdown="1">Les valeurs [req.ip](/{{ page.lang }}/api.html#req.ip) et [req.ips](/{{ page.lang }}/api.html#req.ips) sont renseignées avec la liste des adresses provenant de `X-Forwarded-For`.
  </li>
</ul>

Le paramètre `trust proxy` est implémenté en utilisant le paquet [proxy-addr](https://www.npmjs.com/package/proxy-addr). Pour plus d'informations, voir sa documentation.
