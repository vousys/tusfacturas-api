---
description: >-
  Consulta desde la API de TusFacturas.app, la información relacionada con tu
  cuenta.
---

# Mi Cuenta - consumo

## Consultá el consumo de tu cuenta

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`micuenta/consumo`</mark>

💡 El uso de éste método  contabiliza como un request en tu suscripción



Éste método te brindara que cantidad de comprobantes podes emitir en el mes en curso, cuantos tenés programados como abono, y cuantos te quedan disponibles.

#### Request Body

| Name      | Type   | Description                |
| --------- | ------ | -------------------------- |
| apikey    | string | Tus credenciales de acceso |
| apitoken  | string | Tus credenciales de acceso |
| usertoken | string | Tus Credenciales de acceso |

{% tabs %}
{% tab title="200 " %}
{% code title="JSON" %}
```
{
"error":"N",
"errores":[],
"abonos_pendientes":21,
"comprobantes_generados":12,
"comprobantes_cupo":100,
"comprobantes_disponibles": 79
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```
{
   "usertoken":"xxxxx",
    "apitoken":"xxxx",
    "apikey":"xxxx" 
}
```
{% endcode %}

### Ejemplo del JSON de respuesta

```
{
"error":"N",
"errores":[],
"abonos_pendientes":21,
"comprobantes_generados":12,
"comprobantes_cupo":100,
"comprobantes_disponibles": 79
}
```

##
