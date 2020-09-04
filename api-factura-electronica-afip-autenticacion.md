# Autenticación

{% hint style="info" %}
Poder utilizar la API debes estar [registradx](https://www.tusfacturas.com.ar/registrarme-factura-electronica.html). 

Mientras estés en etapa de testing, configurá tu CUIT con un punto de venta irreal \(Ej: 679\), y usa ese CUIT de prueba para facturar, la respuesta que recibirás es la misma que si facturas  contra AFIP, solo que los campos CAE y Vencimiento del CAE te retornaran vacios.  Una vez que hayas probado todos los métodos, crea el nuevo CUIT+punto de venta y lo enlazas con AFIP.

Ten en cuenta que al registrarte, te asignamos un plan gratuito que te permite emitir 5 comprobantes por mes y una vez vencido tu período de prueba, debes contratar algún [plan API](https://www.tusfacturas.com.ar/tarifas-factura-electronica.html) de los que tenemos disponibles [aquí](https://www.tusfacturas.com.ar/tarifas-factura-electronica.html) .En caso que requieras 10 días más para el desarrollo, contáctanos a tusfacturas@vousys.com 

Resúmen de pasos para comenzar a trabajar:

1\)  Crear tu cuenta [aquí](https://www.tusfacturas.app)

2\) Configurar tu CUIT + PDV

3\) Ir al menú  Mi espacio de trabajo &gt; Configurar éste espacio de trabajo y habilitar tu IP  
{% endhint %}

Una vez registrado, desde el menú "Mi Cuenta" -&gt; "Mis Cuits" podrás obtener los datos requeridos para poder consultar cada uno de los métodos que tenemos disponibles.

| `apitoken` | Token de tu cuenta **Ejemplo:d26b8fe8c8bf67c884e1405e26c03c85**  Obtenelo ingresando al menú "Mi Cuenta - Mis CUITS". Es un valor único generado automáticamente por nuestro sistema. |
| :--- | :--- |
| `apikey` | Código de empresa **Ejemplo:1134** Podes obtenerlo ingresando al menú "Mi Cuenta - Mis CUITS". |
| `usertoken` | Token del CUIT que va a facturar **Ejemplo:aa6b8fe8c8bf67c884e1405e26c03c85** Obtenelo ingresando al menú "Mi Cuenta - Mis CUITS" y entrando a consultar al registro en cuestión. Es un valor único generado automáticamente por nuestro sistema. |

## Errores HTTP <a id="errores-http"></a>

Errores de HTTP comunes que puede devolver :   
401, 403: El acceso ha sido denegado  
404: El recurso no existe  
400: Entrada de datos invalida \(query string, post, etc\)  
405: Método no permitido

