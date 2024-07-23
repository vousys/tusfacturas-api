---
description: >-
  Mediante éste método podrás obtener en la casilla de e-mail de los
  administradores de tu cuenta, un nuevo certificado de seguridad
---

# Solicitar certificado de enlace con AFIP

El certificado se generará para el CUIT desde el cual estas haciendo la solicitud.

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

