---
description: >-
  Integra la API para AFIP de TusFacturasAPP a tu sistema y accede a información
  relacionada con tu cuenta, asi como predeterminar un punto de venta.
---

# Predeterminar punto de venta

### ¿Cómo predeterminar un punto de venta para usarlo desde la plataforma web?

{% hint style="success" %}
<mark style="color:green;">`POST`</mark>    `https://www.tusfacturas.app/app/api/v2/puntos_venta/`<mark style="color:purple;">**`predeterminar`**</mark>
{% endhint %}

{% hint style="info" %}
🪙 **Consumo de créditos:** `1 request = 1 llamada`\
Los requests se cuentan individualmente por cada método utilizado. [¿Cómo se calculan?](https://ayuda.tusfacturas.app/es/articles/11679150-api-que-contabiliza-como-un-request-en-tusfacturasapp)
{% endhint %}

#### Request Body

| Name      | Type   | Description                              |
| --------- | ------ | ---------------------------------------- |
| apitoken  | string | Tus credenciales de acceso               |
| apikey    | string | Tus credenciales de acceso               |
| usertoken | string | <p>Tus credenciales de acceso</p><p></p> |

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

