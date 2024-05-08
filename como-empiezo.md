---
description: El paso a paso para comenzar a integrar TusFacturasAPP, con tu plataforma.
---

# ¿Cómo empiezo?

## Aprende cómo integrar a tu software la API de facturación electrónica AFIP

Para probar la integración con la API para AFIP, debes crear una cuenta en nuestra plataforma [desde aquí](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).

Luego de creada la cuenta y con tu plan API DEV activo, podrás emitir hasta 1500 comprobantes _**que no son de curso legal**_** por 1 mes y sin costo** (solo para nuevas cuentas y por única vez). Una vez vencido tu período de prueba, deberás contratar algún [plan API](https://www.tusfacturas.app/tarifas-tusfacturas-planes-api-factura-electronica.html) de los que tenemos disponibles [aquí.](https://www.tusfacturas.app/tarifas-tusfacturas-planes-api-factura-electronica.html)

Por cuestiones legales, nuestra plataforma **no cuenta con un ambiente de testing**, por lo que no podrás enlazar tu CUIT con AFIP mientras realizas las pruebas, evitando problemas con el fisco, ya que los comprobantes emitidos en AFIP no pueden ser modificados ni eliminados.

Mientras estés en testing la respuesta que recibirás desde nuestra API es la misma que si lo harías en modo productivo impactando los comprobantes en AFIP, solo que los campos CAE y vencimiento del CAE retornaran vacios; Ademas no contarás con las validaciones adicionales que AFIP realiza desde sus servicios.

Te sugerimos revisar nuestros [términos y condiciones](https://www.tusfacturas.app/terminos-y-condiciones.html) para estar al tanto de lo que podés y no podes realizar en nuestra plataforma y leer las [FAQs](faqs-or-preguntas-frecuentes.md).

Mientras estés en etapa de testing:

* Sugerimos configurar tu CUIT personal con un punto de venta (PDV) irreal (Ej: 679).&#x20;
* Una vez que hayas probado todo y estes listo/a para ir a producción, podrás borrar desde nuestra plataforma web todos los comprobantes asociados a ese CUIT/PDV y luego dar de baja el CUIT/PDV para crear el nuevo y enlazarlo con AFIP.

### **Resumen para comenzar a trabajar:**

1\) Crea tu cuenta API DEV [desde aquí](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html), gratis por 1 mes.

2\) Configura tu CUIT/Punto de venta (PDV) desde nuestra plataforma web [www.tusfacturas.app](https://www.tusfacturas.app/app/login.html), ingresando a  menú > "Mi espacio de trabajo > Cuits/PDV.  Una vez creado el CUIT/PDV, desde la pantalla del listado obtendrás las keys requeridas para iniciar tu integración.

3\) En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a hola@tusfacturas.app o contactanos por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).

4\) Una vez activa tu cuenta con el plan API DEV, ingresá desde nuestra la web [www.tusfacturas.app](https://www.tusfacturas.app/app/login.html) a  menú > Mi espacio de trabajo > Configurar éste espacio de trabajo y habilita tu IP dentro del bloque "ACCESO API".

¿Qué esperas para comenzar a [emitir factura electrónica AFIP](https://www.tusfacturas.app/como-empezamos-a-hacer-facturas-electronicas.html) con nuestra API?
