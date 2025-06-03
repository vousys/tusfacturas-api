---
description: >-
  Integra la facturación electrónica AFIP fácil y rápido con nuestra API.
  ¡Confiable desde 2015! Elegida por todos los desarrolladores.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 📗 Documentación API Facturación AFIP/ARCA

<figure><img src="../.gitbook/assets/157.webp" alt="TusFacturasAPP API Factura Electronica AFIP. SDK AFIP"><figcaption></figcaption></figure>

Nuestra [API de facturación electrónica AFIP/ARCA](https://www.tusfacturas.app/api-factura-electronica-afip.html) te permite integrar la[ facturación electrónica AFIP/ARCA ](https://www.tusfacturas.app/factura-electronica-afip.html)directamente en tu plataforma, eliminando la necesidad de lidiar con los complejos webservices de AFIP/ARCA.  TusFacturasAPP es la solución SaaS ideal para tu negocio.

### ¿Cómo empezar con la API de facturación electrónica de TusFacturasAPP?

Integrar facturación electrónica en tu sistema nunca fue tan fácil.\
Sigue nuestra [**guía paso a paso sobre cómo empezar**](../como-empiezo/) para **crear una cuenta gratuita**, generar tus credenciales y comenzar a **emitir comprobantes electrónicos válidos ante AFIP/ARCA** desde tu software.

#### 🚀 Integra rápidamente la facturación electrónica en tu software

Con la **API de facturación electrónica de TusFacturasAPP**, podés conectar tu sistema a AFIP de manera ágil, segura y cumpliendo todas las normativas fiscales argentinas.

**✅ Características destacadas:**

* **Conexión rápida y segura** para emitir facturas electrónicas válidas ante **AFIP/ARCA**.
* **Automatiza la emisión de comprobantes**: facturas, notas de crédito, recibos y más, [directamente desde tu sistema de gestión](https://www.tusfacturas.app/como-integrar-mi-software-de-facturacion-con-afip.html), ERP o software a medida.
* **Documentación técnica completa** con ejemplos en formato JSON.
* **100% en regla con ARCA**: mantenemos la API actualizada con las últimas disposiciones fiscales, gracias al respaldo de un equipo contable-impositivo especializado.

> 💡 Empezá hoy mismo con nuestra API y simplificá la emisión de comprobantes electrónicos para tus clientes o tu empresa.

### Nuestras opciones de API para facturación electrónica AFIP/ARCA:&#x20;

* **Emisión individual o por lotes**: Selecciona la modalidad que mejor se adapte a tu volumen de facturación.
* **Procesamiento instantáneo o asincrónico**: Obtene respuestas inmediatas o gestiona tu flujo de trabajo con colas de procesamiento. T**e recomendamos** utilizar siempre que sea posible, los **métodos de facturación asincrónicos**, ya que los instantáneos dependen de cómo funcionen los servicios de AFIP/ARCA en el momento de la emisión.



<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>En éste método envías un solo request para ser procesado y  obtenes la respuesta mediante un <a href="webhooks-notificaciones.md">webhook</a> (no dependes del estado de los servicios de facturación de AFIP/ARCA). Conoce más sobre la <a href="api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md">facturación electrónica individual  asincrónica</a></td><td><strong>Endpoint</strong>: </td><td>https://www.tusfacturas.app/app/api/v2/<mark style="color:purple;">facturacion/nuevo_encola</mark></td><td><a href="../.gitbook/assets/metodo-asinc-individual.webp">metodo-asinc-individual.webp</a></td><td><a href="api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md">api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md</a></td></tr><tr><td>Utilizando éste método envías un  request  y obtenes la respuesta al instante, sujeto al estado de los servicios AFIP/ARCA. Conoce más sobre la <a href="api-factura-electronica-afip-facturacion-nuevo-comprobante.md">facturación electrónica individual e instantánea</a></td><td><p>Endpoint: </p><p>https://www.tusfacturas.app/app/api/v2/<mark style="color:purple;">facturacion/nuevo</mark></p></td><td></td><td><a href="../.gitbook/assets/metodo-instantaneo-individual.webp">metodo-instantaneo-individual.webp</a></td><td><a href="api-factura-electronica-afip-facturacion-nuevo-comprobante.md">api-factura-electronica-afip-facturacion-nuevo-comprobante.md</a></td></tr><tr><td>Con éste método envías una cierta cantidad de requests para ser procesados y obtenes la respuesta al instante . Sujeto al estado de los servicios AFIP/ARCA. Conoce más sobre la <a href="api-factura-electronica-afip-api-facturacion-por-lotes.md#facturacioninstantaneaporlotes">facturación electrónica en lotes instantánea</a></td><td><p></p><p>Endpoint:</p></td><td>https://www.tusfacturas.app/app/api/v2/<mark style="color:purple;">facturacion/lotes</mark></td><td><a href="../.gitbook/assets/metodo-instantaneo-lote.webp">metodo-instantaneo-lote.webp</a></td><td></td></tr></tbody></table>

### 📌 ¿Qué comprobantes podes facturar con la API para AFIP/ARCA?

Nuestro servicio API de [facturación electrónica AFIP/ARCA ](https://www.tusfacturas.app/factura-electronica-afip.html)te permite enviar a facturar  comprobantes de tipo [A](../web-services-afip-api-arca/api-factura-electronica-afip-factura-a.md),[B](../web-services-afip-api-arca/api-factura-electronica-afip-factura-b.md),[C](../web-services-afip-api-arca/api-factura-electronica-afip-factura-c.md),[E](../web-services-afip-api-arca/api-factura-electronica-afip-factura-e.md), M y comprobantes de tipo "[Factura de crédito MiPyme](api-factura-electronica-afip-factura-de-credito-electronica-mipyme-fce.md)",  ya sean facturas, notas de crédito, notas de débito y hasta facturas-recibos.  ¿No sabes qué tipo de comprobante debes emitir? Consulta [desde aquí](que-tipos-de-comprobante-debo-puedo-emitir.md)

🧐 ¿Tenés alguna duda del servicio? checkea las [FAQs](../faqs-or-preguntas-frecuentes.md), y si no encontrás lo que buscabas, contactanos por los [canales de atención](https://www.tusfacturas.app/contacto.html) que tenemos disponibles.



### Explora la API AFIP/ARCA

Explora las funcionalidades de nuestra [API Rest para AFIP/ARCA](referencia-api-afip-arca.md) y descubrí cómo podes personalizarla para tus necesidades.&#x20;

{% content-ref url="referencia-api-afip-arca.md" %}
[referencia-api-afip-arca.md](referencia-api-afip-arca.md)
{% endcontent-ref %}





***

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).

