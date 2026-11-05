---
description: >-
  Qué son WSAA y WSFEv1, cómo se obtiene el CAE y qué resuelve la API REST de
  TusFacturasAPP para que no tengas que integrar SOAP, certificados ni tokens de
  ARCA.
tagTitle: 'Web services de ARCA: WSAA y WSFEv1 | TusFacturasAPP'
---

# FAQs | Web services ARCA

Para emitir comprobantes electrónicos con validez fiscal en Argentina, todo sistema tiene que comunicarse con los web services de ARCA (ex AFIP). Esa integración se puede hacer directamente o a través de una API intermediaria como la de TusFacturasAPP. En esta página te explicamos cómo funciona la conexión con ARCA por dentro y qué partes del proceso maneja la API para que tu sistema solo tenga que enviar un JSON.

### Cómo funciona la integración directa con ARCA

Una integración directa con ARCA tiene dos etapas.

#### 1. Autenticación: WSAA

El **WSAA** (Web Service de Autenticación y Autorización) es la puerta de entrada. Para usarlo, tu sistema necesita:

* Un **certificado digital** asociado al CUIT, generado a partir de un pedido de certificado (CSR) y una clave privada.
* Firmar un pedido de acceso con ese certificado y enviarlo al WSAA.
* Recibir un **Ticket de Acceso (TA)** con un token y una firma, que tiene vencimiento y hay que renovar periódicamente.

Sin un TA vigente, ARCA rechaza cualquier pedido a los servicios de negocio.

#### 2. Emisión: WSFEv1

Con el TA, el sistema llama al servicio que corresponde al tipo de comprobante. El más usado es el **WSFEv1**, que autoriza facturas, notas de crédito y notas de débito A, B, C y M, y la factura de crédito electrónica MiPyME. Este servicio recibe los importes totales del comprobante, no el detalle de los ítems.

El flujo típico es:

1. Consultar el último número autorizado para ese punto de venta y tipo de comprobante.
2. Armar el pedido con el número siguiente, fecha, importes, alícuotas de IVA y tributos.
3. Enviarlo y recibir la respuesta: si ARCA lo aprueba, devuelve el **CAE** y su fecha de vencimiento. Si lo rechaza, devuelve los errores u observaciones.

Para los comprobantes de exportación (factura E) ARCA usa un web service separado, con su propia estructura de datos.

#### Homologación y producción

ARCA tiene dos entornos con certificados distintos: **homologación**, para pruebas sin validez fiscal, y **producción**. Una integración propia tiene que gestionar ambos, con sus certificados, URLs y puntos de venta.

### Qué resuelve la API Rest de TusFacturasAPP

Integrar los web services de ARCA de forma directa implica trabajar con SOAP y XML, manejar certificados y claves, renovar tickets de acceso, controlar la numeración y traducir los códigos de respuesta. Con la API REST de TusFacturasAPP, todo eso queda del lado de la plataforma:

| Tarea                                         | Integración directa con ARCA                     | API de TusFacturasAPP                             |
| --------------------------------------------- | ------------------------------------------------ | ------------------------------------------------- |
| Formato de comunicación                       | SOAP / XML                                       | REST / JSON                                       |
| Autenticación WSAA y renovación del TA        | A cargo de tu sistema                            | Automática                                        |
| Certificado digital                           | Lo generas y lo administras vos                  | Se gestiona desde la plataforma                   |
| Numeración de comprobantes                    | Consultas el último número antes de cada emisión | Automática y validada contra ARCA                 |
| Elección del web service según el comprobante | A cargo de tu sistema                            | Automática                                        |
| PDF con QR y envío al cliente                 | Lo desarrollas vos                               | Incluido                                          |
| Cambios en los web services de ARCA           | Tenes que actualizar tu integración              | Los absorbe la plataforma siempre que sea posible |

Tu sistema envía los datos del comprobante en JSON y recibe el CAE, el número asignado y el PDF. Podes trabajar en modo sincrónico, con respuesta inmediata, o asincrónico, con una cola de procesamiento y notificación por webhook cuando el comprobante queda emitido.

### Antes de empezar a integrar

* **Enlaza tu CUIT con ARCA** desde la plataforma. Es el paso que autoriza a TusFacturasAPP a operar los web services en nombre de tu CUIT. Seguí el [instructivo de enlace con ARCA](https://www.tusfacturas.app/enlace-arca.html).
* **Creá un punto de venta habilitado para web services** en ARCA. Los puntos de venta de "Comprobantes en línea" no sirven para emitir por API.
* **Respetá el orden cronológico:** una vez emitido un comprobante con una fecha, no podes emitir otro del mismo punto de venta y tipo con una fecha anterior.

### Preguntas frecuentes

**¿Qué es el WSFEv1 de ARCA?**\
Es el web service de factura electrónica que ARCA pone a disposición de los sistemas para autorizar comprobantes A, B, C y M. Recibe los totales del comprobante y devuelve el CAE.

**¿Necesito un certificado digital para usar la API?**\
El certificado es obligatorio para operar con los web services de ARCA, pero no tenes que integrarlo en tu código: se genera y se carga una sola vez desde TusFacturasAPP durante el enlace con ARCA.

**¿Puedo probar la integración sin emitir comprobantes reales?**\
Sí. Podes probar la API antes de pasar a producción, sin que los comprobantes tengan validez fiscal.

**¿Qué pasa si ARCA no está disponible?**\
En modo sincrónico la respuesta depende de que los servicios de ARCA estén funcionando. En modo asincrónico el comprobante queda en cola y se procesa cuando el servicio vuelve a responder.

**¿Qué lenguajes de programación puedo usar?**\
Cualquiera que pueda hacer pedidos HTTP y trabajar con JSON. Para PHP hay un SDK disponible.

***
