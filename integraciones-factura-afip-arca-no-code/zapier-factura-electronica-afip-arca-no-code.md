---
description: >-
  Automatiza tus facturas de AFIP/ARCA con Zapier y TusFacturasApp. Integración
  no-code para e-commerce y CRM.
---

# Zapier: Factura electrónica AFIP/ARCA No-Code

### Cómo Generar Facturas Electrónicas AFIP/ARCA con Zapier&#x20;

La **automatización de la facturación con herramientas no-code** permite crear **factura electronica AFIP/ARCA desde zapier** sin escribir código. Aprende a integrar TusFacturas.app con Zapier para automatizar completamente tu facturación electrónica.

> 🤝 Queremos que aproveches la posibilidad de usar Zapier, pero <mark style="color:purple;">**es importante que sepas que desde TusFacturasApp no podemos ofrecer soporte ni solucionar inconvenientes relacionados con estas plataformas externas.**</mark>

### ¿Cómo automatizas tu facturación con la integración a zapier?

* Generar facturas en AFIP/ARCA automáticamente cuando recibas pagos
* Conectar múltiples plataformas (Stripe, QuickBooks, etc.)
* Emitir facturas electrónicas AFIP/ARCA sin intervención manual
* Ahorrar horas de trabajo administrativo

#### Paso 1: Configurar tu Cuenta en TusFacturas.app

Para comenzar a automatizar la **facturación electronica AFIP/ARCA con herramientas no-code**, cómo lo es zapier, primero necesitas configurar tu cuenta en TusFacturasAPP:

1. Accede a [developers.tusfacturas.app](https://developers.tusfacturas.app/)
2. Sigue los pasos detallados en la sección **"**[**Cómo Empiezo**](../como-empiezo/)**"** de la documentación
3. Guarda tus credenciales de acceso - las necesitarás para integrar en Zapier

#### Paso 2: Crear tu Cuenta en Zapier

**2.1 Registrate en Zapier**

1. Accede a [zapier.com](https://zapier.com/)&#x20;
2. Hace clic en "Sign Up" y crea tu cuenta gratuita
3. Verifica tu email y crea tu primer "Zap"

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

**2.2 Entende los Conceptos Básicos de zapier**

* **Zap**: Tu automatización completa
* **Trigger**: Lo que inicia la automatización (ej: nuevo pago)
* **Action**: Lo que sucede después (ej: crear factura)

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

### Automatizar la facturación AFIP/ARCA con un webhook desde otra plataforma externa hacia TusFacturasAPP

A continuación te presentamos ejemplos de cómo automatizar tu facturación AFIP/ARCA y otra plataforma externa, usando herramientas no-code como Zapier.&#x20;

> 🤝 Queremos que aproveches la posibilidad de usar Zapier, pero <mark style="color:purple;">**es importante que sepas que desde TusFacturasApp no podemos ofrecer soporte ni solucionar inconvenientes relacionados con estas plataformas externas.**</mark>

**Configura el Zap**

Si tu plataforma externa puede enviar webhooks:

1. **App**: "Webhooks by Zapier"
2. **Trigger**: "Catch Hook"
3. **Action**: Selecciona "Utilities" > "Webhooks"

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

**Configura el trigger**

1. Zapier te dará una URL única.  Copia esa URL y configúrala en tu plataforma externa
2. Envia un hook a esa URL que te dio Zapier, con el contenido del JSON esperado por TusFacturasAPP de acuerdo a los [ejemplos de factura ](../web-services-afip-api-arca/)que te ofrecemos.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

**Configura el Action**:

1. Ingresa la URL en la que TusfacturasAPP recibirá tu facturacion. En este caso usamos la [facturación instántanea individual.](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md)
2. Selecciona el tipo de payload: "JSON"
3. Ingresa todos los campos esperados del JSON dentro del campo "data", segun los [ejemplos proporcionados por TusFacturasAPP](../web-services-afip-api-arca/)

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

Mapeo de datos desde tu plataforma.

&#x20;Para enviar datos desde otra plataforma, podes usar una solicitud a nuestra API que contenga la siguiente información:

```json
{
  "customer_name": "Juan Pérez",
  "customer_email": "juan@email.com",
  "customer_cuit": "20123456789",
  "amount": "1000.00",
  "description": "Servicio de consultoría",
  "invoice_date": "2025-01-15"
}
```

y mapearlos de acuerdo a lo requerido en TusFacturasApp

```json
{
  ...
  "cliente": {
    ...
    "documento_nro": "[Webhook: customer_cuit]",
    "razon_social": "[Webhook: customer_name]",
    "email": "[Webhook: customer_email]",
    
  },
  "comprobante": {
    ...
    "fecha": "[Webhook: invoice_date]",
    "observaciones": "Generado automáticamente desde plataforma externa en zapier"
  },
  "detalle": [
    ...
    {
      ...
      "producto": {
        ...
        "descripcion": "[Webhook: description]",
        "precio_unitario": "[Webhook: amount]",
      }
    }
  ]
}
```

**Probar y Activar tu Zap**

Luego de configurados los ejemplos, debes probar la Integración que realizaste:

1. Hace clic en **"Test & Continue"**
2. Zapier enviará una prueba a TusFacturas.app
3. Verifica que aparezca "Success" o status 200
4. Revisa en tu panel de  TusFacturas.app (Menú > Facturación > Mis ventas) que se haya creado la factura

**Revisar Respuesta de la API**

Una respuesta exitosa de TusFacturasAPP se ve así:

```json
{
	"error": "N",
	"errores": [],
	"error_cod": [],
	"error_details": [],
	"external_reference": "",
	"requiere_fec": "NO",
	"observaciones": "",
	"rta": "El comprobante FACTURA B 00010-00000032 (PRUEBA) se ha guardado correctamente ",
	"cae": "xxx ",
	"vencimiento_cae": "13/08/2025",
	"vencimiento_pago": "12/09/2025",
	"comprobante_nro": "00010-00000032",
	"comprobante_tipo": "FACTURA B",
	"afip_codigo_barras": " ",
	"afip_qr": "xxx",
	"micrositios": {
		"descarga": "xxx",
		"cliente": "xxx"
	},
	"envio_x_mail": "N" 
	"comprobante_pdf_url": "xxx",
	"comprobante_ticket_url": "xxx"
}
```

**Activa el Zap**

1. Dale un nombre a tu Zap, como por ejemplo: "Integracion a TusFacturasAPP - Facturación Automática"
2. Hace clic en **"Turn on Zap"**
3. ¡Tu automatización ya está funcionando en Zapier!

### Ejemplo de como automatizar la facturación AFIP/ARCA con Stripe y TusFacturasAPP

A continuación te presentamos ejemplos de cómo automatizar tu facturación AFIP/ARCA  dsde Stripe usando herramientas no-code como Zapier.&#x20;

Sugerimos revisar la documentación oficial de [Stripe](https://stripe.partners/directory/zapier) y [Zapier](https://zapier.com/apps/stripe/integrations) antes de comenzar.

> 🤝 Queremos que aproveches la posibilidad de usar Zapier, pero <mark style="color:purple;">**es importante que sepas que desde TusFacturasApp no podemos ofrecer soporte ni solucionar inconvenientes relacionados con estas plataformas externas.**</mark>

#### Paso 1: Configurar el Trigger - Nuevo Pago en Stripe

1. En Zapier, hace clic en **"Create Zap"**
2. Busca y selecciona **"Stripe"**
3. Selecciona el trigger **"New Payment"**
4. Hace clic en **"Continue"**
5. Conecta tu cuenta de Stripe:
   * Hace clic en "Sign in to Stripe"
   * Autoriza la conexión
   * Selecciona tu cuenta
6.  Configura la manera de autenticarte

    Hace clic en "API Key"
7. **Configurar el trigger**:
   * En "Set up trigger", deja las opciones por defecto
   * Hace clic en **"Continue"**
8. **Probar el trigger**:
   * Zapier buscará pagos recientes
   * Selecciona un pago de ejemplo
   * Hace clic en **"Continue"**

#### Paso 2:  Configurar la Acción - Crear Factura en TusFacturas.app

1. Hace clic en **"Choose App & Event"**
2. Busca **"Webhooks by Zapier"**
3. Selecciona **"POST"**
4. Hace clic en **"Continue"**

#### Paso 3: Configurar la Llamada a la API

A continuación te mostramos como usar la [facturación instantánea e individual en ARCA](../api-factura-electronica-afip-facturacion-ventas/api-factura-electronica-afip-facturacion-nuevo-comprobante.md).

**URL**:

```
https://www.tusfacturas.app/app/api/v2/facturacion/nuevo
```

**Method**: POST

**Headers**:

```
Content-Type: application/json
```

#### Paso 4: Mapear los Datos del Body&#x20;

En el campo **"Data"**, configura estos campos según la [API de TusFacturas.app](../api-factura-electronica-afip-facturacion-ventas/referencia-api-afip-arca.md#json-de-ejemplo-para-emitir-comprobantes-electronicos). &#x20;

Para automatizar la creación de facturas, puedes copiar un ejemplo de los modelos de  [factura B](../web-services-afip-api-arca/api-factura-electronica-afip-factura-b.md), [factura A](../web-services-afip-api-arca/api-factura-electronica-afip-factura-a.md) , [Factura C](../web-services-afip-api-arca/api-factura-electronica-afip-factura-c.md), y sustituir los siguientes campos con la información que obtengas de la API de Stripe. Para una lista completa de los datos disponibles, consulta la [documentación de Stripe](https://stripe.com/docs)

```json
{
  "cliente": {
     ...
    "documento_nro": "[Usar dato de Stripe: Tax ID]",
    "razon_social": "[Usar dato de Stripe: Customer Name]",
    "email": "[Usar dato de Stripe: Customer Email]",
    "domicilio": "[Usar dato de Stripe: Customer address]",
    
  },
  "comprobante": {
    ...
    "fecha": "[Usar dato de Stripe: Created Date - formato esperado: dd/mm/yyyy]",
    "observaciones": "Pago procesado via Stripe"
  },
  "detalle": [
    ...
    {
      "cantidad": "1",
      "producto": {
        ...
        "descripcion": "[Usar dato de Stripe: Description]",
        "precio_unitario": "[Usar dato de Stripe: Amount / 100]",
         
      }
    }
  ]
}
```

#### Paso 5: Configuración Visual en Zapier

**Para mapear los campos de Stripe:**

1. **Customer Name**: Busca en la lista desplegable "Stripe Customer Name" o "Billing Details Name"
2. **Customer Email**: Selecciona "Stripe Customer Email"
3. **Amount**: Selecciona "Stripe Amount" (se divide automáticamente por 100)
4. **Description**: Usa "Stripe Description" o "Metadata Description"
5. **Created Date**: Selecciona "Stripe Created" y aplica formato de fecha dd/mm/aaaa

### Automatizar la facturación AFIP/ARCA con QuickBooks y TusFacturasAPP

A continuación te presentamos ejemplos de cómo automatizar tu facturación AFIP/ARCA y Quickbooks, usando herramientas no-code como Zapier.&#x20;

Sugerimos revisar la documentación oficial de [QuickBooks](https://quickbooks.intuit.com/app/apps/appdetails/zapier/en-us/) y [Zapier](https://zapier.com/apps/quickbooks/integrations) antes de comenzar.

> 🤝 Queremos que aproveches la posibilidad de usar Zapier, pero <mark style="color:purple;">**es importante que sepas que desde TusFacturasApp no podemos ofrecer soporte ni solucionar inconvenientes relacionados con estas plataformas externas.**</mark>

**Crea un Trigger para una nueva Factura en QuickBooks**

1. **App**: QuickBooks Online
2. **Trigger**: "New Invoice"
3. **Configuración**: Conecta tu cuenta de QuickBooks

**Configura el Action: Crear Factura en TusFacturas.app**

Usa la misma configuración de Webhook pero con estos mapeos de acuerdo a la documentación de QuickBooks

```json
{
  ...
  "cliente": {
    ...
    "documento_nro": "[QuickBooks: Customer Tax ID]",
    "razon_social": "[QuickBooks: Customer Company Name]",
    "email": "[QuickBooks: Customer Email]",
    "domicilio": "[QuickBooks: Billing Address Line 1]",
  },
  "comprobante": {
    ...
    "fecha": "[QuickBooks: Invoice Date - formato dd/mm/aaaa]",
    "observaciones": "Sincronizado desde QuickBooks"
  },
  "detalle": [
    ...
    {
      ...
      "cantidad": "[QuickBooks: Line Item Quantity]",
      "producto": {
        ...
        "descripcion": "[QuickBooks: Line Item Description]",
        "precio_unitario": "[QuickBooks: Line Item Rate]",
        "codigo": "[QuickBooks: Line Item Product/Service]"
      }
    }
  ]
}
```

### Casos de Uso Adicionales

> 🤝 Queremos que aproveches la posibilidad de usar Zapier, pero <mark style="color:purple;">**es importante que sepas que desde TusFacturasApp no podemos ofrecer soporte ni solucionar inconvenientes relacionados con estas plataformas externas.**</mark>

#### Conectá tu e-commerce con WooCommerce a Zapier y emiti factura electrónica AFIP/ARCA desde TusFacturasAPP

Sugerimos revisar la documentación oficial de Woocomerce y [Zapier](https://zapier.com/apps/woocommerce/integrations) antes de comenzar.

* **Trigger**: WooCommerce "New Order"
* **Mapear**: Order total, customer data, line items

#### CRM con HubSpot

* **Trigger**: HubSpot "Deal Won"
* **Mapear**: Deal amount, company info, contact details

#### Plataformas de Cursos

* **Trigger**: Teachable "New Sale"
* **Mapear**: Course price, student info, enrollment date

### Control de errores

* Revisa logs de Zapier semanalmente. Los servicios de ARCA pueden arrojar diferentes errores, asi como observaciones y es importante que te mantengas al tanto.
* Proba la integración mensualmente ya que las plataformas pueden introducir cambios y tu integración puede dejar de funcionar.&#x20;

#### Seguridad

* Nunca compartas tus credenciales con nadie.
* Usa HTTPS siempre
* Revisa permisos de aplicaciones conectadas

Tu integración de **factura electronica AFIP/ARCA no-code** ya está listo para funcionar automáticamente.

### Recursos Adicionales

* [Documentación completa de la API](../api-factura-electronica-afip-facturacion-ventas/referencia-api-afip-arca.md)
* [Ejemplos de códigos AFIP](../web-services-afip-api-arca/)&#x20;

