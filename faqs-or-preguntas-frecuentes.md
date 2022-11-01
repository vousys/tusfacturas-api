---
description: Las respuestas a las preguntas más frecuentes
---

# FAQs | Preguntas generales

## Preguntas frecuentes sobre el servicio API

**Si no quiero que mis clientes ingresen a TusFacturasAPP, ¿Se puede utilizar igual?**

Si, se puede utilizar igual, ya que vos tendrías el usuario para acceder a la plataforma y no tus clientes. Deberías realizar o enviarle manualmente a cada cliente, el instructivo de enlace con AFIP, que te envia nuestra plataforma, de modo que toda factura que emitan sea de curso legal.

**¿Puedo generar el PDF desde mi plataforma?**

Si, podes generar el PDF desde tu plataforma, ya que TusFacturasAPP te envia en el retorno de la llamada a la API de nueva facturacion, el CAE, el vencimiento del CAE, y el texto necesario para armar el QR.

**¿Es muy tedioso de configurar?**

No, nuestra plataforma se caracteriza por ser muy simple de usar. Para comenzar a facturar tan solo debes hacer los siguientes pasos:

1. Das de alta en nuestra plataforma el CUIT+ PDV, completando la info obligatoria.
2. Haces el enlace con AFIP según el instructivo que se envía automáticamente desde la plataforma. Todo se hace online, no puede llevarte más de 10 mins, pero tenes que tener los datos de AFIP (CUIT y la clave fiscal), para poder entrar y hacerlo. TusFacturasAPP no gestiona ni administra datos de acceso al panel de AFIP de los clientes.

**¿Es un servicio de marca blanca?**

No, no es un servicio de marca blanca. Nuestra plataforma agrega por cuestiones legales al pie del PDF, una leyenda indicando que el comprobante fue emitido desde nuestra plataforma. También se menciona a TusFacturasAPP en los emails que se envían, con los comprobantes de venta que se emiten, y éstos son enviados desde nuestras casillas de email (vos configuras el from name y el reply to).

**¿Qué sucede si se cae AFIP, como se manejan los errores?**

Automáticamente se activan las alertas y recibís un error, porque impedimos la facturación para evitar inconsistencias. A veces pasa que el comprobante queda dando vueltas en AFIP, pero a nosotros no nos mandó nunca la respuesta, entonces el servicio te dice que debes enviar ese comprobante, con tales datos, que son los que impactaron en AFIP.

**Estoy integrando desde reactjs y obtengo un error de CORS.**

En ese caso, te sugerimos que tu frontend se comunique con tu backend y desde el backend realices la petición a nuestra API. También te sugerimos usar axios para el fetch

**¿AFIP me permite facturar con cualquier fecha?**

No. AFIP no te permite facturar con cualquier fecha.  Para CUITs cuyas actividades estén indicadas como  servicios, AFIP permitirá facturar con una anterioridad de hasta 10 días. Para CUITs cuyas actividades estén relacionadas a la comercialización de bienes, el plazo es de 5 días hacia atrás. Esto ademas aplica, contemplando que no hayas emitido previamente algun comprobante con fecha posterior a la que queres emitir.

Ej:&#x20;

Si  hoy es 20/10/2022 y queres emitir una factura con fecha 01/10/2022 AFIP te lo va a rechazar.

Si  hoy es 20/10/2022 y queres emitir una factura con fecha 18/10/2022, pero ya emitiste una con fecha 10/10/2022, AFIP te lo va a rechazar.

**¿Puedo eliminar o modificar un comprobante que impactó en AFIP?**

No. Aquellos comprobantes que impactaron en AFIP sólo pueden ser anulados contablemente, generando una nota de crédito.



