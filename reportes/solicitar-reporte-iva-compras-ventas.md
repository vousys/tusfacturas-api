---
description: >-
  Solicita fácilmente reportes de IVA compras-ventas. Adaptados a tus
  necesidades. API AFIP
---

# Solicitar reporte IVA compras-ventas

Mediante éste método podrás solicitar el envío del reporte IVA compras-ventas a una casilla de e-mail determinada. Se permite 1 casilla de e-mail por solicitud.

### Endpoint

{% hint style="success" %}
<mark style="color:green;">`POST`</mark>    `https://www.tusfacturas.app/app/api/v2/micuenta/`<mark style="color:purple;">**`iva_compras_ventas`**</mark>
{% endhint %}

{% hint style="info" %}
🪙 **Consumo de créditos:** `1 request =  1 llamada`\
Los requests se cuentan individualmente por cada método utilizado. [¿Cómo se calculan?](https://ayuda.tusfacturas.app/es/articles/11679150-api-que-contabiliza-como-un-request-en-tusfacturasapp)
{% endhint %}



#### Request Body

| Name      | Type   | Description                                          |
| --------- | ------ | ---------------------------------------------------- |
| anio      | number | El año del período que se consulta.                  |
| mes       | number | El mes del período que se consulta.                  |
| email     | string | La dirección de e-mail a donde se enviará el reporte |
| apikey    | string | Tus credenciales de acceso                           |
| apitoken  | string | Tus credenciales de acceso                           |
| usertoken | string | Tus credenciales de acceso                           |

#### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```
{
"usertoken" :  "xxxx",
"apikey"    :  "xxxx",
"apitoken"  :  "xxxx",
"mes": 11,
"anio": 2018,
"email": "tumail@dominio.com"

}
```
{% endcode %}

#### Ejemplo del JSON de respuesta

```
{
"error":"N",
"errores":[]
}
```
