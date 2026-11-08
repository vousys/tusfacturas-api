---
description: >-
  La API de TusFacturasAPP recibe un JSON por POST y devuelve el resultado de
  ARCA. Cualquier lenguaje que haga pedidos HTTPS sirve.
---

# Ejemplos de código y SDK para facturar en ARCA: cURL, PHP, Python, Node.js y Ruby

### 1. Prepara el JSON del comprobante

Copiá el ejemplo del comprobante que necesitas y guardalo como `factura.json`:

* [Factura A](../web-services-afip-api-arca/api-factura-electronica-afip-factura-a.md)
* [Factura B](../web-services-afip-api-arca/api-factura-electronica-afip-factura-b.md)
* [Factura C](../web-services-afip-api-arca/api-factura-electronica-afip-factura-c.md)
* [Todos los comprobantes](../web-services-afip-api-arca/)

Completa tus credenciales (`apikey`, `apitoken`, `usertoken`; cómo obtenerlas) y usa la fecha del día en formato `dd/mm/aaaa`.

### 2. Envialo desde tu lenguaje

Endpoint: `POST https://www.tusfacturas.app/app/api/v2/facturacion/nuevo`

{% tabs %}
{% tab title="cURL" %}
```bash
curl -X POST https://www.tusfacturas.app/app/api/v2/facturacion/nuevo \
  -H "Content-Type: application/json" \
  --data @factura.json
```
{% endtab %}

{% tab title="PHP" %}
```php
<?php
$ch = curl_init('https://www.tusfacturas.app/app/api/v2/facturacion/nuevo');
curl_setopt_array($ch, [
    CURLOPT_POST           => true,
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_HTTPHEADER     => ['Content-Type: application/json'],
    CURLOPT_POSTFIELDS     => file_get_contents('factura.json'),
    CURLOPT_TIMEOUT        => 60,
]);
$respuesta = curl_exec($ch);
if ($respuesta === false) {
    die('Error de conexión: ' . curl_error($ch));
}
curl_close($ch);
print_r(json_decode($respuesta, true));
```
{% endtab %}

{% tab title="Python" %}
```python
import json
import requests

with open("factura.json", encoding="utf-8") as f:
    comprobante = json.load(f)

r = requests.post(
    "https://www.tusfacturas.app/app/api/v2/facturacion/nuevo",
    json=comprobante,
    timeout=60,
)
r.raise_for_status()
print(r.json())
```
{% endtab %}

{% tab title="Node.js" %}
```javascript
// Node.js 18 o superior (fetch nativo)
import { readFile } from "node:fs/promises";

const body = await readFile("factura.json", "utf8");

const res = await fetch("https://www.tusfacturas.app/app/api/v2/facturacion/nuevo", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body,
});

console.log(await res.json());
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
require "net/http"
require "json"

uri = URI("https://www.tusfacturas.app/app/api/v2/facturacion/nuevo")
res = Net::HTTP.post(uri, File.read("factura.json"), "Content-Type" => "application/json")
puts JSON.parse(res.body)
```
{% endtab %}
{% endtabs %}

El mismo código sirve para cualquier otro endpoint de la API: cambia la URL y el contenido de `factura.json`.

### 3. Revisá la respuesta

La respuesta indica si ARCA aprobó el comprobante y, en ese caso, trae el CAE, su vencimiento, el número asignado y el link al PDF. Los campos están en la Referencia API y los rechazos más frecuentes en Errores comunes de ARCA.

Si emitís muchos comprobantes, usá el modo asincrónico: ARCA bloquea temporalmente a quien envía pedidos sincrónicos muy seguidos.

### SDK para PHP

El SDK para PHP está en GitHub y se usa desde 2015 en integraciones homologadas por AFIP/ARCA.

{% embed url="https://github.com/vousys/tusfacturas" %}

{% embed url="https://github.com/vousys/tusfacturas.app" %}

### Soporte

Dudas sobre la integración directo con humanos en: api@tusfacturas.app o en [tusfacturas.app](https://www.tusfacturas.app).
