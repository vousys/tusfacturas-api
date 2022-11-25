---
description: El paso a paso para comenzar a integrar TusFacturasAPP, con tu plataforma.
---

# ¿Cómo empiezo?

## Aprendé cómo integrar tu sistema con la API de TusFacturasAPP

Para probar la integración con la API, debes [crear una cuenta](https://www.tusfacturas.app/registrarme-factura-electronica.html) en nuestra plataforma [desde aquí](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).

Luego de creada la cuenta y por cuestiones de seguridad, contáctanos a hola@tusfacturas.app, **desde la casilla con la cual te registraste** y te brindamos el plan API DEV, para que puedas emitir hasta 150 comprobantes _que no son de curso legal_, por 1 mes y sin costo (solo para nuevas cuentas y por única vez). Una vez vencido tu período de prueba, deberás contratar algún [plan API](https://www.tusfacturas.app/tarifas-tusfacturas-planes-api-factura-electronica.html) de los que tenemos disponibles [aquí.](https://www.tusfacturas.app/tarifas-tusfacturas-planes-api-factura-electronica.html)

Por cuestiones legales, nuestra plataforma **no cuenta con un ambiente de testing**, por lo que no podrás enlazar con AFIP tu CUIT, mientras realizas las pruebas, evitando problemas con el fisco, dado que los comprobantes emitidos no pueden ser modificados ni eliminados.

Mientras estés en testing, la respuesta que recibirás desde nuestra API, es la misma que si facturas contra AFIP, solo que los campos CAE y vencimiento del CAE, te retornarán vacíos y no contarás con las validaciones adicionales que AFIP realiza.

Te sugerimos revisar nuestros [términos y condiciones](https://www.tusfacturas.app/terminos-y-condiciones.html), para estar al tanto de lo que podés y no podés realizar en nuestra plataforma.

Mientras estés en etapa de testing, te sugerimos configurar tu CUIT, con un punto de venta (PDV) irreal (Ej: 679). Una vez que hayas probado todo, eliminas desde nuestra plataforma web, todos los comprobantes asociados a ese CUIT + PDV y luego das de baja el CUIT+PDV para crear el nuevo y enlazarlo con AFIP.

**Resumen de pasos, para comenzar a trabajar:**

1\) Crea tu cuenta API DEV [desde aquí](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html), gratis por 1 mes.

2\) Configura tu CUIT/Punto de venta (PDV) desde nuestra plataforma web [www.tusfacturas.app](https://www.tusfacturas.app/app/login.html), ingresando a  menú > "Mi espacio de trabajo > Cuits/PDV.  Una vez creado el CUIT/PDV, obtendrás las keys requeridas para iniciar tu integración.

3\) En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a hola@tusfacturas.app o contactanos por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).

4\) Una vez activa tu cuenta con el plan API DEV, ingresá desde nuestra la web [www.tusfacturas.app](https://www.tusfacturas.app/app/login.html) a  menú > "Mi espacio de trabajo > Configurar éste espacio de trabajo y habilita tu IP dentro del bloque "ACCESO API".
