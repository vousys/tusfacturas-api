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

#### Cuándo y qué se emite

La cola de procesamiento intentará emitir en el transcurso del día , todos aquellos comprobantes que se encuentren:

* En cola
* Sin errores
* Que hayan intentado emitirse menos de 100 veces
* Y cuya fecha del comprobante, sea menor o igual a la del dia

#### ¿Donde puedo ver el listado de las ventas que tengo en cola de procesamiento?

Dentro de nuestra plataforma web >  menú > Facturación > Ventas en cola

#### ¿Qué acciones que puedo realizar sobre un comprobante en cola?

Podes realizar las siguientes operaciones:

* [Enviarlos a reprocesar](api-factura-electronica-afip-facturacion-ventas/re-enviar-a-procesar-ventas-afip-asincronicas-con-error.md). Una vez que un comprobante fue marcado con errores, no se intentará emitir nuevamente, salvo que lo envies a reprocesar.
* Puedes [eliminarlo](api-factura-electronica-afip-facturacion-ventas/eliminar-comprobantes-encolados.md), en caso que no se pueda procesar.
* Modificar la [fecha del comprobante](api-factura-electronica-afip-facturacion-ventas/cambiar-fecha-a-comprobante-encolado.md) y automáticamente [enviarlos a reprocesar](api-factura-electronica-afip-facturacion-ventas/re-enviar-a-procesar-ventas-afip-asincronicas-con-error.md).&#x20;

#### ¿Qué comprobantes no pueden enviarse a la cola de procesamiento?

* Pedidos, Remitos, presupuestos, órdenes de compra
* Comprobantes de exportación
* Comprobantes relacionados con remitos y/o pedidos, ya sea porque incluyes remitos o pedidos o porque intentas facturar un remito o pedido.
* Comprobantes de tipo "NO VÁLIDO EN AFIP"

#### ¿Qué sucede si pasó +1 día y los comprobantes no se pudieron emitir?

Los comprobantes permanecerán en la cola de procesamiento hasta tanto los elimines o bien cambies la fecha de emisión y se intenten emitir nuevamente

#### ¿Qué sucede una vez que el comprobante se emite?

Los comprobantes que se han podido emitir, pasan automáticamente al reporte de Mis Ventas, desapareciendo del listado de "ventas en cola"

#### Si un request es aceptado para su procesamiento, y se detectan errores, se vuelve a enviar automáticamente a procesar?

Solo se vuelve a enviar automáticamente a procesar, si el error obtenido, se debe a caídas del servicio de facturación de AFIP.

#### Si tengo comprobantes en cola de procesamiento, y quiero enviar un nuevo request en cola, ya sea por lotes o individual, se puede?

Si, se puede, siempre y cuando cumpla con los requisitos mencionados para ser procesado.

#### Si tengo comprobantes en cola de procesamiento, y quiero enviar un nuevo request pero que sea en la modalidad instantánea, se puede?

No, no se puede. Recibirás un error instantáneo, informandote que existen comprobantes en cola y que solo podrás enviarlos bajo esa modalidad.&#x20;

#### En el hook que recibo, obtengo todos los datos del comprobante?

No. El hook te envia el estado de ese request y el mensaje de error, en caso que no se haya podido procesar.&#x20;

En caso de éxito, deberás realizar una  [consulta avanzada por external\_reference](api-factura-electronica-afip-facturacion-ventas/consulta-avanzada-de-comprobantes-enviados.md#como-realizar-una-consulta-avanzada-por-external-reference),  para obtener los datos generados de éste comprobante

#### ¿Hay una reducción de tiempo considerable al emitir los comprobantes de esta forma

Optimizas, porque lo podes dejar programado con anterioridad, podes mandar el lote el dia 5 e indicar que esos comprobantes se emitan el dia 29; además tu proceso no se trabaria esperando la respuesta de la factura como si la mandaras instantánea. Sigue con las siguientes y a medida q va procesando te va notificando.

#### ¿Qué sucede si los servicios de AFIP no se encuentran funcionando, puedo enviar requests?

Si, está especialmente desarrollado para éstos casos. Los requests que envíes, se guardarán en la cola de procesamiento y serán enviados a medida que los servicios de AFIP se restauren.

#### ¿Qué sucede si los servicios de AFIP no se encuentran funcionando y tengo comprobantes en cola?

Los comprobantes seguirán en la cola y se emitirán cuando los servicios de AFIP se encuentren funcionando, siempre y cuando la fecha de éstos comprobantes sea menor o igual a la del día.

#### ¿Puedo enviar requests con fecha posterior a hoy?

Si, podes enviarlos y quedarán en la cola de procesamiento hasta la fecha indicada en el comprobante.

#### ¿Puedo cambiar la fecha de un request que se encuentra en la cola de procesamiento

Si, para eso debés utilizar el método de:  [Cambiar fecha encolado](api-factura-electronica-afip-facturacion-ventas/cambiar-fecha-a-comprobante-encolado.md)



#### ¿Puedo eliminar requests que aún no se han procesado?

Si, para eso debés utilizar el método de:  [Eliminar comprobante encolado](api-factura-electronica-afip-facturacion-ventas/eliminar-comprobantes-encolados.md)



**Si creo un abono desde la API o desde la plataforma web, ¿Cada vez que se emita la factura, me notifica por webhook?**

No. La plataforma en ese caso no te notifica por webhook. Si llegas a necesitar ésta funcionalidad, por favor contactanos.



**Si se intentó emitir 100 veces un comprobante en cola, ¿En qué momento recibo un webhook con el error?**

Recibís un webhook de error cuando se alcance el máximo de intentos definidos.&#x20;



**¿Qué debo hacer si un comprobante superó el límite de reintentos?**

Debes solucionar el inconveniente y probar de enviar a re-procesar ese comprobante, usando el método de ["Reenviar a procesar, comprobante encolado con error"](api-factura-electronica-afip-facturacion-ventas/re-enviar-a-procesar-ventas-afip-asincronicas-con-error.md)



**Si envío un lote de comprobantes, ¿Cómo recibo los hooks?**

Siempre vas a recibir los hooks independientes por cada comprobante.



**¿Tenes más dudas?** Contactanos por el chat de la web [www.tusfacturas.app](https://www.tusfacturas.app)
