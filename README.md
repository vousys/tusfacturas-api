---
description: >-
  Mediante nuestra API podrás conectar tu sistema de gestión actual, con nuestra
  plataforma y emitir facturas electrónicas AFIP válidas. Estamos homologados
  por AFIP
---

# Documentación de la API para Factura Electrónica AFIP

Ademas, podrás generar y consultar de manera segura, comprobantes de venta y de compra , como así también utilizar todas las funcionalidades que te brinda nuestra plataforma web. 

{% hint style="info" %}
Importante: Para utilizar la API debes estar [registrado](https://www.tusfacturas.com.ar/registrarme-factura-electronica.html). 

Mientras estés en etapa de testing, configurá tu CUIT con un punto de venta irreal \(Ej: 679\), y usa ese CUIT de prueba para facturar; la respuesta que recibirás es la misma que si facturas contra AFIP, solo que los campos CAE y Vencimiento del CAE te retornaran vacios. Una vez que hayas probado todos los métodos, crea el nuevo CUIT+punto de venta y lo enlazas con AFIP.

Ten en cuenta que al registrarte, te asignamos un plan gratuito que te permite emitir 5 comprobantes por mes y una vez vencido tu período de prueba, debes contratar algún [plan API](https://www.tusfacturas.com.ar/tarifas-factura-electronica.html) de los que tenemos disponibles [aquí](https://www.tusfacturas.com.ar/tarifas-factura-electronica.html) .

En caso que requieras 10 días más para el desarrollo, contáctanos a tusfacturas@vousys.com
{% endhint %}

  
En la documentación encontrarás algunos ejemplos para que luego los adaptes al lenguaje de tu sistema actual; Si bien no te podemos brindar soporte para los diferentes lenguajes de programación que existen en el mercado, al ser los input y los output en formato JSON, podes conectarlo el lenguaje que mas te guste, teniendo a mano stackoverflow por si tenes dudas ;\) 

  
Versión actual: **API v2**   
Tipo de API: **API Rest**  
Tipo de datos entrada y respuesta: **JSON**  
Charset: **UTF-8**  
Tipo de request : **POST**  
URL : **https://www.tusfacturas.com.ar/app/api/v2/estado\_servicios/alertas**  
Probá la API : **https://www.tusfacturas.com.ar/proba-la-api-factura-electronica-afip.html**



**Tené en cuenta éstas cosas:**  
1\) Para procesar correctamente los campos, debes enviarlos siempre encodeados con **UTF-8**.   
2\) Cuando realices comprobantes AFIP Factura electrónica válida, tené en cuenta que cada request que hagas para generar comprobantes, debe tener una diferencia de tiempo de 1 minuto, ya que sino la misma AFIP te bloquea el CUIT  y no podrás emitir comprobantes por unos minutos.   
3\) Nuestra API ya ha sido implementada contra sistemas que trabajan en PHP, Visual basic 6.0 y Ruby, como asi tambien entornos AMAZON WS, servidores dedicados y servidores compartidos. 

También podés probar las respuestas de la API, en nuestro API TESTER: [https://www.tusfacturas.com.ar/proba-la-api-factura-electronica-afip.html](https://www.tusfacturas.com.ar/proba-la-api-factura-electronica-afip.html)

{% hint style="info" %}
Podes descargarte nuestros [SDK](https://github.com/vousys/tusfacturas/) desde [GitHub](https://github.com/vousys/tusfacturas/)
{% endhint %}

