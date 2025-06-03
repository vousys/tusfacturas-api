---
description: >-
  Conocé que datos necesitas para poder integrar en tu software con la API para
  AFIP -  facturación electrónica Argentina provista por TusFacturasAPP
---

# Autenticación

{% hint style="info" %}
**¿Cómo obtener mis credenciales de acceso?**

Una vez creada tu cuenta y teniendo habilitado un plan API, accedé a nuestra plataforma web www.tusfacturas.app > menú > Mi espacio de trabajo > Puntos de venta  y desde ahi, podrás obtener las keys requeridos para poder operar en cada uno de los métodos que tenemos disponibles.
{% endhint %}

### **¿Qué datos necesito para enviar un request a la API de TusFacturasAPP?**

Para cada solicitud o consulta que realices a nuestra **API de facturación electrónica**, es **obligatorio** que incluyas información clave relacionada con tu **Punto de Venta**. Esta información es esencial para autenticar tus operaciones y garantizar la seguridad de tus datos.

**¿Cómo obtener las credenciales API requeridas (API Key y API Token)?**

Acceder a tus credenciales es muy simple desde nuestra plataforma web:

1. Ingresá a tu cuenta en TusFacturasAPP.
2. Dirigite a **Menú > Mi Espacio de Trabajo > Puntos de Venta**.

Desde allí, podrás gestionar y obtener las claves API (API Key y API Token) necesarias para tus integraciones. Recordá que todos los planes API de TusFacturasAPP cuentan con estas herramientas disponibles una vez que hayas dado de alta tu punto de venta.

**Más información:** Para un tutorial completo sobre cómo obtener tu API Key y API Token y comenzar a probar nuestra API de facturación electrónica, visitá nuestro centro de ayuda: [https://ayuda.tusfacturas.app/es/articles/11503635-como-obtener-api-key-y-api-token-para-probar-la-api](https://ayuda.tusfacturas.app/es/articles/11503635-como-obtener-api-key-y-api-token-para-probar-la-api)

| `apitoken`  | <p>Valor alfanumerico<br><strong>Ejemplo:</strong> </p><p><strong>xxxxxxxx</strong></p>    |
| ----------- | ------------------------------------------------------------------------------------------ |
| `apikey`    | <p>Valor númerico</p><p><strong>Ejemplo:  1134</strong></p>                                |
| `usertoken` | <p>Valor alfanumerico<br><strong>Ejemplo:</strong> </p><p><strong>xxxxxxx</strong><br></p> |

## Requerimientos <a href="#errores-http" id="errores-http"></a>

SSL: **requiere TLS 1.2+**\
Tipo de datos entrada y respuesta: **JSON**\
Charset: **UTF-8**\
Tipo de request : **POST**

## Errores HTTP <a href="#errores-http" id="errores-http"></a>

Errores de HTTP comunes que puede devolver :\
401, 403: El acceso ha sido denegado\
404: El recurso no existe\
400: Entrada de datos invalida (query string, post, etc)\
405: Método no permitido



### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
