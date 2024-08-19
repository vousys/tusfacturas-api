---
description: >-
  Integra la API para AFIP de TusFacturasAPP a tu sistema y solicita un nuevo
  certificado de enlace con AFIP para tu punto de venta.
---

# Solicitar certificado de enlace con AFIP

Mediante ésta herramienta podras solicitar un certificado de enlace con AFIP y su instructivo. El certificado se generará para el CUIT desde el cual estas haciendo la solicitud y lo recibiras en la casilla de correo del usuario administrador de la cuenta.

## Solicitar certificado

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`puntos_venta/certificado`</mark>

💡 El uso de éste método  contabiliza como un request en tu suscripción

#### Request Body

| Name      | Type   | Description                 |
| --------- | ------ | --------------------------- |
| apikey    | string | Tus credenciales de acceso  |
| apitoken  | string | Tus credenciales de acceso  |
| usertoken | string | Tus credenciales de acceso. |

{% tabs %}
{% tab title="200 " %}
```
```
{% endtab %}
{% endtabs %}

### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```
{
   "usertoken":"xxxx",
    "apitoken":"xxxx",
    "apikey":"xx" 
}
```
{% endcode %}

