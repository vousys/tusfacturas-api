---
description: >-
  Resolve tus dudas sobre la API de facturación electrónica AFIP de
  TusFacturasAPP
---

# FAQs | Preguntas generales

### **¿La API de TusFacturasAPP tiene rate limit?**

Sí. La API cuenta con un rate limit  de <mark style="color:purple;">**25 requests en 10 segundos**</mark>  para proteger la estabilidad del servicio y garantizar un uso equitativo entre todos los usuarios.  Si tu integración supera el límite, vas a recibir un error de bloqueo temporal en lugar de la respuesta habitual de la API. Ese error no proviene del procesamiento de tu comprobante, sino del control de tráfico, y se resuelve solo una vez que baja el volumen de requests.

### En la modalidad instantánea ¿Puedo enviar la external reference? ¿Queda guardada?

Si, podes enviarla y queda guardada pero no te enviaremos un hook.

### **Si no quiero que mis clientes ingresen a TusFacturasAPP, ¿Se puede utilizar igual?**

Sí, podes utilizar nuestra plataforma de facturación electrónica incluso si tus clientes no son usuarios de TusFacturasAPP. Vos tendrías acceso como usuario principal y recibirías un instructivo de enlace con ARCA/AFIP para enviar manualmente a cada cliente. De esta forma, todas las facturas que emitan tus clientes a través del sistema tendrán curso legal y estarán validadas por ARCA.

**¿Tengo que mencionar a TusFacturasAPP en mi plataforma?**

Sí. Si utilizas nuestra API como motor de facturación dentro de tu propia plataforma o sistema, debes informarlo de forma visible en tu sitio web, incluyendo un enlace a [www.tusfacturas.app](https://www.tusfacturas.app), identificando a TusFacturasAPP® como proveedor del servicio de facturación electrónica. Podes usar una mención del estilo: _“Facturación electrónica provista por_ [_TusFacturasAPP®_](https://www.tusfacturas.app)_”_.

Lo que **no** está permitido es revender o presentar el servicio como propio, bajo tu marca o cualquier otra denominación, sin identificar a TusFacturasAPP® como proveedor tecnológico. Para más detalles, consulta nuestros [Términos y Condiciones](https://www.tusfacturas.app/terminos-y-condiciones.html), puntos 9 y 17.

### **¿Qué contabiliza como un request?**

Un request es cualquier petición realizada a la API, independientemente del método utilizado o si devuelve éxito o error.  Conoce más sobre [cómo se contabiliza el cupo API](https://ayuda.tusfacturas.app/es/articles/14657130-como-se-consume-el-cupo-de-la-api)&#x20;

### **¿La URL de descarga de PDF cuenta como un request?**

No, la llamada para descargar facturas electrónicas en formato PDF no se considera request adicional en nuestro sistema de facturación. Sin embargo, es importante tener en cuenta que las URLs de descarga de PDF son temporales por motivos de seguridad. Por eso, recomendamos descargar siempre el archivo PDF en tu propio servidor para poder consultarlo las veces que sea necesario de manera local y permanente. De esta forma, optimizas el uso de nuestro servicio de facturación electrónica y mantienes un respaldo confiable de tus comprobantes fiscales en cualquier momento.

### **¿Puedo generar el PDF desde mi plataforma?**

Sí, podes generar el PDF desde tu plataforma. Al realizar una nueva facturación a través de nuestra API, TusFacturasAPP te envía en la respuesta todos los datos clave que necesitas, como el Código de Autorización Electrónica (CAE), la fecha de vencimiento del CAE y el texto requerido para generar el código QR correspondiente. De esta manera, tu plataforma puede automatizar la creación de facturas en formato PDF con información válida y autorizada por la AFIP, lo que garantiza el cumplimiento de las regulaciones fiscales vigentes y brinda una experiencia de facturación digital completa para ti y tus clientes.

### **¿Es muy tedioso de configurar?**

No. TusFacturasAPP se caracteriza por ser muy simple de usar y de configurar. Para comenzar a facturar tan solo debes hacer los siguientes pasos:

1. Das de alta en nuestra plataforma el CUIT+ PDV, completando la info obligatoria.
2. Haces el enlace con AFIP según el instructivo que se envía automáticamente desde la plataforma. Todo se hace online, no puede llevarte más de 10 mins, pero necesitas  tener los datos de AFIP (CUIT y la clave fiscal), para poder entrar y hacerlo. TusFacturasAPP no gestiona ni administra datos de acceso al panel de AFIP de los clientes.

### **¿Es un servicio de marca blanca?**

No. TusFacturasAPP® no es un servicio de marca blanca, y es importante entender qué implica eso en la práctica antes de integrarte.

**¿Dónde aparece la marca TusFacturasAPP®?**

* **PDF de la factura:** nuestro sistema agrega automáticamente un pie de página en todos los archivos PDF indicando que el comprobante fue emitido a través de TusFacturasAPP®. Esto no puede ser removido ni personalizado.
* **Correos electrónicos de envío de comprobantes:** los emails que se envían a los destinatarios de las facturas mencionan a TusFacturasAPP® como proveedor del servicio. Sin embargo, podes configurar el nombre del remitente (_from name_) y la dirección de respuesta (_reply to_) con los datos de tu empresa o los de tu cliente.
* **Mensajes de error:** las respuestas de error de la API pueden incluir referencias a TusFacturasAPP® como parte de la descripción del problema.
* **Instructivo de enlace con ARCA:** el documento que se envía automáticamente para configurar el enlace con ARCA menciona a TusFacturasAPP® como la plataforma desde la cual se realiza el proceso.
* **Otros puntos de contacto:** la marca puede aparecer en otras comunicaciones automáticas, notificaciones del sistema y documentación generada por la plataforma.

**¿Puedo integrar la API en mi plataforma y ofrecerla a mis clientes?**

Sí, podes usar nuestra API como motor de facturación electrónica dentro de tu propia plataforma o sistema. En ese caso aplican las siguientes condiciones:

* **Lo que está permitido:** ofrecer el servicio de facturación a tus clientes a través de tu plataforma, cobrando un fee por la gestión si así lo deseas.
* **Lo que está prohibido:** revender el servicio bajo la marca TusFacturasAPP® o presentarlo como un desarrollo propio, omitiendo nuestra identidad como proveedor tecnológico.
* **Lo que es obligatorio:** informar de forma visible en tu sitio web que la facturación electrónica es provista por TusFacturasAPP®, incluyendo un enlace a [www.tusfacturas.app](https://www.tusfacturas.app). Podes usar una mención del estilo: _“Facturación electrónica provista por_ [_TusFacturasAPP®_](https://www.tusfacturas.app)_”_. El uso del logotipo o elementos gráficos de nuestra marca requiere autorización previa por escrito.

Para más detalles sobre estas condiciones, consulta nuestros [Términos y Condiciones](https://www.tusfacturas.app/terminos-y-condiciones.html), puntos 9 y 17.

### **¿Qué sucede si se cae ARCA, como se manejan los errores?**

En caso de que se produzcan caídas o interrupciones en los servicios de la AFIP, nuestro sistema de facturación electrónica activa automáticamente alertas y notificaciones de error para evitar inconsistencias en los comprobantes emitidos. En ocasiones, puede suceder que un comprobante quede pendiente de procesamiento en los servidores de la AFIP, pero nuestra plataforma no reciba la respuesta correspondiente. En estos casos excepcionales, nuestro servicio te indicará que debes reenviar ese comprobante en particular, proporcionándote los datos clave como el número de comprobante, fechas y montos, que ya fueron registrados en la AFIP. De esta manera, garantizamos la integridad y trazabilidad de tus facturas electrónicas, cumpliendo con los estándares de facturación digital y minimizando los riesgos de inconsistencias o errores en tu operatoria fiscal.

### **Estoy integrando desde reactjs y obtengo un error de CORS.**

En ese caso, te sugerimos que tu frontend se comunique con tu backend y desde el backend realices la petición a nuestra API. También te sugerimos usar axios para el fetch

### **¿AFIP me permite facturar con cualquier fecha?**

No, ARCA no permite facturar con cualquier fecha. La normativa vigente establece restricciones específicas para la emisión de comprobantes con fechas anteriores. Conoce  [hasta cuántos días podes facturar para atrás](https://ayuda.tusfacturas.app/es/articles/10355161-hasta-cuantos-dias-puedo-facturar-para-atras). Nuestro sistema de facturación electrónica cumple estrictamente con estos requisitos de la AFIP para garantizar la validez legal de tus facturas y evitar posibles sanciones o inconvenientes fiscales.&#x20;

### **¿Puedo eliminar o modificar un comprobante que impactó en ARCA (ex AFIP)?**

No. Los comprobantes que han sido registrados y aceptados por ARCA no pueden ser anulados directamente en nuestro sistema de facturación electrónica. De acuerdo con las regulaciones fiscales vigentes, aquellos comprobantes que ya han impactado y quedado registrados en los sistemas de ARCA, sólo pueden ser revertidos o anulados contablemente mediante la emisión de una nota de crédito. Esta nota de crédito debe ser generada a través de nuestra plataforma de facturación electrónica, cumpliendo con todos los requisitos legales y formales exigidos por ARCA. De esta manera, se mantiene la trazabilidad e integridad de tus registros contables y fiscales, evitando posibles inconsistencias o sanciones por parte del ente regulador.

### **¿Como es la numeración de los comprobantes?**

La numeración de los comprobantes en nuestro sistema de facturación electrónica sigue una secuencia lógica y organizada basada en dos factores clave: el tipo de comprobante y el punto de venta. Cada combinación de tipo de comprobante (Factura A, Factura B, Nota de Crédito, etc.) y punto de venta tiene su propia secuencia numérica independiente. Por ejemplo, si emitiste la Factura A del punto de venta 00001 con el número 0000123, la siguiente Factura A del mismo punto de venta será la 0000124. No obstante, puedes tener múltiples puntos de venta configurados, lo que te permite emitir comprobantes con numeraciones diferentes de manera simultánea. Así, podrías tener la Factura A 00002-0000123 del punto de venta 00002 y, al mismo tiempo, la Factura B 00001-0000123 del punto de venta 00001. Esta estructura de numeración secuencial y organizada por tipo de comprobante y punto de venta facilita la gestión y el control de tus operaciones de facturación electrónica, cumpliendo con los requisitos legales y formales exigidos por la AFIP.

### **¿Los PDFs que se generan de la factura, quedan disponibles para mas adelante en algún CDN o los tengo que descargar y guardar yo?**

Nuestro sistema de facturación electrónica está diseñado para brindar un flujo de trabajo eficiente y seguro. Cada vez que se emite un comprobante a través de nuestra API, se genera una URL temporal que te permite descargar el archivo PDF correspondiente en ese preciso momento. Es fundamental que aproveches esta oportunidad para descargar y resguardar localmente los PDF de tus facturas, ya que si tu suscripción a nuestro servicio no se encuentra activa y vigente, no podrás acceder ni descargar estos comprobantes nuevamente desde nuestra plataforma. Por esta razón, recomendamos enfáticamente descargar y almacenar los PDF de forma inmediata, asegurándote de tener un respaldo local y permanente de tus facturas electrónicas. De esta manera, podrás cumplir con tus obligaciones fiscales, mantener un registro confiable y evitar posibles contratiempos o sanciones por falta de respaldo documental.

### **¿Nuestro sistema va a ir sumando clientes paulatinamente, que tipo de suscripción me conviene contratar?**&#x20;

Nuestros planes de facturación electrónica ofrecen la flexibilidad de contratar una suscripción con límites definidos de CUITs/Puntos de Venta y cantidad de comprobantes. Esto te permite gestionar y administrar de manera centralizada la facturación de múltiples clientes o unidades de negocio. Sin embargo, algunos de nuestros clientes han compartido experiencias en las que esta modalidad no resultó óptima para sus necesidades específicas. En algunos casos, al tener un plan con capacidad limitada, el crecimiento repentino de uno de sus clientes los obligó a contratar un plan superior con mayor costo, lo que afectó la rentabilidad de su operación.

Como alternativa, estas empresas han optado por un modelo en el que cada cliente contrata su propia suscripción a nuestro servicio de facturación electrónica, y ellos brindan acceso a través de su plataforma cobrando un fee por la gestión y administración. Esta estrategia les permite escalar sin límites, adaptarse a las necesidades cambiantes de cada cliente y optimizar sus costos operativos.

Es importante que analices detenidamente las ventajas y desafíos de cada modelo de suscripción, considerando el tamaño y proyección de crecimiento de tus clientes, para elegir la opción más conveniente y rentable para tu empresa. En TusFacturasAPP, estamos comprometidos en brindarte todas las herramientas y flexibilidad necesarias para que puedas implementar la estrategia que mejor se ajuste a tus requerimientos comerciales y operativos

**¿Dudas sobre la estructura de tu cuenta?**

Si necesitas evaluar si te conviene utilizar uno o varios espacios de trabajo, te recomendamos consultar los siguientes artículos de ayuda:

* [¿Qué es un espacio de trabajo?](https://ayuda.tusfacturas.app/es/articles/11832654-que-es-un-espacio-de-trabajo)
* [Gestión de múltiples clientes: ¿Espacios de trabajo separados o uno único?](https://ayuda.tusfacturas.app/es/articles/11839614-gestion-de-multiples-clientes-conviene-espacios-de-trabajo-separados-vs-unico)
* [¿Qué es un punto de venta?](https://ayuda.tusfacturas.app/es/articles/10421730-que-es-un-punto-de-venta)

### **¿Qué sucede si me quedo sin cupo de facturación?**

Nuestro sistema de facturación electrónica cuenta con límites de capacidad basados en la cantidad de comprobantes que puedes emitir según el plan de suscripción contratado. Si llegas a agotar tu cupo de facturación, recibirás un mensaje de error en cada solicitud o request que envíes a través de nuestra API, impidiéndote emitir nuevos comprobantes hasta que adquieras una renovación o ampliación de tu suscripción.

Para ayudarte a gestionar y monitorear tu capacidad de facturación, TusFacturasAPP implementa un sistema de notificaciones por correo electrónico. Cuando tu cupo disponible se encuentre por debajo del 20%, todos los usuarios administradores de tu espacio de trabajo recibirán un aviso por email alertando sobre esta situación. Esta notificación se repetirá cada 3 días hasta que renueves tu suscripción o amplíes tu capacidad de facturación.

De esta manera, podras anticiparte y tomar las medidas necesarias para evitar interrupciones en tus operaciones de facturación electrónica, garantizando el cumplimiento de tus obligaciones fiscales y brindando un servicio continuo a tus clientes. En TusFacturasAPP, nos enfocamos en ofrecerte herramientas y funcionalidades que faciliten la gestión y el control de tus procesos de facturación digital.

### ¿Puedo contratar la suscripción desde el exterior para mi cliente en Argentina?

Si. Consulta éste artículo de ayuda:  [Soy una Empresa del Exterior: Cómo Adquirir una Suscripción para mi Cliente en Argentina](https://ayuda.tusfacturas.app/es/articles/13504270-soy-una-empresa-del-exterior-como-adquirir-una-suscripcion-para-mi-cliente-en-argentina)



### &#x20;¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).

