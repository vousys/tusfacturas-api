---
description: >-
  Qué son WSAA y WSFEv1, cuándo conviene integrarlos directo y qué verificar
  antes de elegir una API intermediaria para facturar en ARCA.
tagTitle: 'Web services de ARCA: WSAA y WSFEv1 | TusFacturasAPP'
---

# Integrar ARCA: directo o con una API

Para emitir comprobantes electrónicos con validez fiscal en Argentina, todo sistema tiene que comunicarse con los web services de ARCA (ex AFIP). Esa integración se puede hacer directamente o a través de una API intermediaria como la de TusFacturasAPP. En esta página te explicamos cómo funciona la conexión con ARCA por dentro y qué partes del proceso maneja la API para que tu sistema solo tenga que enviar un JSON.

TusFacturasAPP es una plataforma privada e independiente de facturación y gestión, que no pertenece ni está vinculada a ARCA (ex AFIP) ni a ningún organismo público. La emisión de comprobantes se realiza mediante los servicios web oficiales de ARCA, utilizando el CUIT que cada usuario configura y habilita.

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

#### ¿Cuándo conviene integrar ARCA directo?

Integrar WSAA y WSFEv1 por tu cuenta tiene sentido si:

* Tenes un equipo que puede mantener una integración SOAP y seguir cada cambio de ARCA.
* Emitís un volumen tan alto que el costo por comprobante de un intermediario supera el costo de mantenerla.
* Solo necesitas el CAE y vas a generar vos el PDF, el QR, el envío por email y los reportes.

Una API intermediaria conviene cuando queres salir a producción en días en lugar de semanas, no querés manejar certificados ni tickets de acceso, o necesitas más que el CAE: PDF, recibos, cuentas corrientes, padrones provinciales.

#### Qué verificar antes de elegir una API para ARCA

Una API intermediaria opera con tu CUIT y tus datos fiscales. Antes de elegirla, revisa estos puntos:

| Qué verificar               | Por qué importa                                                                      | TusFacturasAPP                                   |
| --------------------------- | ------------------------------------------------------------------------------------ | ------------------------------------------------ |
| Empresa identificable       | Si hay un problema con un comprobante, necesitas saber a quién reclamar              | VYAR S.R.L., CUIT 30-71625243-0                  |
| Marca registrada            | Indica que hay una empresa que invierte en el producto a largo plazo                 | Marca registrada en INPI, registro N° 3.480.509  |
| Años en funcionamiento      | ARCA cambia normativas seguido; un proveedor con historia ya atravesó varios cambios | Desde 2015                                       |
| Respaldo impositivo         | Los cambios de ARCA no son solo técnicos, también son fiscales                       | Respaldo continuo de un estudio impositivo       |
| Estado del servicio público | Para saber si el problema es tuyo, del proveedor o de ARCA                           | Endpoint de estado                               |
| Changelog público           | Muestra con qué frecuencia se actualiza ante cambios de ARCA                         | Changelog                                        |
| Modo asincrónico            | Si ARCA se cae, tu venta no se pierde                                                | Cola con reintento y webhook                     |
| Soporte con canal técnico   | Para resolver errores en la integración.                                             | Canal directo por e-mail con humanos.            |
| Prueba sin compromiso       | Para probar la integración antes de pagar                                            | Cuenta gratis renovable las veces que necesites. |

### Antes de empezar a integrar

* **Enlaza tu CUIT con ARCA** desde la plataforma. Es el paso que autoriza a TusFacturasAPP a operar los web services en nombre de tu CUIT. Seguí el [instructivo de enlace con ARCA](https://www.tusfacturas.app/enlace-arca.html).
* **Creá un punto de venta habilitado para web services** en ARCA. Los puntos de venta de "Comprobantes en línea" no sirven para emitir por API.
* **Respetá el orden cronológico:** una vez emitido un comprobante con una fecha, no podes emitir otro del mismo punto de venta y tipo con una fecha anterior.

### Preguntas frecuentes

**¿Quién está detrás de TusFacturasAPP?**\
VYAR S.R.L., CUIT 30-71625243-0, empresa argentina en producción desde 2015 y titular de la marca registrada TusFacturasAPP. Ver sobre [TusFacturasAPP](https://www.tusfacturas.app/quienes-hacemos-tusfacturas.html).

**¿Qué diferencia hay entre usar TusFacturasAPP y una librería de código abierto para WSFEv1?** \
Una librería te ahorra escribir el cliente SOAP, pero el certificado, el ticket de acceso, la numeración, el PDF y los cambios de ARCA siguen a tu cargo. Con TusFacturasAPP envias un JSON y todo eso queda del lado de la plataforma.

**¿TusFacturasAPP sirve para facturar desde un agente de IA?**\
Sí. La API es REST con JSON y un solo endpoint por operación, así que cualquier agente que pueda hacer pedidos HTTP la puede usar con la documentación de [llms.txt](https://developers.tusfacturas.app/llms.txt).

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
