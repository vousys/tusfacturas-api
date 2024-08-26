---
description: >-
  Solicita fácilmente reportes de IVA compras-ventas. Adaptados a tus
  necesidades. API AFIP
---

# Solicitar reporte IVA compras-ventas

Mediante éste método, solicitarás el envío del reporte IVA compras-ventas a una casilla de e-mail determinada. Se permite 1 casilla solamente por solicitud.

## Solicitá el IVA Compras - Ventas

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`micuenta/iva_compras_ventas`</mark>

💡 El uso de éste método  contabiliza como un request en tu suscripción

#### Request Body

| Name      | Type   | Description                                          |
| --------- | ------ | ---------------------------------------------------- |
| anio      | number | El año del período que se consulta.                  |
| mes       | number | El mes del período que se consulta.                  |
| email     | string | La dirección de e-mail a donde se enviará el reporte |
| apikey    | string | Tus credenciales de acceso                           |
| apitoken  | string | Tus credenciales de acceso                           |
| usertoken | string | Tus credenciales de acceso                           |

{% tabs %}
{% tab title="200 La respuesta es error = S o error = N" %}
{% code title="JSON" %}
```
{
"error":"N",
"errores":[]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```
{
"usertoken" :  "xxxx",
"apikey"    :  "xxxx",
"apitoken"  :  "xxxx",
"mes": 11,
"anio": 2018,
"email": "tumail@dominio.com"

}
```
{% endcode %}

### Ejemplo del JSON de respuesta

```
{
"error":"N",
"errores":[]
}
```
