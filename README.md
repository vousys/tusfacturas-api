# Documentación de la API para Factura Electrónica AFIP

Al utilizar la API de facturación electrónica de TusFacturasAPP,  podrás generar de manera segura y rápida, facturas electrónicas AFIP.

Contamos con el respaldo de un estudio impositivo que nos mantiene asesorados ante las nuevas normativas que surgen día a día en nuestro país/

&#x20;Ademas de usar la API, podrás utilizar nuestra plataforma web, con todas las funcionalidades que ésta brinda.&#x20;

\
En la documentación encontrarás algunos ejemplos en JSON, para que luego los adaptes al lenguaje de tu sistema actual; Si bien no te podemos brindar soporte para los diferentes lenguajes de programación que existen en el mercado, al ser los input y los output en formato JSON, podes conectarlo el lenguaje que mas te guste, teniendo a mano stackoverflow, por si tenes dudas ;)&#x20;

\
Versión actual: **API v2** \
Tipo de API: **API Rest**

SSL: **requiere TLS 1.2+**\
Tipo de datos entrada y respuesta: **JSON**\
Charset: **UTF-8**\
Tipo de request : **POST**\
URL : **https://www.tusfacturas.app/app/api/v2/estado\_servicios/alertas**\




**Tené en cuenta éstas cosas:**\
1\) Para procesar correctamente los campos, debes enviarlos siempre encodeados con **UTF-8**. \
2\) Cuando realices comprobantes AFIP Factura electrónica válida, ten en cuenta que cada request que hagas para generar comprobantes, debe tener una diferencia de tiempo de 1 a 2 minutos, ya que dependiendo de como funcionen los servicios de AFIP,  pueden existir bloqueos y no podrás emitir comprobantes por unos minutos. \
3\) Nuestra API ya ha sido implementada contra diferentes sistemas, desarrollados con múltiples lenguajes (PHP, Visual basic 6.0, Ruby, node), como asi tambien en entornos AMAZON WS, Google Cloud, servidores dedicados y servidores compartidos.&#x20;
