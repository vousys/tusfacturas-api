---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la lista
  de paises definidos por AFIP
---

# Consulta de Países en AFIP

### Parámetros: Consulta de paises&#x20;

{% hint style="success" %}
<mark style="color:green;">`POST`</mark>    `https://www.tusfacturas.app/app/api/v2/tablas_referencia/`<mark style="color:purple;">**`paises`**</mark>
{% endhint %}

{% hint style="info" %}
🪙 **Consumo de créditos:** `1 request =  1 llamada`\
Los requests se cuentan individualmente por cada método utilizado. [¿Cómo se calculan?](https://ayuda.tusfacturas.app/es/articles/11679150-api-que-contabiliza-como-un-request-en-tusfacturasapp)
{% endhint %}

#### Request Body

| Name      | Type   | Description                 |
| --------- | ------ | --------------------------- |
| apikey    | string | Tus credenciales de acceso  |
| apitoken  | string | Tus credenciales de acceso  |
| usertoken | string | Tus credenciales de acceso. |

### Estructura del JSON a enviar

{% code title="JSON" %}
```
{
	"usertoken": "xxxx",
	"apikey": "xxx",
	"apitoken": "xxxx"
}
```
{% endcode %}
