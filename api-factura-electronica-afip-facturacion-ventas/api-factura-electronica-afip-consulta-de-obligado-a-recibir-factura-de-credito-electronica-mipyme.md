---
description: >-
  ¿Tu cliente debe recibir Factura de Crédito electrónica MiPyme? ¡Consulta
  fácil y rápido con la API TusFacturas.app!
---

# Comprobantes MiPyme: ¿Debo emitirla?

### ¿Qué son las **facturas MiPyme?**

Las **facturas MiPyME** son un tipo de comprobante electrónico diseñado específicamente para las micro, pequeñas y medianas empresas (MiPyme) en Argentina. Estas facturas cumplen con los requisitos establecidos por la Administración Federal de Ingresos Públicos (AFIP/ARCA) y facilitan la emisión y gestión de comprobantes electrónicos para este sector.

### **¿Para qué sirven las** **facturas MiPyme?**

El objetivo principal es el impulso al financiamiento de las micro, pequeñas y medianas empresas. Su finalidad es desarrollar un mecanismo que mejore las condiciones de financiación de dichas empresas y les permita aumentar su productividad, mediante el cobro anticipado de los créditos y de los documentos por cobrar emitidos a sus clientes y/o deudores, con los que hubieran celebrado una venta de bienes, locación de cosas muebles u obras o prestación de servicios a plazo.

**Características principales:**

* **Obligatoriedad:** La obligatoriedad de emitir facturas MiPyme depende del tipo de operación, el monto y otros factores establecidos por  AFIP/ARCA.
* **Formato electrónico:** Se emiten y reciben de forma electrónica, a través de plataformas habilitadas por la AFIP/ARCA o por proveedores de servicios de facturación electrónica.
* **Información detallada:** Incluyen toda la información necesaria para identificar la operación, los intervinientes y los impuestos aplicables.

**En resumen,** las facturas MiPyme son una herramienta fundamental para las pequeñas y medianas empresas en Argentina, ya que les permiten cumplir con las obligaciones fiscales de manera más eficiente y sencilla.



{% hint style="info" %}
IMPORTANTE: Para poder realizar ésta consulta, deberás tener agregado en tu cuenta AFIP, el servicio de "**Webservice Registro de Facturas de Crédito Electrónica MiPyMEs "** . Te indicamos cómo hacerlo en el [instructivo de integración con AFIP : Paso 6](https://youtu.be/_YSRksd0_A0)
{% endhint %}



### :rocket: ¿Cómo consultar si debes emitir una MiPyme?

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

Ejemplo:

{% content-ref url="../web-services-afip-api-arca/debo-emitir-una-mipyme.md" %}
[debo-emitir-una-mipyme.md](../web-services-afip-api-arca/debo-emitir-una-mipyme.md)
{% endcontent-ref %}

#### Parámetros

| Name      | Type   | Description                                                                    |
| --------- | ------ | ------------------------------------------------------------------------------ |
| fecha     | string | La fechad de emisión del comprobante en cuestión. Formato esperado: dd/mm/aaaa |
| cuit      | number | El CUIT de tu cliente. Campo numérico de 11 digitos                            |
| apikey    | number | Tus credenciales de acceso                                                     |
| usertoken | string | Tus credenciales de acceso                                                     |
| apitoken  | string | <p>Tus credenciales de acceso</p><p>\</p>                                      |

#### Ejemplo del JSON de respuesta:

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

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
