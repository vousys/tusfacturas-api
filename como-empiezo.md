---
description: El paso a paso para comenzar a integrar TusFacturasAPP, con tu plataforma.
---

# ¿Cómo empiezo?

## Aprende cómo integrar a tu software la API de facturación electrónica AFIP

Para probar la integración con la API para AFIP, debes crear una cuenta en nuestra plataforma [desde aquí](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html). Luego de creada la cuenta y con tu plan API DEV activo, podrás emitir hasta 1500 comprobantes que no son de curso legal por 1 mes y sin costo (solo para nuevas cuentas y por única vez). Una vez vencido tu período de prueba, deberás contratar algún plan API de los que tenemos disponibles aquí.

### Mientras estes en desarrollo:

* Por cuestiones legales, nuestra plataforma **no cuenta con un ambiente de testing**, por lo que **no podrás enlazar tu CUIT con AFIP mientras realizas las pruebas**, evitando problemas con el fisco, ya que los comprobantes emitidos en AFIP no pueden ser modificados ni eliminados; Sin embargo mientras estés en testing la respuesta que recibirás desde nuestra API es la misma que si lo harías en modo productivo impactando los comprobantes en AFIP, solo que los campos CAE y vencimiento del CAE retornaran vacio (tampoco contarás con las validaciones adicionales que AFIP realiza desde sus servicios).
* Sugerimos configurar tu CUIT personal con un punto de venta (PDV) irreal (Ej: 679).&#x20;
* Una vez que hayas probado todo y estes listo/a para ir a producción, podrás borrar desde nuestra plataforma web todos los comprobantes asociados a ese CUIT/PDV,  dar de baja el CUIT/PDV y crear el nuevo para ser enlazado con AFIP.

{% hint style="info" %}
Te sugerimos revisar nuestros [términos y condiciones](https://www.tusfacturas.app/terminos-y-condiciones.html) para estar al tanto de lo que podes realizar en nuestra plataforma y leer las [FAQs](faqs-or-preguntas-frecuentes.md) para despejar tus dudas.

En caso que necesites asistencia, podes [contactarnos](https://www.tusfacturas.app/contacto.html).
{% endhint %}

### **El paso a paso para comenzar:**

1\) Crea tu cuenta API DEV [desde aquí](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html), gratis por 1 mes. Si necesitas extenderlo porque no llegaste a finalizar el desarrollo, [contactanos](https://www.tusfacturas.app/contacto.html).

2\) Configura tu CUIT/Punto de venta (PDV) desde nuestra plataforma web [www.tusfacturas.app](https://www.tusfacturas.app/app/login.html), ingresando a  menú > "Mi espacio de trabajo > Cuits/PDV. &#x20;

Una vez creado el CUIT/PDV, podrás encontrar en la grilla las keys requeridas para iniciar tu integración.

3\) Habilitá la IP desde la cual vas a enviar requests. Ingresá a nuestra la web [www.tusfacturas.ap](https://www.tusfacturas.app/app/login.html), luego a  menú > Mi espacio de trabajo > Configurar éste espacio de trabajo y habilita tu IP dentro del bloque "ACCESO API".

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a hola@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).



¿Qué esperas para comenzar a [emitir factura electrónica AFIP](https://www.tusfacturas.app/como-empezamos-a-hacer-facturas-electronicas.html) con nuestra API?
