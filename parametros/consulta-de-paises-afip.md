---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la lista
  de paises definidos por AFIP
---

# Consulta de Países en AFIP

### Parámetros: Consulta de paises&#x20;

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`tablas_referencia/paises`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

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
