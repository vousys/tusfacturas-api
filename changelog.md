# Changelog

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
  


