---
description: >-
  Consulta fácil y rápido el tope AFIP para ventas a consumidor final. ¡Sin
  necesidad de datos del comprador!
---

# Consultar el tope para ventas a consumidor final



<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">`topecf`</mark>

💡 El uso de éste método  contabiliza como un request en tu suscripción



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
