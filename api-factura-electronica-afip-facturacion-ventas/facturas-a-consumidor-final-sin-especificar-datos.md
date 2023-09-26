# Facturas a consumidor final, sin especificar datos

Si queres facturar un comprobante **a consumidor final, sin especificar su nombre y DNI**, debes enviar dentro del bloque "cliente" >  campo "tipo" y "número"  de documento, lo siguiente:

Nro de documento = "0"

Tipo de documento = "OTRO"

En nombre, indicá lo que tu contador/a te recomiende.

Tené en cuenta, que solo podrás facturar sin indicar el documento del comprador, hasta ciertos montos, que AFIP actualiza regularmente. TusFacturasAPP, cuenta con un método que te permite obtener el monto actualizado. [Consultá la documentación: los topes de venta a CF](https://developers.tusfacturas.app/api-factura-electronica-afip-or-consulta-de-tope-para-ventas-a-consumidor-final)   (basta con consultarlo 1 vez al día)
