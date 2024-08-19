---
description: >-
  ¿Tu cliente debe recibir Factura de Crédito electrónica MiPyme? ¡Consulta
  fácil y rápido con la API TusFacturas.app!
---

# Consulta para verificar si estoy obligado a recibir o emitir Factura de Crédito electrónica MiPyme

### ¿Qué son las **facturas MiPyME?**

Las **facturas MiPyME** son un tipo de comprobante electrónico diseñado específicamente para las micro, pequeñas y medianas empresas (MiPyMEs) en Argentina. Estas facturas cumplen con los requisitos establecidos por la Administración Federal de Ingresos Públicos (AFIP) y facilitan la emisión y gestión de comprobantes electrónicos para este sector.

### **¿Para qué sirven las** **facturas MiPyME?**

El objetivo principal es el impulso al financiamiento de las micro, pequeñas y medianas empresas. Su finalidad es desarrollar un mecanismo que mejore las condiciones de financiación de dichas empresas y les permita aumentar su productividad, mediante el cobro anticipado de los créditos y de los documentos por cobrar emitidos a sus clientes y/o deudores, con los que hubieran celebrado una venta de bienes, locación de cosas muebles u obras o prestación de servicios a plazo.

**Características principales:**

* **Obligatoriedad:** La obligatoriedad de emitir facturas MiPyME depende del tipo de operación, el monto y otros factores establecidos por la AFIP.
* **Formato electrónico:** Se emiten y reciben de forma electrónica, a través de plataformas habilitadas por la AFIP o por proveedores de servicios de facturación electrónica.
* **Información detallada:** Incluyen toda la información necesaria para identificar la operación, los intervinientes y los impuestos aplicables.

**En resumen,** las facturas MiPyME son una herramienta fundamental para las pequeñas y medianas empresas en Argentina, ya que les permiten cumplir con las obligaciones fiscales de manera más eficiente y sencilla.



{% hint style="info" %}
<mark style="background-color:purple;">El uso de éste método contabiliza como 1 request en tu suscripción. El límite de request que dispones para realizar las consultas, es el mismo limite que tenés habilitado en tu plan para la emisión de comprobantes . Ej: si tu plan incluye 1000 comprobantes, podrás realizar 1000 request a éste método en el período en curso.</mark>

IMPORTANTE: Para poder realizar ésta consulta, deberás tener agregado en tu cuenta AFIP, el servicio de "**Webservice Registro de Facturas de Crédito Electrónica MiPyMEs "** . Te indicamos cómo hacerlo en el [instructivo de integración con AFIP : Paso 6](https://youtu.be/\_YSRksd0\_A0)
{% endhint %}

## Consulta de obligado a recibir MiPyme

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/requiere_fec`

Éste método te devolverá si tu cliente se encuentra obligado a recibir facturas de tipo MiPyme y a partir de que monto se encuentra obligado.

#### Request Body

| Name      | Type   | Description                                                                    |
| --------- | ------ | ------------------------------------------------------------------------------ |
| fecha     | string | La fechad de emisión del comprobante en cuestión. Formato esperado: dd/mm/aaaa |
| cuit      | number | El CUIT de tu cliente. Campo numérico de 11 digitos                            |
| apikey    | number | Tus credenciales de acceso                                                     |
| usertoken | string | Tus credenciales de acceso                                                     |
| apitoken  | string | <p>Tus credenciales de acceso</p><p>\</p>                                      |

{% tabs %}
{% tab title="200 " %}
{% code title="JSON" %}
```
En caso de no encontrar errores obtendrás una respuesta 
como la siguiente:

{
	"error": "N",
	"errores": [],
	"rta": "",
	"esta_obligado": "S",
	"importe_desde": 100000
}

En caso de detectar errores, obtendrás una respuesta 
como la siguiente:

{
	"error": "S",
	"errores": ["El CUIT enviado INF es invalido."],
	"rta": "", 
}





```
{% endcode %}
{% endtab %}
{% endtabs %}

### Ejemplo del JSON a enviar:

```
{
	"apitoken": "xxxx",
	"apikey": xxxx,
	"usertoken": "xxxx",
	"cuit": 12345678901,
	"fecha": "08/12/2019"
}
```

### Ejemplo del JSON de respuesta:

```
En caso de éxito:

{
	"error": "N",
	"errores": [],
	"rta": "",
	"esta_obligado": "S",
	"importe_desde": 100000
}

En caso de detectar errores:

{
	"error": "S",
	"errores": ["El CUIT enviado INF es invalido."],
	"rta": "", 
}
```
