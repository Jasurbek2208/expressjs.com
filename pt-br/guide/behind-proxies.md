---
layout: page
title: Expresso atrás dos proxies
description: Aprenda a configurar os aplicativos Express.js para funcionar corretamente atrás de proxies reversas, incluindo o uso do proxy confiável para manipular endereços IP do cliente.
menu: guide
lang: pt-br
redirect_from: ""
---

# Expresso atrás dos proxies

Ao executar um app Expresso atrás de um proxy reverso, alguns das APIs Express podem retornar valores diferentes do esperado. A fim de se ajustar para isto, a configuração do aplicativo `trust proxy` pode ser usada para expor informações fornecidas pelo proxy reverso na API Express. O problema mais comum é expressar APIs que expõem o endereço IP do cliente pode mostrar um endereço IP interno do proxy inverso.

<div class="doc-box doc-info" markdown="1">
Ao configurar a configuração `proxy confiável`, é importante entender a configuração exata do proxy reverso. Como esta configuração confiará nos valores fornecidos na solicitação, é importante que a combinação da configuração no Express corresponda à forma como o proxy reverso funciona.
</div>

A configuração do aplicativo 'proxy confiável' pode ser definida para um dos valores listados na tabela a seguir.

<table class="doctable" border="1" markdown="1">
  <thead><tr><th>tipo</th><th>Valor</th></tr></thead>
  <tbody>
    <tr>
      <td>Boolean</td>
<td markdown="1">
Se `true`, o endereço de IP do cliente será
compreendido como a entrada mais a esquerda no cabeçalho `X-Forwarded-*`.

Se `false`, o aplicativo é entendido como diretamente virado para o cliente e o endereço IP do cliente é derivado de `req.socket.remoteAddress`. Esta é a configuração padrão.

<div class="doc-box doc-warn" markdown="1">
When setting to `true`, it is important to ensure that the last reverse proxy trusted is removing/overwriting all of the following HTTP headers: `X-Forwarded-For`, `X-Forwarded-Host`, and `X-Forwarded-Proto`, otherwise it may be possible for the client to provide any value.
</div>
</td>
    </tr>
    <tr>
      <td>IP addresses</td>
<td markdown="1">
An IP address, subnet, or an array of IP addresses and subnets to trust as being a reverse proxy. The following list shows the pre-configured subnet names:

- loopback - `127.0.0.1/8`, `::1/128`
- linklocal - `169.254.0.0/16`, `fe80::/10`
- uniquelocal - `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, `fc00::/7`

Você pode definir endereços IP das seguintes maneiras:

```js
app.set('trust proxy', 'loopback') // specify a single subnet
app.set('trust proxy', 'loopback, 123.123.123.123') // specify a subnet and an address
app.set('trust proxy', 'loopback, linklocal, uniquelocal') // specify multiple subnets as CSV
app.set('trust proxy', ['loopback', 'linklocal', 'uniquelocal']) // specify multiple subnets as an array
```

Quando especificado, os endereços IP ou as subredes são excluídos do processo de determinação de endereço, e o endereço IP não confiável mais próximo do servidor de aplicativos é definido como o endereço IP do cliente. Isto funciona verificando se 'req.socket.remoteAddress' é confiável. Em caso afirmativo, então cada endereço em `X-Forwarded-For` é verificado da direita para a esquerda até o primeiro endereço não confiável.

</td>
    </tr>
    <tr>
      <td>numero</td>
<td markdown="1">
Use o endereço que, no máximo, está fora do número de hops do aplicativo Express. `req.socket.remoteAddress` é o primeiro hop, e o resto é procurado no cabeçalho `X-Forwarded-for` da direita para a esquerda. Um valor de `0` significa que o primeiro endereço não confiável seria `req.socket.remoteAddress`, ou seja, não há um proxy reverso.

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

Habilitar `trust proxy` terá o seguinte impacto:

<ul>
  <li markdown="1">O valor de [req.hostname](/{{ page.lang }}/api.html#req.hostname) é
derivado do valor configurado no cabeçalho
`X-Forwarded-Host`, que pode ser configurado pelo
cliente ou pelo proxy.
  </li>
  <li markdown="1">`X-Forwarded-Proto` pode ser configurado pelo proxy reverso para dizer ao aplicativo se ele é `https` ou `http` ou até mesmo um nome inválido. Este valor é refletido pelo [req.protocol](/{{ page.lang }}/api.html#req.protocol).
  </li>
  <li markdown="1">O [req.ip](/{{ page.lang }}/api.html#req.ip) e [req.ips](/{{ page.lang }}/api.html#req. os valores são preenchidos com base no endereço do socket e no cabeçalho `X-Forwarded-for`, começando no primeiro endereço não confiável.
  </li>
</ul>

A configuração `trust proxy` é implementada usando o pacote [proxy-addr](https://www.npmjs.com/package/proxy-addr). Para obter mais informações, consulte a documentação.
