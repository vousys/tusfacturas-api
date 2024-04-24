---
description: >-
  Mediante éste método, podrás consultar el tope especificado por AFIP, para
  ventas a consumidor final, sin requisito de detallar tipo y número de
  documento del comprador.
---

# Consultar el tope para ventas a consumidor final

## &#x20;

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/topecf`

Mediante éste método, podrás consultar el tope especificado por AFIP, para ventas a consumidor final, sin requisito de detallar tipo y número de documento del comprador.

#### Request Body

| Name      | Type   | Description                |
| --------- | ------ | -------------------------- |
| apikey    | String | Tus credenciales de acceso |
| apitoken  | String | Tus credenciales de acceso |
| usertoken | String | Tus credenciales de acceso |

{% tabs %}
{% tab title="200: OK " %}
```javascript
{
	"error": "N",
	"errores": [],
	"monto": 26228
}
```
{% endtab %}
{% endtabs %}

### Ejemplo de JSON a enviar

```
{
    "apitoken":"xxxx",
    "apikey": xxx,
    "usertoken":"xxxx"
}
```
