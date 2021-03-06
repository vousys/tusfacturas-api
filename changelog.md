# Changelog

## 16 de noviembre de 2020

Nueva venta. Implementamos el QR que lanzó AFIP \( [https://www.afip.gob.ar/fe/qr/especificaciones.asp](https://www.afip.gob.ar/fe/qr/especificaciones.asp) \) en reemplazo del código de barras. Si bien, por el momento la url te lleva a la misma página de la documentación del QR, estimamos que en breve estarán implementando una especie de constatación de comprobantes. El texto que debe incluir ese QR, te será devuelvo dentro de la variable "afip\_qr", para que puedas generar vos el QR de tu lado en caso que lo desees.

## 16 de Julio de 2020

Nueva venta &gt; bloque clientes. Se agrega el campo opcional: codigo para que puedan enviar el codigo interno del cliente.

## 07 de Mayo de 2020

Cotizaciones: Se agrega la posibilidad de enviar la fecha para obtener la cotización AFIP de alguna moneda, con hasta 2 meses para atras.

## 08 de diciembre de 2019

Se agrega el método de consulta para las facturas de crédito electrónica MiPyme. Mediante éste método podrás consultar antes de enviar a facturar, si tu cliente se encuentra obligado a recibir una factura de tipo MiPyme y en caso afirmativo, a partir de que monto.

## 03 de diciembre de 2019

Se agrega la consulta de cotización multi-moneda .

## 06 de noviembre de 2019

Se agrega una variable al response de la emisión de comprobantes, llamado "requiere\_fec" cuya respuesta puede ser "SI" o "NO", para indicar que el comprobante a emitir debe ser generado como Factura Electrónica de Crédito MiPyme \(FEC\) y no como un comprobante común de tipo A, B o C.

## 16 de octubre de 2019

Se agrega el campo ["fecha\_pago" ](api-factura-electronica-afip-facturacion-nuevo-comprobante/api-factura-electronica-afip-factura-electronica-afip-exportacion.md)para las facturas de exportación.

## 14 de octubre de 2019

Se agrega el campo "cbu" al [bloque de la factura](mi-cuenta.md#objeto-factura), en Mi Cuenta -&gt; Mis Puntos de venta / administrar.

## 22 de septiembre de 2019

Cambios para la emisión de un nuevo comprobante:

**Nueva alícuota: IVA No gravado**. Ahora podes enviar a facturar conceptos con IVA no gravado. Para eso agregamos una nueva alícuota \(-2\) para que puedas enviarla dentro de cada concepto.

En conjunto con este cambio, se dejó sin uso el campo de "nogravados" que se enviaba en el bloque de los totales del comprobante. A partir de hoy, serán rechazados todos los comprobantes que indiquen un valor mayor a cero en el campo: nogravados"

## 14 de septiembre de 2019

Cambios para la emisión de un nuevo comprobante:

* **Cambiamos la url a donde deberás enviar los request.** Ahora deberan ser enviados a https://www.tusfacturas.app
* **Cambio de códigos:** En el bloque de "clientes", cambian los códigos a enviar en concepto de "condicion\_pago". [Consultar la tabla de referencia](tablas-de-referencia.md#condiciones-de-venta) 
* **Nueva condición de pago:** Se agrega la condición de pago "otras", la cual le permite enviar cualquier texto para que salga impreso en el pdf. Ésta información deberá ser enviada, dentro del campo "condicion\_pago\_otra" en el bloque de "clientes". [Consultar ejemplo aquí](api-factura-electronica-afip-facturacion-nuevo-comprobante/#estructura-de-cliente). Éste campo es util cuando se lo junta con el campo de vencimiento \(donde se indica la fecha de vencimiento de manera manual\)
* **Nuevas monedas de facturación:** Ahora podes emitir comprobantes en otras monedas extranjeras. [Consultá las monedas disponibles aquí ](tablas-de-referencia.md#monedas). Si necesitas alguna que no esté incluida, solicitála via email. 



## 05 de Agosto de 2019

**Nuevo comprobante:** Se agrega el porcentaje de impuestos internos dentro del bloque de  cada "producto

## 10 de Julio de 2019

**1\) Nuevos campos para Percepciones e Impuestos internos** Se agregaron campos dentro del bloque "comprobantes" para el envio de las percepciones e impuestos internos   
percepciones\_iibb\_base,  
percepciones\_iibb\_alicuota,  
percepciones\_iva\_base,  
percepciones\_iva\_alicuota,  
impuestos\_internos\_base,  
impuestos\_internos\_alicuota,  
**D**ocumentacion:   [https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante](https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante)  
  
**2\) RG Especiales**

Se creo un nuevo bloque de información para enviar los datos asociados a RG Especiales.AFIP requiere que segun las diferentes RG que tiene publicadas, se envien datos adicionales.Estos datos, estan catalogados en la siguiente tabla, según el regimen al que correspondan:[https://tusfacturas.gitbook.io/api-factura-electronica-afip/tablas-de-referencia\#datos-opcionales-para-rg-especiales](https://tusfacturas.gitbook.io/api-factura-electronica-afip/tablas-de-referencia#datos-opcionales-para-rg-especiales)  
Ej: Quienes facturan alquileres casa familia, aplicados a la RG 4004-E deben enviar datos adicionales.Lo mismo sucede, con los nuevos comprobantes de tipo "Factura Electronica de Creédito MiPyme \(FCE\)"Consultá la documentacion:  [https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante\#estructura-de-rg-especiales](https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante#estructura-de-rg-especiales)  
  
**3\) Comprobantes asociados**

Se agrego el campo "comprobante\_fecha" dentro de los datos a enviar. Éste campo es obligatorio para los nuevos comprobantes de tipo "Factura Electronica de Creédito MiPyme \(FCE\)"Consultá la documentacion:  [https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante\#estructura-de-comprobantes-asociados](https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante#estructura-de-comprobantes-asociados)   
  
**4\) Factura Electrónica de Creédito MiPyme \(FCE\)**

Se agrego la posibilidad de emitir éste tipo de comprobantes, en todas sus modalidades \(Facturas, Notas de debito y Notas de Credito\).Es importante que consulten con su contador/a las particularidades de éstos comprobantes, ya que requieren un tratamiento posterior especial, que no aplica a nuestra plataforma.En la documentación [https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante/factura-de-credito-electronica-mipyme-fce](https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante/factura-de-credito-electronica-mipyme-fce)   podrán encontrar ejemplos tanto de una factura A como de una NC

## 28 de Junio de 2019

Ajustes mandatorios requeridos por AFIP para las NC / ND. Éste cambio aplicará a la API y la WebApp www.tusfacturas.app  
Para ésto se requiere que envien dentro del bloque "comprobante", un array con los diferentes comprobantes asociados, según estructura:

`{"tipo_comprobante" : "FACTURA A", "punto_venta" : "145","numero" : 12313,"cuit": 111111111}`   
Ya se encuentra actualizada la documentación:  [https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante/factura-a-nota-de-debito-a-nota-de-credito-a](https://tusfacturas.gitbook.io/api-factura-electronica-afip/facturacion-nuevo-comprobante/factura-a-nota-de-debito-a-nota-de-credito-a)  
  


