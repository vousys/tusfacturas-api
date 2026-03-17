---
description: >-
  Integra la API para AFIP de TusFacturasAPP a tu sistema y solicita un nuevo
  certificado de enlace con AFIP para tu punto de venta.
---

# Solicitar certificado de enlace con AFIP

{% hint style="info" %}
A través de esta herramienta, podrás solicitar tu certificado de enlace con ARCA y acceder al instructivo paso a paso. El sistema generará el certificado para el CUIT de la sesión activa y lo enviará al correo del usuario administrador.

Importante: Esta función solo está disponible para cuentas en producción (no aplica para el plan API DEV).
{% endhint %}

### ¿Cómo solicitar certificado de enlace?

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`puntos_venta/certificado`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

#### Request Body

| Name      | Type   | Description                 |
| --------- | ------ | --------------------------- |
| apikey    | string | Tus credenciales de acceso  |
| apitoken  | string | Tus credenciales de acceso  |
| usertoken | string | Tus credenciales de acceso. |

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

