---
description: >-
  Integra la API para AFIP de TusFacturasAPP a tu sistema y solicita un nuevo
  certificado de enlace con AFIP para tu punto de venta.
---

# Solicitar certificado de enlace con AFIP

{% hint style="info" %}
A través de esta herramienta, podrás solicitar tu certificado de enlace con ARCA y acceder al instructivo  paso a paso. El sistema generará el certificado para el CUIT de la sesión activa y lo enviará al correo del usuario administrador.

Importante: Esta función solo está disponible para cuentas en producción (no aplica para el plan API DEV).
{% endhint %}

### ¿Cómo solicitar el certificado de enlace con ARCA?

{% hint style="success" %}
<mark style="color:green;">`POST`</mark>    `https://www.tusfacturas.app/app/api/v2/puntos_venta/`<mark style="color:purple;">**`certificado`**</mark>
{% endhint %}

{% hint style="info" %}
🪙 **Consumo de créditos:** `1 request = 1 llamada`\
Los requests se cuentan individualmente por cada método utilizado. [¿Cómo se calculan?](https://ayuda.tusfacturas.app/es/articles/11679150-api-que-contabiliza-como-un-request-en-tusfacturasapp)
{% endhint %}

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

