# Documentación de la API para Factura Electrónica AFIP

Ademas, podrás generar y consultar de manera segura, comprobantes de venta y de compra , como así también utilizar todas las funcionalidades que te brinda nuestra plataforma web. 

{% hint style="info" %}
Importante: Para utilizar la API debes estar [registradx](https://www.tusfacturas.com.ar/registrarme-factura-electronica.html). 

Mientras estés en etapa de testing, configurá tu CUIT, con un punto de venta irreal \(Ej: 679\), y usa ese CUIT de prueba para facturar. La respuesta que recibirás es la misma que si facturas contra AFIP, solo que los campos CAE y Vencimiento del CAE te retornaran vacios. Una vez que hayas probado todos los métodos, eliminá todos los comprobantes asociados a ese PDV, elimina el PDV y crea el nuevo CUIT+punto de venta para poder enlazarlo con AFIP. 

Tené en cuenta que al registrarte, cualquier usuario goza de un plan gratuito que le permite emitir 5 comprobantes por mes, pero **no posee acceso API para pruebas**. Para probar la integración con la API, contáctanos a tusfacturas@vousys.com, **desde la casilla con la cual te registraste** \(**debe ser una dirección de e-mail válida, la cual podamos validar y corroborar su existencia** \) y te brindamos un plan API DEV por 1 mes sin costo \(solo para nuevas cuentas y por única vez\). Una vez vencido tu período de prueba, debes contratar algún [plan API](https://www.tusfacturas.com.ar/tarifas-factura-electronica.html) de los que tenemos disponibles [aquí](https://www.tusfacturas.com.ar/tarifas-factura-electronica.html) .

Resumen de pasos para comenzar a trabajar:

1\)  Crear tu cuenta [aquí](https://www.tusfacturas.app)

2\) Configurar tu CUIT + PDV

3\) Contactar a tusfacturas@vousys.com para solicitar plan API DEV según requerimientos mencionados.

4\) Una vez activado el plan API DEV, Ir al menú  "Mi espacio de trabajo &gt; Configurar éste espacio de trabajo y habilitar tu IP  dentro del bloque "ACCESO API".
{% endhint %}

  
En la documentación encontrarás algunos ejemplos para que luego los adaptes al lenguaje de tu sistema actual; Si bien no te podemos brindar soporte para los diferentes lenguajes de programación que existen en el mercado, al ser los input y los output en formato JSON, podes conectarlo el lenguaje que mas te guste, teniendo a mano stackoverflow por si tenes dudas ;\) 

  
Versión actual: **API v2**   
Tipo de API: **API Rest**

SSL: **requiere TLS 1+**  
Tipo de datos entrada y respuesta: **JSON**  
Charset: **UTF-8**  
Tipo de request : **POST**  
URL : **https://www.tusfacturas.app/app/api/v2/estado\_servicios/alertas**  




**Tené en cuenta éstas cosas:**  
1\) Para procesar correctamente los campos, debes enviarlos siempre encodeados con **UTF-8**.   
2\) Cuando realices comprobantes AFIP Factura electrónica válida, tené en cuenta que cada request que hagas para generar comprobantes, debe tener una diferencia de tiempo de 1 minuto, ya que sino la misma AFIP te bloquea el CUIT  y no podrás emitir comprobantes por unos minutos.   
3\) Nuestra API ya ha sido implementada contra sistemas que trabajan en PHP, Visual basic 6.0 y Ruby, como asi tambien entornos AMAZON WS, Google Cloud, servidores dedicados y servidores compartidos. 



{% page-ref page="api-factura-electronica-afip-plugins-y-sdks.md" %}



