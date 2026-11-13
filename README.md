---
description: >-
  API REST para emitir facturas y notas de crédito con CAE de ARCA, enviando un
  JSON, sin SOAP, certificados ni tokens. Desde 2015 en producción, con
  monitoreo continuo y respaldo impositivo.
---

# API REST de factura electrónica ARCA (ex AFIP) fácil – TusFacturasAPP

TusFacturasAPP® es una API REST para emitir comprobantes electrónicos con CAE de ARCA (ex AFIP) desde cualquier sistema. TusFacturasAPP® es una marca registrada de VYAR S.R.L. y está en producción desde 2015, con monitoreo continuo de VOUSYS® y el respaldo de un estudio impositivo que nos mantiene actualizados con las últimas normativas de facturación Argentina.

TusFacturasAPP es una plataforma privada e independiente de facturación y gestión, que no pertenece ni está vinculada a ARCA (ex AFIP) ni a ningún organismo público. Los comprobantes se emiten a través de los web services oficiales de ARCA, con el CUIT que cada usuario configura y habilita.

Tu sistema envía un JSON con los datos del comprobante y recibe el CAE, el número asignado y el PDF con QR. La autenticación WSAA, los certificados, la numeración y los cambios en los web services de ARCA quedan del lado de TusFacturasAPP® siempre que sea posible.&#x20;

### Ficha técnica

|                     |                                                                                                                                              |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Tipo de API         | REST, versión 2                                                                                                                              |
| URL base            | `https://www.tusfacturas.app/app/api/v2/`                                                                                                    |
| Formato             | JSON, UTF-8                                                                                                                                  |
| Método              | POST                                                                                                                                         |
| Seguridad           | HTTPS con TLS 1.2 o superior                                                                                                                 |
| Autenticación       | `apikey`, `apitoken` y `usertoken` en el cuerpo del pedido (ver [Autenticación](como-empiezo/api-factura-electronica-afip-autenticacion.md)) |
| Modos de emisión    | Sincrónico (individual o por lotes) y asincrónico (individual)                                                                               |
| Notificaciones      | Webhooks                                                                                                                                     |
| SDK                 | PHP ([GitHub](https://github.com/vousys/tusfacturas))                                                                                        |
| Prueba              | Cuenta gratuita, renovable las veces que necesites.                                                                                          |
| Estado del servicio | Endpoint de [estado de servicios ARCA y API](web-services-afip-api-arca/api-factura-electronica-afip-estado-de-los-servicios-afip.md)        |

### Qué podes hacer con la API

* **Emisión de facturas electrónicas con CAE.** Facturas A, B, C, E (exportación), M y Factura de Crédito Electrónica MiPyME, autorizadas por ARCA. Ver la [referencia de campos](api-factura-electronica-afip-facturacion-ventas/referencia-de-la-api-campos-para-crear-comprobantes-en-arca.md).
* **Facturas y notas de crédito.** Las notas de crédito y débito se emiten con el mismo endpoint que las facturas, asociadas al comprobante original o a un período. Ver [notas de crédito y débito](api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-notas-credito-debito.md).
* **Consulta de comprobantes.** Obtené un comprobante por tipo y número, o listá los de una fecha, un rango o tu propio identificador. Ver [consulta simple](api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-consulta-de-comprobantes.md) y [consulta avanzada](api-factura-electronica-afip-facturacion-ventas/consulta-avanzada-listar-comprobantes-por-fecha-rango-o-external-reference.md).
* **Descarga de PDF.** Cada comprobante emitido trae el link al PDF en A4 y en ticket de 80 mm, con el código QR de ARCA.
* **Webhooks para notificaciones.** En modo asincrónico te avisamos cuando el comprobante queda autorizado o si tuvo errores. Ver [facturación asincrónica](api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md).
* **Entorno de pruebas gratuito.** Integrá y probá sin costo antes de pasar a producción. [Crear cuenta de prueba](https://www.tusfacturas.app/probar-gratis-api-factura-electronica-tusfacturasapp).

Además:

* **Consultar ARCA:** datos de un CUIT desde la constancia de inscripción, base APOC de facturas apócrifas, cotizaciones oficiales y obligados a recibir FCE MiPyME.
* **Consultar padrones provinciales:** alícuotas de ARBA y AGIP.
* **Gestionar el negocio:** recibos de cobro, órdenes de pago, cuentas corrientes, productos y stock, reportes de IVA compras y ventas.
* **Integrar sin código:** Zapier.

### Quién está detrás de TusFacturasAPP®

* Empresa: VYAR S.R.L., CUIT 30-71625243-0, Buenos Aires, Argentina.
* Marca registrada en INPI: registro N° 3.480.509.
* Desarrollada por: [VOUSYS®](https://www.vousys.com/)
* Respaldo impositivo continuo.
* En producción desde 2015.

Más información en sobre [TusFacturasAPP®](https://www.tusfacturas.app/).

### Lenguajes

La API acepta cualquier lenguaje que pueda hacer un pedido HTTPS con JSON. Hay integraciones en producción en PHP, Python, Node.js, Ruby y Visual Basic 6.0, sobre AWS, Google Cloud y servidores propios. Tenes [ejemplos en cURL, PHP, Python, Node.js y Ruby ](como-empiezo/api-factura-electronica-afip-plugins-y-sdks.md)

### Soporte

* Email técnico con humanos: api@tusfacturas.app
* Chat en [tusfacturas.app](https://www.tusfacturas.app/) &#x20;
* Centro de ayuda: [ayuda.tusfacturas.app](https://ayuda.tusfacturas.app/)

