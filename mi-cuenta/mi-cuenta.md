---
description: >-
  Integra la API para AFIP de TusFacturasAPP a tu sistema y accede a información
  relacionada con tu cuenta, como consultar tu consumo actual.
---

# Mi Cuenta - consumo

### **💡 ¿Cómo funciona el consumo de cupos en la API?**

Es fundamental entender que los límites de tu plan no funcionan como un pozo único, sino que se distribuyen de forma independiente según el tipo de operación. Consulta nuestro centro de ayuda para más detalles sobre [qué contabiliza como un request](https://ayuda.tusfacturas.app/es/articles/11679150-api-que-contabiliza-como-un-request-en-tusfacturasapp).

### Consulta el consumo de tu cuenta

Éste método te brindara que cantidad de comprobantes que tenes incluidos en tu suscripción actual,  cuantos tenes programados como abono, y cuantos te quedan disponibles para consumir..

{% hint style="success" %}
<mark style="color:green;">`POST`</mark>    `https://www.tusfacturas.app/app/api/v2/micuenta/`<mark style="color:purple;">**`consumo`**</mark>
{% endhint %}

{% hint style="info" %}
🪙 **Consumo de créditos:** `1 request =  1 llamada`\
Los requests se cuentan individualmente por cada método utilizado. [¿Cómo se calculan?](https://ayuda.tusfacturas.app/es/articles/11679150-api-que-contabiliza-como-un-request-en-tusfacturasapp)
{% endhint %}

#### Request Body

| Name      | Type   | Description                |
| --------- | ------ | -------------------------- |
| apikey    | string | Tus credenciales de acceso |
| apitoken  | string | Tus credenciales de acceso |
| usertoken | string | Tus Credenciales de acceso |

### Ejemplo del JSON a enviar:

{% code title="JSON" %}
```
{
   "usertoken":"xxxxx",
    "apitoken":"xxxx",
    "apikey":"xxxx" 
}
```
{% endcode %}

### Ejemplo del JSON de respuesta

```
{
"error":"N",
"errores":[],
"abonos_pendientes":21,
"comprobantes_generados":12,
"comprobantes_cupo":100,
"comprobantes_disponibles": 79
}
```

