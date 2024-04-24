---
description: >-
  Consulta desde la API de facturación electrónica de TusFacturas.app, la lista
  de paises definidos por AFIP
---

# Parámetros: Consulta de Países en AFIP

## Consulta de paises&#x20;

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/tablas_referencia/paises`

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
