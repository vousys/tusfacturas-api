---
description: >-
  ¿Tenes preguntas sobre las ventas programadas? Encontra las respuestas en
  nuestras FAQs.
---

# FAQs | Ventas asincrónicas

**Ventas programadas:** En el contexto de una plataforma de facturación electrónica como TusFacturasAPP, las ventas programadas se refieren a facturas que se generan y envían automáticamente en una fecha y hora pre-establecida.

**¿Por qué son útiles?**

* **Automatización:** Elimina la necesidad de generar facturas manualmente, ahorrando tiempo y recursos.
* **Planificación:** Permite planificar la emisión de facturas con anticipación, asegurando que se envíen a tiempo.
* **Recurrentes:** Son ideales para facturas recurrentes, como alquileres, suscripciones o servicios periódicos.
* **Control:** Facilita el control de los vencimientos y evita el envío de facturas fuera de plazo.

**En resumen,** las ventas programadas son una herramienta muy útil para automatizar procesos de facturación y garantizar que tus clientes reciban sus facturas a tiempo.

### Preguntas frecuentes sobre el servicio API de facturación AFIP asincrónico

#### Cuándo y qué se emiten las ventas asincrónicas

La cola de procesamiento intentará emitir en el transcurso del día , todos aquellos comprobantes que se encuentren:

* En cola
* Sin errores
* Que hayan intentado emitirse menos de 100 veces
* Y cuya fecha del comprobante, sea menor o igual a la del dia

***

#### ¿Donde puedo ver el listado de las ventas que tengo en cola de procesamiento?

Dentro de nuestra plataforma web >  menú > Facturación > Ventas en cola

***

#### ¿Qué acciones que puedo realizar sobre un comprobante en cola?

Podes realizar las siguientes operaciones:

* [Enviarlos a reprocesar](web-services-afip-api-arca/reenvio-de-comprobantes-encolados-con-error.md). Una vez que un comprobante fue marcado con errores, no se intentará emitir nuevamente, salvo que lo envies a reprocesar.
* Puedes [eliminarlo](web-services-afip-api-arca/eliminar-comprobantes-encolados.md), en caso que no se pueda procesar.
* Modificar la [fecha del comprobante](web-services-afip-api-arca/cambiar-fecha-a-comprobante-encolado.md) y automáticamente [enviarlos a reprocesar](web-services-afip-api-arca/reenvio-de-comprobantes-encolados-con-error.md).&#x20;

***

#### ¿Qué comprobantes no pueden enviarse en ésta modalidad de facturación?

* Pedidos, Remitos, presupuestos, órdenes de compra
* Comprobantes de exportación de tipo "E"&#x20;
* Comprobantes relacionados con remitos y/o pedidos, ya sea porque incluyes remitos o pedidos o porque intentas facturar un remito o pedido.
* Comprobantes de tipo "NO VÁLIDO EN AFIP"

***

#### ¿Qué sucede si pasó +1 día y los comprobantes no se pudieron emitir?

Los comprobantes permanecerán en la cola de procesamiento hasta tanto los elimines o bien cambies la fecha de emisión y se intenten emitir nuevamente

***

#### ¿Qué sucede una vez que el comprobante se emite?

Los comprobantes que se han podido emitir, pasan automáticamente al reporte de Mis Ventas, desapareciendo del listado de "ventas en cola"

***

#### Si un request es aceptado para su procesamiento, y se detectan errores, se vuelve a enviar automáticamente a procesar?

Solo se vuelve a enviar automáticamente a procesar, si el error obtenido, se debe a caídas del servicio de facturación de AFIP.

***

#### Si tengo comprobantes en cola de procesamiento, y quiero enviar un nuevo comprobante asincrónico, se puede?

Si, se puede, siempre y cuando cumpla con los requisitos mencionados para ser procesado.

***

#### Si tengo comprobantes en cola de procesamiento, y quiero enviar un nuevo request pero que sea en la modalidad instantánea, se puede?

No, no se puede. Recibirás un error instantáneo, informandote que existen comprobantes en cola y que solo podrás enviarlos bajo esa modalidad.&#x20;

***

#### En el hook que recibo, obtengo todos los datos del comprobante?

No. El hook te envia el estado de ese request y el mensaje de error, en caso que no se haya podido procesar.&#x20;

En caso de éxito, deberás realizar una  [consulta avanzada por external\_reference](api-factura-electronica-afip-facturacion-ventas/consulta-avanzada.md#como-realizar-una-consulta-avanzada-por-external-reference),  para obtener los datos generados de éste comprobante

***

#### ¿Hay una reducción de tiempo considerable al emitir los comprobantes de esta forma

Optimizas, porque lo podes dejar programado con anterioridad, podes mandar el lote el dia 5 e indicar que esos comprobantes se emitan el dia 29; además tu proceso no se trabaria esperando la respuesta de la factura como si la mandaras instantánea. Sigue con las siguientes y a medida q va procesando te va notificando.

***

#### ¿Qué sucede si los servicios de ARCA/AFIP no se encuentran funcionando, puedo enviar mas ventas?

Si, está especialmente desarrollado para éstos casos. Los requests que envíes, se guardarán en la cola de procesamiento y serán enviados a medida que los servicios de ARCA se restauren.

***

#### ¿Qué sucede si los servicios de ARCA no se encuentran funcionando y tengo comprobantes en cola?

Los comprobantes seguirán en la cola y se emitirán cuando los servicios de ARCA se encuentren funcionando, siempre y cuando la fecha de éstos comprobantes sea menor o igual a la del día.

***

#### ¿Puedo enviar requests con fecha posterior a hoy?

Si, podes enviarlos y quedarán en la cola de procesamiento hasta la fecha indicada en el comprobante.

***

#### ¿Puedo cambiar la fecha de un comprobante que se encuentra en la cola de procesamiento?

Si, para eso debés utilizar el método de:  [Cambiar fecha encolado](web-services-afip-api-arca/cambiar-fecha-a-comprobante-encolado.md)

***

#### ¿Puedo eliminar requests que aún no se han procesado?

Si, para eso debés utilizar el método de:  [Eliminar comprobante encolado](web-services-afip-api-arca/eliminar-comprobantes-encolados.md)

***

#### **Si creo un abono desde la API o desde la plataforma web, ¿Cada vez que se emita la factura, me notifica por webhook?**

No. La plataforma en ese caso no te notifica por webhook. Si llegas a necesitar ésta funcionalidad, por favor contactanos.

***

#### **Si se intentó emitir 100 veces un comprobante en cola, ¿En qué momento recibo un webhook con el error?**

Recibís un webhook de error cuando se alcance el máximo de intentos definidos.&#x20;

***

#### **¿Qué debo hacer si un comprobante superó el límite de reintentos?**

Debes solucionar el inconveniente, si es un error de datos vas a tener que eliminarlo y volverlo a crear. Si es un tema con tu enlace con ARCA o tu suscripción, podes probar de enviar a re-procesar ese comprobante, usando el método de ["Reenviar a procesar, comprobante encolado con error"](web-services-afip-api-arca/reenvio-de-comprobantes-encolados-con-error.md)

***

#### Estados de las ventas que esperan ser emitidas

Si consultamos por external\_reference un comprobante que todavía está en cola (aún no emitido), ¿aparece en la respuesta? ¿Qué valores puede tener status, y cuáles son definitivos?&#x20;

Conocé todos los [estados disponibles](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-consulta-de-comprobantes#campos-devueltos-que-no-forman-parte-del-json-que-vos-envias) desde aquí.

***

#### Consulta por external\_reference en ventas instantáneas: ¿Funciona también para comprobantes emitidos con el método instantáneo, o solo con el asincrónico?

La external reference solo se guarda para ventas asincrónicas, asi se especifica en la [referencia API](https://developers.tusfacturas.app/api-factura-electronica-afip-facturacion-ventas/referencia-api-afip-arca)

***

#### Tiempo en cola y fecha: ¿cuánto suele tardar un comprobante desde que se encola hasta que se emite?&#x20;

No hay un tiempo estimado, es una cola de procesamiento para todos los clientes.&#x20;

***

#### Si ARCA está caído, ¿la cola reintenta sola? ¿Hasta cuándo, antes de pasar a error?&#x20;

Si, se reintenta hasta 100 veces, salvo que sea un error irrecuperable y en ese caso queda marcada con error de manera inmediata.

***

#### Si un comprobante encolado con la fecha de hoy se procesa recién al día siguiente, ¿con qué fecha se emite?

La factura se emite siempre con la fecha original

***

### Validación del total: si el total que enviamos no coincide con el que recalculan ustedes, ¿rechazan el comprobante o lo emiten con su cálculo?&#x20;

El comprobante se rechaza inmediatamente y no se incorpora a la cola de procesamiento.

***

### ¿Como manejan el redondeo?

Nuestra plataforma gestiona los precios unitarios de productos y servicios con 3 decimales, mientras que los totales se calculan con 2 decimales. Debido a esto, pueden surgir pequeñas diferencias de facturación en aquellas empresas que trabajan con precios finales (IVA incluido).

Para garantizar la precisión fiscal, aplicamos el método de redondeo "Round half even" (redondeo bancario), siguiendo estrictamente los lineamientos de ARCA.

En el siguiente artículo sobre [ajustes, redondeos y precios sin IVA](https://ayuda.tusfacturas.app/es/articles/12548047-redondeos-ajustes-y-precios-sin-iva) te explicamos cómo funciona mediante un ejemplo práctico.

***

#### Consulta de un comprobante ya enviado: Si una emisión se corta por timeout y no recibimos respuesta, ¿cómo podemos saber si se autorizó? ¿Se puede buscar un comprobante por el external\_reference que enviamos?&#x20;

Si se corta de tu lado por timeout, podes hacer una [consulta avanzada por external reference](web-services-afip-api-arca/consulta-avanzada-por-external-reference.md) para ver el estado de la misma.

***

#### ¿Se puede consultar el último número autorizado de un punto de venta y tipo de comprobante?

Si, podes usar el método de [consulta de numeración](web-services-afip-api-arca/api-factura-electronica-afip-consultar-numeracion-de-comprobantes..md)

***

#### Envíos duplicados: si mandamos dos veces la misma solicitud con el mismo external\_reference, ¿emiten dos comprobantes o rechazan el segundo? TF: El external\_reference debe ser único en tu sistema.&#x20;

TusFacturasAPP no valida su unicidad y, dado que existen distintos flujos de trabajo según cada empresa, si envias el mismo external\_reference más de una vez, la plataforma procesará cada solicitud sin realizar esta validación.

***

#### Totales: ¿el total del comprobante es el que enviamos o lo recalculan desde los ítems?&#x20;

Se valida lo que vos envias con el recalculo de la informacion.

***

Desglose de IVA: ¿la respuesta de una emisión autorizada trae el neto y el IVA por alícuota (21 %, 10,5 %) tal como se informaron a ARCA?

No. La respuesta que te enviamos es como en muestra en el [ejemplo de consulta simple](api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-consulta-de-comprobantes.md#ejemplo-del-json-de-respuesta)

***

#### Timeouts: ¿qué tiempo máximo de respuesta recomiendan esperar en una emisión?

Sugerimos un máximo de 90 segundos.&#x20;

***

### ARCA fuera de servicio: si ARCA no responde, ¿rechazan la solicitud, la encolan o tienen algún mecanismo de contingencia?

En el método asincrónico no importa el estado de los servicios de ARCA. Si los servicios de ARCA están caidos cuando se intenta facturar, se reintenta.

***

#### Alta en ARCA: ¿qué tiene que configurar el contribuyente en ARCA para emitir a través de ustedes

{% content-ref url="como-paso-a-produccion.md" %}
[como-paso-a-produccion.md](como-paso-a-produccion.md)
{% endcontent-ref %}

***

#### El sistema lo usan varios comercios. ¿Una cuenta puede emitir para varios CUIT o se necesita una cuenta por contribuyente? ¿Cómo cambia el costo?

Eso depende de tu negocio y tu estrategia comercial. Para más info, accede al artíoculo en nuestro centro de ayuda:  [Conviene espacios de trabajo separados vs único](https://ayuda.tusfacturas.app/es/articles/11839614-gestion-de-multiples-clientes-conviene-espacios-de-trabajo-separados-vs-unico)<br>

***

### ¿Hay algún ambiente que vaya contra la homologación de ARCA, o la cuenta de pruebas es solo simulada?

No ofrecemos el servicio de pruebas contra el entorno de homologación de ARCA. Las pruebas que realices bajo el plan de suscripción gratuito API DEV no te permiten conectar con el organismo, por lo que obtenes la misma respuesta que en producción, solo que no obtenes el CAE, QR y fecha de vencimiento del CAE, asi como tampoco las validaciones que el organismo realiza.

***

#### PDF: ¿por cuánto tiempo se puede volver a descargar el PDF de un comprobante ya emitido?

Mientras tengas la suscripción abonada y vigente al dia de la consulta. Las URLS de descarga son temporales, debes descargar elmarca

&#x20;PDF a tu plataforma, ya que no actuamos como CDN.

***

### ¿Es marca blanca?

No. TusFacturasAPP no es marca blanca.

***

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
