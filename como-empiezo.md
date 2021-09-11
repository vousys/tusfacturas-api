---
description: El paso a paso para iniciar con tu integración
---

# ¿Cómo empiezo?

Para probar la integración con la API, debes [crear una cuenta](https://www.tusfacturas.app/registrarme-factura-electronica.html) en nuestra plataforma [desde aquí](https://www.tusfacturas.app/registrarme-factura-electronica.html). 

Luego de creada la cuenta y por cuestiones de seguridad, contáctanos a hola@tusfacturas.app, **desde la casilla con la cual te registraste** \(debe ser una dirección de e-mail válida, la cual podamos validar y corroborar su existencia\) y te brindamos el plan API DEV, para que puedas emitir hasta 150 comprobantes _que no son de curso legal_, por 1 mes y sin costo \(solo para nuevas cuentas y por única vez\). Una vez vencido tu período de prueba, debes contratar algún [plan API](https://www.tusfacturas.com.ar/tarifas-factura-electronica.html) de los que tenemos disponibles [aquí](https://www.tusfacturas.com.ar/tarifas-factura-electronica.html). 

Por cuestiones legales, nuestra plataforma no cuenta con un ambiente de testing, por lo que no podrás enlazar con AFIP tu CUIT, mientras realizas las pruebas y de ésta manera evitarás problemas con el fisco, dado que los comprobantes emitidos no pueden ser modificados ni eliminados. La respuesta que recibirás desde nuestra API, es la misma que si facturas contra AFIP, solo que los campos CAE y vencimiento del CAE, te retornaran vacios y no contarás con las validaciones adicionales que el organismo realiza.

Te sugerimos revisar nuestros [términos y condiciones](https://www.tusfacturas.app/terminos-y-condiciones.html), para estar al tanto de lo que podés y no podés realizar en nuestra plataforma.

Mientras estés en etapa de testing, te sugierimos configurar tu CUIT, con un punto de venta \(PDV\) irreal \(Ej: 679\). Una vez que hayas probado todo, eliminás desde nuestra plataforma web, todos los comprobantes asociados a ese CUIT + PDV y luego das de baja el CUIT+PDV para crear el nuevo y enlazarlo con AFIP.  

Resumen de pasos, para comenzar a trabajar:

1\)  Crea tu cuenta [aquí](https://www.tusfacturas.app)

2\) Configura tu CUIT + PDV sin enlazarlo con AFIP. 

3\) Envianos un mensaje a hola@tusfacturas.app para solicitar el plan API DEV según requerimientos mencionados.

4\) Una vez activado el plan API DEV, accedé desde nuestra plataforma web, al menú  "Mi espacio de trabajo &gt; Configurar éste espacio de trabajo y habilitá tu IP  dentro del bloque "ACCESO API".

