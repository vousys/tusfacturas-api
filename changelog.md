---
description: >-
  A continuación podrás conocer los cambios realizados sobre nuestra plataforma
  API.
---

# Changelog

## 30 de agosto de 2023

Facturación: A partir del 01/01/2024 se dejará de enviar como respuesta en el JSON, el campo "afip\_codigo\_barras"

## 29 de agosto de 2023

Facturación > Vencimiento del comprobante. A partir del 01/10/2023 el campo "vencimiento" del comprobante será un dato obligatorio.

## 21 de abril de 2023

Facturacion > Clientes: Se amplia hasta 15 casillas de e-mail.

## 26 de marzo de 2023

Facturación: Se agrega el bloque "tributos" dentro de la estructuctura de "comprobante" y el atributo "rg5329" al bloque de productos y clientes. Se eliminan los siguientes atributos de un comprobante:  percepciones\_iibb, percepciones\_iibb\_base, percepciones\_iibb\_alicuota, percepciones\_iibb2, percepciones\_iibb2\_base, percepciones\_iibb2\_alicuota, percepciones\_iva, percepciones\_iva\_base, percepciones\_iva\_alicuota.

Se habilita el envió de hasta un máximo de 6 percepciones de IVA y/o Ingresos brutos.

Se adecua la plataforma para la entrada en vigencia de la [RG5329.](faqs-or-rg5329.md)



## 22 de junio de 2022

Facturación: Se agrega en el response del bloque de "comprobante", la estructura de información para los micrositios, para los métodos de nuevas ventas y consultas.

## 03 de junio de 2022

Se agrega el tipo de documento: CDI y CUIL en las [tablas de referencia.](parametros/)

## 24 de mayo de 2022

Se modificó el manejo de errores para los comprobantes asincrónicos (en lote o individual), ya que se empieza a notificar vía webhook, si corresponde.

## 25 de marzo de 2022

Se agrega la documentación de "[nuevo recibo de cobro](recibos-de-cobro-y-ordenes-de-pago/api-factura-electronica-afip-or-ingresar-pago-1.md)"  y "[nueva orden de pago](recibos-de-cobro-y-ordenes-de-pago/api-factura-electronica-afip-or-ingresar-pago-2.md)"

## 23 de marzo de 2022

Se agrega el campo "webhook" a la documentación de "[Mi cuenta - administrar puntos de venta (PDV)](mi-cuenta/agregar-o-modificar-puntos-de-venta-pdv.md)

Se agrega la documentación de "[Eliminar comprobante encolado](api-factura-electronica-afip-facturacion-ventas/eliminar-comprobantes-encolados.md)".

Se agrega la documentación de "[Cambiar fecha a comprobantes encolado](api-factura-electronica-afip-facturacion-ventas/cambiar-fecha-a-comprobante-encolado.md)"

Se agrega la documentación de "[Reenviar a procesar, comprobante encolado con error](api-factura-electronica-afip-facturacion-ventas/reenviar-a-procesar-comprobante-encolado-con-error.md)

## 22 de marzo de 2022

Se incluye la documentación de ["Webhooks (notificaciones)](webhooks-notificaciones.md)

## 21 de Marzo de 2022

Se incluye la documentación de la ["Facturación por lotes asincrónica (encolada)](api-factura-electronica-afip-facturacion-ventas/facturacion-asincronica-por-lotes-encolada.md)

## 17 de marzo de 2022

Se incluye en la documentación de la [consulta avanzada de comprobantes](api-factura-electronica-afip-facturacion-ventas/consulta-avanzada-de-comprobantes-enviados.md), el campo de total de registros resultantes de esa búsqueda, la paginación y su límite por página.

Se incluye también en la documentación de [facturación](api-factura-electronica-afip-facturacion-ventas/) > [comprobantes asociados](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-ventas#envio-de-comprobantes-asociados-detallados), una nueva acción que se ejecutará a partir del 26/03/2022 con las notas de crédito: la auto-acreditación en caja de la NC.

## 16 de marzo de 2022

Se modifica la documentación de [facturación](api-factura-electronica-afip-facturacion-ventas/), y se agrega el bloque de "**tags**", como opcional para el envío de nuevos comprobantes.

## 11 de marzo de 2022

Se modifica la documentación de la[ consulta de comprobantes individual](api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-consulta-de-comprobantes.md) y [avanzada](api-factura-electronica-afip-facturacion-ventas/consulta-avanzada-de-comprobantes-enviados.md). Se agrega el método de [consulta por "external\_reference"](api-factura-electronica-afip-facturacion-ventas/consulta-avanzada-de-comprobantes-enviados.md#como-realizar-una-consulta-avanzada-por-external-reference) , a partir del 01/04/2022 y se agrega la paginación a la consulta avanzada, a partir del 01/05/2022.

## 07 de febrero de 2022

Nuevo comprobante de venta: Se agrega el campo "external\_reference" dentro del bloque "comprobante", para que puedas referenciar cada comprobante en tu sistema, ya sea si lo envías por lotes o individuales.

## 12 de enero de 2022

Se agrega el método de reenvío de comprobantes. Conocé más desde aquí: [https://developers.tusfacturas.app/api-factura-electronica-afip-or-reenviar-comprobante](https://developers.tusfacturas.app/api-factura-electronica-afip-or-reenviar-comprobante)

## 07 de enero de 2022

Se agrega el método de consulta del monto tope, para la emisión de ventas a consumidor final, sin especificar su tipo y número de documento. Conocé más desde aquí: [https://developers.tusfacturas.app/api-factura-electronica-afip-or-consulta-de-tope-para-ventas-a-consumidor-final](https://developers.tusfacturas.app/api-factura-electronica-afip-or-consulta-de-tope-para-ventas-a-consumidor-final)

## 28 de diciembre de 2021

Se agrega un método para informar los pagos asociados a un comprobante ya emitido. Conocé más desde aquí: [https://developers.tusfacturas.app/api-factura-electronica-afip-ingresar-pago](https://developers.tusfacturas.app/api-factura-electronica-afip-ingresar-pago)

## 16 de diciembre de 2021

Se agrega la condición frente al IVA: "IVNA", correspondiente a "IVA No Alcanzado"

## 29 de octubre de 2021

Se agrega el bloque de "actividad" a la información devuelta por el método de consulta de CUIT.

## 05 de julio de 2021

Se amplía a 130 conceptos por comprobante.

## 07 de junio de 2021

Se agregan 2 nuevos métodos de consulta de comprobantes: por [fecha](https://developers.tusfacturas.app/api-factura-electronica-afip-consulta-de-comprobantes#consulta-de-comprobantes-por-fecha) y por [rango numérico](https://developers.tusfacturas.app/api-factura-electronica-afip-consulta-de-comprobantes#consulta-de-comprobantes-por-rango-de-numeros).

## 01 de junio de 2021

A partir del 01-07-2021, todo comprobante que se emita desde un responsable inscripto a un monotributista, deberá ser de un comprobante de tipo A, en lugar de comprobante B y deberá llevar la siguiente leyenda: "_El crédito fiscal discriminado en el presente comprobante, sólo podrá ser computado a efectos del Régimen de Sostenimiento e Inclusión Fiscal para Pequeños Contribuyentes de la Ley Nº 27.618"._ Éste dato **NO** **debe ser enviado** en el campo "leyenda\_gral", ya que saldrá automáticamente impreso en los PDF que se generen desde nuestra plataforma.

## 31 de marzo de 2021

#### Envío de pagos asociados al comprobante

Opcionalmente se puede informar el pago asociado al comprobante, de modo que la cuenta corriente de tu cliente, quede completa.

Consultar la documentación [desde aquí](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-nuevo-comprobante#estructura-de-pagos-opcional)

## 22 de marzo de 2021

**Nueva venta. Facturas de crédito electronica MiPyme**

A partir del 01/04/2021 se pondrá en funcionamiento un campo obligatorio en éstos tipos de comprobante donde se debe indicar si el comprobante se transfiere al sistema de circulación abierta o al agente de depósito colectivo. Deberán enviar un nuevo dato en el bloque de "opcionales":

SCA = "TRANSFERENCIA AL SISTEMA DE CIRCULACION ABIERTA"

ADC = "AGENTE DE DEPOSITO COLECTIVO"

[Ver documentación](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-nuevo-comprobante/api-factura-electronica-afip-factura-de-credito-electronica-mipyme-fce)

**Notas de débito y crédito por período - Mod. RG 4.540/2019**

A partir del 01/04/2021 entrará también en vigencia una nueva manera de emitir notas de crédito y débito, donde en lugar de indicar uno o mas comprobantes asociados, se podrá indicar un periodo desde/hasta, el cual contempla los comprobantes emitidos dentro del período en cuestión. [Ver documentación](api-factura-electronica-afip-facturacion-ventas/#estructura-de-comprobantes-asociados-detallados)

***

## 16 de noviembre de 2020

Nueva venta. Implementamos el QR que lanzó AFIP ( [https://www.afip.gob.ar/fe/qr/especificaciones.asp](https://www.afip.gob.ar/fe/qr/especificaciones.asp) ) en reemplazo del código de barras. Si bien, por el momento la url te lleva a la misma página de la documentación del QR, estimamos que en breve estarán implementando una especie de constatación de comprobantes. El texto que debe incluir ese QR, te será devuelvo dentro de la variable "afip\_qr", para que puedas generar vos el QR de tu lado en caso que lo desees.

## 16 de Julio de 2020

Nueva venta > bloque clientes. Se agrega el campo opcional: código para que puedan enviar el código interno del cliente.

## 07 de Mayo de 2020

Cotizaciones: Se agrega la posibilidad de enviar la fecha para obtener la cotización AFIP de alguna moneda, con hasta 2 meses para atras.

## 08 de diciembre de 2019

Se agrega el método de consulta para las facturas de crédito electrónica MiPyme. Mediante éste método podrás consultar antes de enviar a facturar, si tu cliente se encuentra obligado a recibir una factura de tipo MiPyme y en caso afirmativo, a partir de que monto.

## 03 de diciembre de 2019

Se agrega la consulta de cotización multi-moneda .

## 06 de noviembre de 2019

Se agrega una variable al response de la emisión de comprobantes, llamado "requiere\_fec" cuya respuesta puede ser "SI" o "NO", para indicar que el comprobante a emitir debe ser generado como Factura Electrónica de Crédito MiPyme (FEC) y no como un comprobante común de tipo A, B o C.

## 16 de octubre de 2019

Se agrega el campo ["fecha\_pago" ](api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-factura-electronica-afip-exportacion.md)para las facturas de exportación.

## 14 de octubre de 2019

Se agrega el campo "cbu" al [bloque de la factura](mi-cuenta/mi-cuenta.md#objeto-factura), en Mi Cuenta -> Mis Puntos de venta / administrar.

## 22 de septiembre de 2019

Cambios para la emisión de un nuevo comprobante:

**Nueva alícuota: IVA No gravado**. Ahora podes enviar a facturar conceptos con IVA no gravado. Para eso agregamos una nueva alícuota (-2) para que puedas enviarla dentro de cada concepto.

En conjunto con este cambio, se dejó sin uso el campo de "nogravados" que se enviaba en el bloque de los totales del comprobante. A partir de hoy, serán rechazados todos los comprobantes que indiquen un valor mayor a cero en el campo: nogravados"

## 14 de septiembre de 2019

Cambios para la emisión de un nuevo comprobante:

* **Cambiamos la url a donde deberás enviar los request.** Ahora deberan ser enviados a https://www.tusfacturas.app
* **Cambio de códigos:** En el bloque de "clientes", cambian los códigos a enviar en concepto de "condicion\_pago". [Consultar la tabla de referencia](parametros/tablas-de-referencia.md#condiciones-de-venta)
* **Nueva condición de pago:** Se agrega la condición de pago "otras", la cual le permite enviar cualquier texto para que salga impreso en el pdf. Ésta información deberá ser enviada, dentro del campo "condicion\_pago\_otra" en el bloque de "clientes". [Consultar ejemplo aquí](api-factura-electronica-afip-facturacion-ventas/#estructura-de-cliente). Éste campo es util cuando se lo junta con el campo de vencimiento (donde se indica la fecha de vencimiento de manera manual)
* **Nuevas monedas de facturación:** Ahora podes emitir comprobantes en otras monedas extranjeras. [Consultá las monedas disponibles aquí ](parametros/tablas-de-referencia.md#monedas). Si necesitas alguna que no esté incluida, solicitála via email.

## 05 de Agosto de 2019

**Nuevo comprobante:** Se agrega el porcentaje de impuestos internos dentro del bloque de cada "producto

## 10 de Julio de 2019

**1) Nuevos campos para Percepciones e Impuestos internos** Se agregaron campos dentro del bloque "comprobantes" para el envio de las percepciones e impuestos internos\
percepciones\_iibb\_base,\
percepciones\_iibb\_alicuota,\
percepciones\_iva\_base,\
percepciones\_iva\_alicuota,\
impuestos\_internos\_base,\
impuestos\_internos\_alicuota,\
**D**ocumentacion: [https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante](https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante)\
\
**2) RG Especiales**

Se creo un nuevo bloque de información para enviar los datos asociados a RG Especiales.AFIP requiere que segun las diferentes RG que tiene publicadas, se envien datos adicionales.Estos datos, estan catalogados en la siguiente tabla, según el regimen al que correspondan:[https://tusfacturas.gitbook.io/api-factura-electronica-afip/tablas-de-referencia#datos-opcionales-para-rg-especiales](https://tusfacturas.gitbook.io/api-factura-electronica-afip/tablas-de-referencia#datos-opcionales-para-rg-especiales)\
Ej: Quienes facturan alquileres casa familia, aplicados a la RG 4004-E deben enviar datos adicionales.Lo mismo sucede, con los nuevos comprobantes de tipo "Factura Electronica de Creédito MiPyme (FCE)"Consultá la documentacion: [https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante#estructura-de-rg-especiales](https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante#estructura-de-rg-especiales)\
\
**3) Comprobantes asociados**

Se agrego el campo "comprobante\_fecha" dentro de los datos a enviar. Éste campo es obligatorio para los nuevos comprobantes de tipo "Factura Electronica de Creédito MiPyme (FCE)"Consultá la documentacion: [https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante#estructura-de-comprobantes-asociados](https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante#estructura-de-comprobantes-asociados)\
\
**4) Factura Electrónica de Creédito MiPyme (FCE)**

Se agrego la posibilidad de emitir éste tipo de comprobantes, en todas sus modalidades (Facturas, Notas de debito y Notas de Credito).Es importante que consulten con su contador/a las particularidades de éstos comprobantes, ya que requieren un tratamiento posterior especial, que no aplica a nuestra plataforma.En la documentación [https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante/factura-de-credito-electronica-mipyme-fce](https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante/factura-de-credito-electronica-mipyme-fce) podrán encontrar ejemplos tanto de una factura A como de una NC

## 28 de Junio de 2019

Ajustes mandatorios requeridos por AFIP para las NC / ND. Éste cambio aplicará a la API y la WebApp www.tusfacturas.app\
Para ésto se requiere que envien dentro del bloque "comprobante", un array con los diferentes comprobantes asociados, según estructura:

`{"tipo_comprobante" : "FACTURA A", "punto_venta" : "145","numero" : 12313,"cuit": 111111111}`\
\`\`Ya se encuentra actualizada la documentación: [https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante/factura-a-nota-de-debito-a-nota-de-credito-a](https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante/factura-a-nota-de-debito-a-nota-de-credito-a)\
\\
