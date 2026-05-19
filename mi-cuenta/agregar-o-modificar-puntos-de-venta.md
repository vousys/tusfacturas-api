---
description: >-
  Integra la API para ARCA de TusFacturasAPP a tu sistema y accede a información
  relacionada con tu cuenta, como agregar o  modificar un punto de venta.
---

# Agregar o modificar puntos de venta

## ¿Qué es un punto de venta?

Un punto de venta es cualquier espacio, ya sea físico (una tienda, un quiosco) o virtual (una tienda online), donde se lleva a cabo la venta de productos o servicios. En este lugar se registra la transacción, se emite el comprobante de pago y se realiza el cobro al cliente.

### Administrar tu CUIT + Punto de venta

Desde éste método podras dar de alta nuevos puntos de venta dentro de tu espacio de trabajo o modificar ciertos datos de tu punto de venta actual.



Datos a tener en cuenta:

{% hint style="info" %}
**Si estás modificando puntos de venta (PDV)**

* En el caso de la modificación del punto de venta, deberás realizar la solicitud con las keys del punto de venta que querés modificar.
* Una vez que un punto de venta tiene comprobantes creados, la plataforma bloquea automáticamente la edición del CUIT, la condición ante el IVA y el número de punto de venta.\
  Para modificar los datos bloqueados, primero debes eliminar todos los comprobantes asociados al punto de venta.

**Si estás dando de alta puntos de venta (PDV)**

* El CUIT que configures solo puede existir en un espacio de trabajo en toda la plataforma.&#x20;
* Si das de alta un punto de venta para un CUIT que ya operaba en TusfacturasAPP con factura electrónica ARCA, éste quedará habilitado automáticamente. No necesitaras cargar un nuevo certificado de seguridad en ARCA; el único paso requerido es dar de alta el nuevo punto de venta  desde el portal de ARCA, como se indica en [éste instructivo de ayuda](https://ayuda.tusfacturas.app/es/articles/10374245-afip-instructivo-paso-4)&#x20;


{% endhint %}

### Endpoint

<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/`<mark style="color:purple;">`puntos_venta/administrar`</mark>

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

#### Request Body

<table><thead><tr><th>Name</th><th width="131.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>operacion</td><td>string</td><td><p>Valores esperados: A o M</p><p>A = Alta de nuevo punto de venta</p><p></p><p>M = Modifica el punto de venta, correspondiente a las apikey desde las cuales estoy enviando para hacer el request.</p></td></tr><tr><td>conceptos_tipo</td><td>string</td><td><p>Debe indicar el tipo de conceptos que factura, los cuales pueden ser:</p><p>P = Productos</p><p>PS = Productos y Servicios</p><p>S = Servicios</p></td></tr><tr><td>es_predeterminado</td><td>string</td><td>Indica si el CUIT + Punto de venta es el predeterminado. Valores esperados: S o N</td></tr><tr><td>esta_activo</td><td>string</td><td>Indica si el CUIT + Punto de venta se encuentra activo y disponible para generar comprobantes. Valores esperados: S o N</td></tr><tr><td>es_agente_retencion</td><td>string</td><td>Indica si el punto de venta es agente de retención. Valores esperados: S o N.</td></tr><tr><td>factura</td><td>object</td><td>Un objeto del tipo "factura" según se detalla abajo.</td></tr><tr><td>punto_venta</td><td>number</td><td><p>El número del punto de venta a crear.</p><p>\</p><p>Ej: 4</p></td></tr><tr><td>factura_afip</td><td>string</td><td><p>Indica si va a querer <a href="https://www.tusfacturas.app/como-empezamos-a-hacer-facturas-electronicas.html">emitir factura electrónica AFIP</a>. En el caso que la respuesta sea "S", se enviará ademas, via email (a la casilla del administrador), el instructivo para realizar el enlace con AFIP, junto con el certificado de seguridad requerido por AFIP.</p><p></p><p>Valores esperados: S o N.</p><p></p></td></tr><tr><td>fecha_inicio</td><td>string</td><td>Fecha de inicio de actividades. Formato: dd/mm/aaaa</td></tr><tr><td>iibb</td><td>string</td><td>El nro de ingresos brutos.</td></tr><tr><td>iva_emails</td><td>string</td><td>Las direcciones de email separadas por coma donde quieren recibir mensualmente el iva compras-ventas.</td></tr><tr><td>iva_condicion</td><td>string</td><td>La condición impositiva según tabla de referencia.</td></tr><tr><td>direccion</td><td>string</td><td>El domicilio fiscal. Dirección + número</td></tr><tr><td>cuit</td><td>number</td><td>Tu CUIT. Solo números.</td></tr><tr><td>razon_social</td><td>string</td><td>La razón social</td></tr><tr><td>apitoken</td><td>string</td><td>Tus credenciales actuales de acceso.</td></tr><tr><td>apikey</td><td>string</td><td>Tus credenciales actuales de acceso.</td></tr><tr><td>usertoken</td><td>string</td><td>Tus credenciales actuales de acceso.</td></tr><tr><td>webhook</td><td>string</td><td><p>Campo alfanumérico de hasta 255 caracteres. Formato esperado: https://www.dominio.com/script-nombre.</p><p><a href="../api-factura-electronica-afip-facturacion-ventas/webhooks-notificaciones.md#direccion-del-webhook">Más información</a></p></td></tr><tr><td>reg_transparencia_provincial</td><td>object</td><td>Un objeto del tipo "reg_transparencia_provincial" según se detalla abajo.</td></tr><tr><td>actividad_enviar_arca</td><td>string</td><td><p>Luego de crear o actualizar tu punto de venta recuperamos desde ARCA las actividades asociadas a tu CUIT. Indica si queres enviar de manera automatica a ARCA, en todas las ventas, la actividad que tenes predeterminada.  Éste dato hoy es opcional para el envío a ARCA. Sugerimos consultar con el estudio contable.</p><p>Valores esperados: S o N</p></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

#### Objeto "factura"

| Campo a enviar                   | Descripcion                                                                                                                                                                                                                                                                                                                                                                                                            |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| leyenda\_general\_predeterminada | Una leyenda predeterminada que saldrá impresa en todos los comprobantes que emitas.                                                                                                                                                                                                                                                                                                                                    |
| titulo                           | El titulo que saldrá como encabezado de la factura. En gral se usa la razón social o el nombre de fantasía de la empresa. Máx de caracteres permitidos: 18                                                                                                                                                                                                                                                             |
| subtitulo                        | El subtitulo que saldrá en el encabezado de la factura, bajo el titulo principal. Máx de caracteres permitidos: 18                                                                                                                                                                                                                                                                                                     |
| reply\_to\_email                 | La dirección de email para los reply-to en cada envío de comprobante.                                                                                                                                                                                                                                                                                                                                                  |
| reply\_to                        | El nombre de quien envía los comprobantes.                                                                                                                                                                                                                                                                                                                                                                             |
| mensaje                          | El mensaje predeterminado que saldrá en el envío de cada comprobante.                                                                                                                                                                                                                                                                                                                                                  |
| copias                           | La cantidad de copias que se generan dentro del PDF. Valores esperados: 2= para recibir original y duplicado, 3= para recibir original, duplicado y triplicado                                                                                                                                                                                                                                                         |
| cbu                              | Opcional: El número del CBU. Campo numérico, maximo 30 dígitos.                                                                                                                                                                                                                                                                                                                                                        |
| defensa\_consumidor              | Según la normativa vigente, las facturas emitidas a consumidores finales deben incluir al pie del comprobante los datos de contacto del organismo de Defensa al Consumidor correspondiente a la jurisdicción donde opera el negocio. TusFacturasAPP incluye por defecto los datos de la Provincia de Buenos Aires y CABA, pero podes sobrescribir esa información si operas en otra provincia. Máximo: 170 caracteres. |
| imprimir\_sku                    | Su función es controlar si el **SKU o código de producto** se muestra o no en el PDF generado. Esto resulta especialmente útil en escenarios donde el código interno no es relevante para el consumidor final, o cuando se busca simplificar la presentación visual del comprobante.  Valores esperados:  S  o N                                                                                                       |

### Objeto "reg\_transparencia\_provincial"

En el marco de la Ley N° 27.743 de Medidas Fiscales Paliativas y Relevantes, reglamentada por la Resolución General ARCA N° 5614/2024 (B.O. 13/12/2024), se estableció el Régimen de Transparencia Fiscal al Consumidor. Esta norma obliga a discriminar en las facturas el IVA y demás impuestos nacionales indirectos en operaciones con consumidores finales.

La misma ley invita a las provincias y a CABA a adherirse para que también se detallen en los comprobantes el Impuesto sobre los Ingresos Brutos (IIBB) y las tasas municipales. A medida que cada jurisdicción se adhiere y reglamenta, los contribuyentes inscriptos en IIBB quedan obligados a incluir una leyenda con la alícuota aplicable en las facturas B emitidas a consumidor final.

Más info:  [Adecuación al Régimen de Transparencia Fiscal Provincial: configuración en TusFacturasAPP ](https://ayuda.tusfacturas.app/es/articles/15137188-adecuacion-al-regimen-de-transparencia-fiscal-provincial-configuracion-en-tusfacturasapp)

| Campo a enviar | Descripcion                                                                                                                                     |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| fecha\_inicio  | Una leyenda predeterminada que saldrá impresa en todos los comprobantes que emitas.                                                             |
| texto          | El texto que se imprimirá dentro del bloque de "Regimen de transparencia fiscal", indicando la adecuación de tu provincia. Máx: 100 caracteres. |

### JSON De ejemplo a enviar

{% code title="JSON" %}
```
{
   "usertoken":"xxxx",
    "apitoken":"xxx",
    "apikey":"xxxx",
    "operacion":"A",
    "punto_venta": "00023",
    "direccion":"AV. 68 N75A - 50, PISO 4, Buenos Aires, Argentina",
    "razon_social": "MI CUIT DE PRUEBA",
    "cuit": "11111123213",
    "iva_condicion": "M",
    "iva_emails": "tuemail@tudominio.com",
    "iibb":"12345",
    "fecha_inicio": "12/12/2017",
    "factura_afip": "S",
    "es_agente_retencion": "N",
    "esta_activo": "S",
    "es_predeterminado": "S",
    "conceptos_tipo": "PS",
    "actividad_enviar_arca": "N",
    "webhook": "https://www.dominio.com/script-name",
    "factura" : {
        "leyenda_general_predeterminada": "TEST",
        "titulo" : "PIRULO & CO",
        "subtitulo": "La mejor barberia",
        "reply_to_email": "info@tudominio.com.ar",
        "reply_to": "PIRULO",
        "mensaje": "Le enviamos la factura que se encuentra adjunta",
        "copias": "2",
         "defensa_consumidor": "Defensa al consumidor WhatsApp 2617542335",
    },
    "reg_transparencia_provincial": {
			"fecha_inicio": "01/09/2026",
		  "texto": "ALICUOTA ISIB CABA 3%"
	   }

}
```
{% endcode %}



