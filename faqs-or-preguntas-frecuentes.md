---
description: >-
  Resuelve tus dudas sobre la API de facturación electrónica AFIP de
  TusFacturasAPP
---

# FAQs | Preguntas generales

### **Si no quiero que mis clientes ingresen a TusFacturasAPP, ¿Se puede utilizar igual?**

Sí, podes utilizar nuestra plataforma de facturación electrónica incluso si tus clientes no son usuarios. Vos tendrías acceso como usuario principal y recibirías un instructivo de enlace con AFIP para enviar manualmente a cada cliente. De esta forma, todas las facturas que emitan tus clientes a través del sistema tendrán curso legal y estarán validadas por la AFIP. Nuestro sistema de facturación electrónica cumple con todos los requisitos fiscales y brinda una solución completa para gestionar las facturas de manera digital, segura y con respaldo legal.

### **¿Qué contabiliza como un request?**

Un request es toda petición realizada a la API en cualquiera de sus métodos, devuelva error o exito.

El límite de request que dispones para realizar las consultas, es el mismo limite que tenes habilitado en tu plan para la emisión de comprobantes . Ej: si tu plan incluye 1000 comprobantes, podrás realizar 1000 request a éste método en la suscripción en curso.

### **¿La URL de descarga de PDF cuenta como un request?**

No, la llamada para descargar facturas electrónicas en formato PDF no se considera request adicional en nuestro sistema de facturación. Sin embargo, es importante tener en cuenta que las URLs de descarga de PDF son temporales por motivos de seguridad. Por eso, recomendamos descargar siempre el archivo PDF en tu propio servidor para poder consultarlo las veces que sea necesario de manera local y permanente. De esta forma, optimizas el uso de nuestro servicio de facturación electrónica y mantienes un respaldo confiable de tus comprobantes fiscales en cualquier momento.

### **¿Puedo generar el PDF desde mi plataforma?**

Sí, podes generar el PDF desde tu plataforma. Al realizar una nueva facturación a través de nuestra API, TusFacturasAPP te envía en la respuesta todos los datos clave que necesitas, como el Código de Autorización Electrónica (CAE), la fecha de vencimiento del CAE y el texto requerido para generar el código QR correspondiente. De esta manera, tu plataforma puede automatizar la creación de facturas en formato PDF con información válida y autorizada por la AFIP, lo que garantiza el cumplimiento de las regulaciones fiscales vigentes y brinda una experiencia de facturación digital completa para ti y tus clientes.

### **¿Es muy tedioso de configurar?**

No. TusFacturasAPP se caracteriza por ser muy simple de usar y de configurar. Para comenzar a facturar tan solo debes hacer los siguientes pasos:

1. Das de alta en nuestra plataforma el CUIT+ PDV, completando la info obligatoria.
2. Haces el enlace con AFIP según el instructivo que se envía automáticamente desde la plataforma. Todo se hace online, no puede llevarte más de 10 mins, pero necesitas  tener los datos de AFIP (CUIT y la clave fiscal), para poder entrar y hacerlo. TusFacturasAPP no gestiona ni administra datos de acceso al panel de AFIP de los clientes.

### **¿Es un servicio de marca blanca?**

No, nuestro sistema de facturación electrónica no es un servicio de marca blanca. Por cuestiones legales y de transparencia, nuestra plataforma agrega un pie de página en los archivos PDF de las facturas, indicando que el comprobante fue emitido a través de nuestro sistema TusFacturasAPP. Además, en los correos electrónicos que se envían con los comprobantes de venta emitidos, se menciona a TusFacturasAPP como el proveedor del servicio de facturación, aunque tú puedes configurar el nombre de remitente (from name) y la dirección de respuesta (reply to) según tus preferencias. De esta manera, garantizamos el cumplimiento de las regulaciones fiscales vigentes y brindamos un servicio de facturación electrónica transparente y confiable para ti y tus clientes.

### **¿Qué sucede si se cae AFIP, como se manejan los errores?**

En caso de que se produzcan caídas o interrupciones en los servicios de la AFIP, nuestro sistema de facturación electrónica activa automáticamente alertas y notificaciones de error para evitar inconsistencias en los comprobantes emitidos. En ocasiones, puede suceder que un comprobante quede pendiente de procesamiento en los servidores de la AFIP, pero nuestra plataforma no reciba la respuesta correspondiente. En estos casos excepcionales, nuestro servicio te indicará que debes reenviar ese comprobante en particular, proporcionándote los datos clave como el número de comprobante, fechas y montos, que ya fueron registrados en la AFIP. De esta manera, garantizamos la integridad y trazabilidad de tus facturas electrónicas, cumpliendo con los estándares de facturación digital y minimizando los riesgos de inconsistencias o errores en tu operatoria fiscal.

### **Estoy integrando desde reactjs y obtengo un error de CORS.**

En ese caso, te sugerimos que tu frontend se comunique con tu backend y desde el backend realices la petición a nuestra API. También te sugerimos usar axios para el fetch

### **¿AFIP me permite facturar con cualquier fecha?**

No, la AFIP no permite facturar con cualquier fecha. La normativa vigente establece restricciones específicas para la emisión de comprobantes con fechas anteriores. En el caso de contribuyentes cuyas actividades están categorizadas como servicios, la AFIP permite facturar con una anterioridad máxima de 10 días. Por otro lado, para aquellos contribuyentes dedicados a la comercialización de bienes, el plazo máximo de anterioridad es de 5 días. Estas limitaciones también aplican siempre y cuando no se hayan emitido previamente otros comprobantes con fechas posteriores a la que se desea facturar. Nuestro sistema de facturación electrónica cumple estrictamente con estos requisitos de la AFIP para garantizar la validez legal de tus facturas y evitar posibles sanciones o inconvenientes fiscales.

Ej:&#x20;

Si  hoy es 20/10/2022 y queres emitir una factura con fecha 01/10/2022 AFIP te lo va a rechazar.

Si  hoy es 20/10/2022 y queres emitir una factura con fecha 18/10/2022, pero ya emitiste una con fecha 10/10/2022, AFIP te lo va a rechazar.

### **¿Puedo eliminar o modificar un comprobante que impactó en AFIP?**

No, los comprobantes que han sido registrados y aceptados por la AFIP no pueden ser anulados directamente en nuestro sistema de facturación electrónica. De acuerdo con las regulaciones fiscales vigentes, aquellos comprobantes que ya han impactado y quedado registrados en los sistemas de la AFIP, sólo pueden ser revertidos o anulados contablemente mediante la emisión de una nota de crédito. Esta nota de crédito debe ser generada a través de nuestra plataforma de facturación electrónica, cumpliendo con todos los requisitos legales y formales exigidos por la AFIP. De esta manera, se mantiene la trazabilidad e integridad de tus registros contables y fiscales, evitando posibles inconsistencias o sanciones por parte del ente regulador.

### **¿Como es la numeración de los comprobantes?**

La numeración de los comprobantes en nuestro sistema de facturación electrónica sigue una secuencia lógica y organizada basada en dos factores clave: el tipo de comprobante y el punto de venta. Cada combinación de tipo de comprobante (Factura A, Factura B, Nota de Crédito, etc.) y punto de venta tiene su propia secuencia numérica independiente. Por ejemplo, si emitiste la Factura A del punto de venta 00001 con el número 0000123, la siguiente Factura A del mismo punto de venta será la 0000124. No obstante, puedes tener múltiples puntos de venta configurados, lo que te permite emitir comprobantes con numeraciones diferentes de manera simultánea. Así, podrías tener la Factura A 00002-0000123 del punto de venta 00002 y, al mismo tiempo, la Factura B 00001-0000123 del punto de venta 00001. Esta estructura de numeración secuencial y organizada por tipo de comprobante y punto de venta facilita la gestión y el control de tus operaciones de facturación electrónica, cumpliendo con los requisitos legales y formales exigidos por la AFIP.

### **¿Los PDFs que se generan de la factura, quedan disponibles para mas adelante en algun CDN o los tengo que descargar y guardar yo?**

Nuestro sistema de facturación electrónica está diseñado para brindar un flujo de trabajo eficiente y seguro. Cada vez que se emite un comprobante a través de nuestra API, se genera una URL temporal que te permite descargar el archivo PDF correspondiente en ese preciso momento. Es fundamental que aproveches esta oportunidad para descargar y resguardar localmente los PDF de tus facturas, ya que si tu suscripción a nuestro servicio no se encuentra activa y vigente, no podrás acceder ni descargar estos comprobantes nuevamente desde nuestra plataforma. Por esta razón, recomendamos enfáticamente descargar y almacenar los PDF de forma inmediata, asegurándote de tener un respaldo local y permanente de tus facturas electrónicas. De esta manera, podrás cumplir con tus obligaciones fiscales, mantener un registro confiable y evitar posibles contratiempos o sanciones por falta de respaldo documental.

### **¿Nuestro sistema va a ir sumando clientes paulatinamente, que tipo de suscripción me conviene contratar?**&#x20;

Nuestros planes de facturación electrónica ofrecen la flexibilidad de contratar una suscripción con límites definidos de CUITs/Puntos de Venta y cantidad de comprobantes. Esto te permite gestionar y administrar de manera centralizada la facturación de múltiples clientes o unidades de negocio. Sin embargo, algunos de nuestros clientes han compartido experiencias en las que esta modalidad no resultó óptima para sus necesidades específicas. En algunos casos, al tener un plan con capacidad limitada, el crecimiento repentino de uno de sus clientes los obligó a contratar un plan superior con mayor costo, lo que afectó la rentabilidad de su operación.

Como alternativa, estas empresas han optado por un modelo en el que cada cliente contrata su propia suscripción a nuestro servicio de facturación electrónica, y ellos brindan acceso a través de su plataforma cobrando un fee por la gestión y administración. Esta estrategia les permite escalar sin límites, adaptarse a las necesidades cambiantes de cada cliente y optimizar sus costos operativos.

Es importante que analices detenidamente las ventajas y desafíos de cada modelo de suscripción, considerando el tamaño y proyección de crecimiento de tus clientes, para elegir la opción más conveniente y rentable para tu empresa. En TusFacturasAPP, estamos comprometidos en brindarte todas las herramientas y flexibilidad necesarias para que puedas implementar la estrategia que mejor se ajuste a tus requerimientos comerciales y operativos



### **¿Qué sucede si me quedo sin cupo de facturación?**

Nuestro sistema de facturación electrónica cuenta con límites de capacidad basados en la cantidad de comprobantes que puedes emitir según el plan de suscripción contratado. Si llegas a agotar tu cupo de facturación, recibirás un mensaje de error en cada solicitud o request que envíes a través de nuestra API, impidiéndote emitir nuevos comprobantes hasta que adquieras una renovación o ampliación de tu suscripción.

Para ayudarte a gestionar y monitorear tu capacidad de facturación, TusFacturasAPP implementa un sistema de notificaciones por correo electrónico. Cuando tu cupo disponible se encuentre por debajo del 20%, todos los usuarios administradores de tu espacio de trabajo recibirán un aviso por email alertando sobre esta situación. Esta notificación se repetirá cada 3 días hasta que renueves tu suscripción o amplíes tu capacidad de facturación.

De esta manera, podrás anticiparte y tomar las medidas necesarias para evitar interrupciones en tus operaciones de facturación electrónica, garantizando el cumplimiento de tus obligaciones fiscales y brindando un servicio continuo a tus clientes. En TusFacturasAPP, nos enfocamos en ofrecerte herramientas y funcionalidades que faciliten la gestión y el control de tus procesos de facturación digital.



**¿Tenes más dudas?** Contactanos por el chat de la web [www.tusfacturas.app](https://www.tusfacturas.app)

