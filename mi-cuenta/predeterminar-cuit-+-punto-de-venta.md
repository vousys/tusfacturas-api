---
description: >-
  Integra la API para AFIP de TusFacturasAPP a tu sistema y accede a información
  relacionada con tu cuenta, asi como predeterminar un punto de venta.
---

# Predeterminar CUIT + Punto de venta



## Predeterminar CUIT + Punto de venta

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`puntos_venta/predeterminar`</mark>

💡 El uso de éste método  contabiliza como un request en tu suscripción

#### Request Body

| Name      | Type   | Description                               |
| --------- | ------ | ----------------------------------------- |
| apitoken  | string | Tus credenciales de acceso                |
| apikey    | string | Tus credenciales de acceso                |
| usertoken | string | <p>Tus credenciales de acceso</p><p>\</p> |

{% tabs %}
{% tab title="200 " %}
```
{
	"error": "N",
	"errores": [] 
}
```
{% endtab %}
{% endtabs %}

#### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```
{
   "usertoken":"xxxx",
    "apitoken":"xxxx",
    "apikey":"xxxx" 
}
```
{% endcode %}

##
