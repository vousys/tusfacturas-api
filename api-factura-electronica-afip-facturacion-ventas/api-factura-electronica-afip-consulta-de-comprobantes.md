---
description: >-
  TusFacturasAPP: Consulta rápida y precisa de comprobantes AFIP. Integra
  nuestra API en tu sistema y optimiza tus procesos.
---

# Consulta simple de ventas

La **API ARCA/AFIP de TusFacturasAPP** ofrece dos métodos para consultar comprobantes fiscales emitidos desde tu sistema: el método de **consulta simple** y el de [**consulta avanzada**](consulta-avanzada.md). Ambos son fundamentales para verificar el estado y obtener los datos de las ventas realizadas.

### 🔸 Consulta simple de ventas

Este método te permite obtener una lista de comprobantes emitidos filtrando por CUIT, punto de venta, fecha, tipo de comprobante u otros parámetros básicos. Es ideal para visualizar un resumen general o hacer auditorías internas de tu facturación electrónica.

Esta función es muy útil para:

* **Verificar el estado de los comprobantes:** Saber si un comprobante fue emitido correctamente, si fue rechazado por la AFIP o si ya fue presentado ante el organismo recaudador.
* **Buscar comprobantes específicos:** Localizar una factura en particular utilizando diferentes criterios de búsqueda, como el número de comprobante, la fecha de emisión, el cliente, etc.
* **Generar reportes:** Obtener información resumida o detallada sobre un conjunto de comprobantes, lo que puede ser útil para tareas de contabilidad o análisis.
* **Integrar con otros sistemas:** Utilizar la información de los comprobantes para alimentar tu sistema o aplicacion, como un ERP o un CRM.

**En resumen,** la consulta de comprobantes es una herramienta esencial para gestionar tu facturación electrónica de manera eficiente y tener un control total sobre tus operaciones.

### :rocket: Ejemplo de consulta simple

💡 El uso de éste método no contabiliza como un request en tu suscripción

{% content-ref url="../web-services-afip-api-arca/consulta-simple-tipo-numero.md" %}
[consulta-simple-tipo-numero.md](../web-services-afip-api-arca/consulta-simple-tipo-numero.md)
{% endcontent-ref %}

### 🛠️ Estructura del request a enviar:

| Name        | Type   | Description                                                             |
| ----------- | ------ | ----------------------------------------------------------------------- |
| comprobante | object | <p>Un objeto según estructura que se detalla a continuación.</p><p></p> |
| apikey      | string | Tus credenciales de acceso.                                             |
| apitoken    | string | Tus Credenciales de acceso.                                             |
| usertoken   | string | Tus Credenciales de acceso.                                             |

#### Estructura a enviar dentro del bloque: "Comprobante"

| `tipo`        | <p>Campo numérico según tabla de referencia de <a href="https://www.tusfacturas.com.ar/api-factura-electronica-afip.html#tabla-comprobantes">Tipos de comprobantes(***)</a>.<br><strong>Ejemplo: FACTURA B</strong></p> |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `operacion`   | <p>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C).<br>Valores Permitidos: <strong>V, C</strong><br><strong>Ejemplo: V</strong></p>                                   |
| `punto_venta` | <p>Campo numérico entero. Longitud máxima 4 digitos.<br><strong>Ejemplo: 3</strong></p>                                                                                                                                 |
| `numero`      | <p>Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante.<br><strong>Ejemplo: 4567</strong></p>                                                  |

### Ejemplo del JSON de respuesta:

La información que obtenés se devuelve estructurada de la misma manera que la enviaste, con el agregado de ciertos campos que se detallan a continuación

```json
{
  "error": "N",
  "errores": [
    ""
  ],
  "rta": "OK",
  "cliente": {
    "documento_tipo": "DNI",
    "documento_nro": "1292963535 ",
    "razon_social": "Pirulo",
    "email": "test@test.com",
    "domicilio": "Av Sta Fe 123"
  },
  "comprobante": {
    "fecha": "28/07/2015",
    "tipo": "NOTA DE DEBITO B",
    "moneda": "PES",
    "idioma": 1,
    "cotizacion": 1,
    "operacion": "V",
    "punto_venta": 2,
    "numero": 6,
    "periodo_facturado_desde": "27/07/2015",
    "periodo_facturado_hasta": "30/07/2015",
    "rubro": "Servicios web",
    "rubro_grupo_contable": "servicios",
    "detalle": [
      {
        "cantidad": 1,
        "producto": {
          "descripcion": "Gomas de borrar",
          "precio_unitario": 100,
          "alicuota": 21,
          "bonificacion": 0,
          "impuestos_internos_alicuota": 0,
          "precio_total": 100
        },
        "bonificacion_porcentaje": 0,
        "leyenda": ""
      }
    ],
    "bonificacion": 10,
    "leyenda_gral": " ",
    "percepciones_iibb": 30,
    "percepciones_iva": 0,
    "tributos": [
      {
        "tipo": 7,
        "tipo_descripcion": "Percepcion de IIBB",
        "regimen": 5,
        "regimen_descripcion": "BUENOS AIRES",
        "base_imponible": 100,
        "alicuota": 10,
        "total": 10
      },
      {
        "tipo": 7,
        "tipo_descripcion": "Percepcion de IIBB",
        "regimen": 6,
        "regimen_descripcion": "CATAMARCA",
        "base_imponible": 100,
        "alicuota": 20,
        "total": 20
      }
    ],
    "exentos": 0,
    "nogravados": 0,
    "impuestos_internos": 0,
    "impuestos_internos_base": 0,
    "impuestos_internos_alicuota": 0,
    "total": 138.9,
    "cae": "65301278726386 ",
    "external_reference": "Lun141",
    "micrositios": {
      "cliente": "url-del-micrositio",
      "descarga": "url-del-micrositio"
    },
    "tags": [
      "etiqueta1",
      "etiqueta2"
    ],
    "ctacte_status": "PAGO PARCIAL",
    "status": "EMITIDO",
    "afip_codigo_barras": "12121212121006000300000000000000201811052 ",
    "afip_observaciones": "Observacion: El credito fiscal discriminado en el presente comprobante solo podra ser computado a efectos del Procedimiento permanente de transicion al Regimen General. [ codigo: 10217 ]. ",
    "afip_qr": "https://www.afip.gob.ar/fe/qr/?p=eyJ2ZXIiOjEsImZlY2hhIjoiMjadadasdasdaAyMS0wNi0wNSIsImN1aXQiOiIyNzI4NTA1MTQ2NiIsInB0b1Z0YSI6IjEwIiwidGlwb0NtcCI6MSwibnJvQ21wIjoiMDAwMDAwNzgiLCJpbXBvcnRlIjoiMDAwMDAwMDAwMzA4NS41MCIsIm1vbmVkYSI6IlBFUyIs ",
    "vencimiento_cae": "07/08/2015",
    "vencimiento_pago": "27/08/2015",
    "comprobante_pdf_url": "https://www.dominio.com/00000006.pdf",
    "comprobante_ticket_url": "https://www.dominio.com/url",
    "abono": "N",
    "comprobantes_asociados_periodos": {
      "fecha_hasta": "31/12/2025",
      "fecha_desde": "29/12/2025"
    }
  }
}
```

{% hint style="info" %}
Es importante que descargues toda la información junto con el pdf y lo almacenes en tu plataforma, ya que si tu cuenta o suscripción no se encuentran vigentes, no podrás obtenerlo.
{% endhint %}

#### Campos devueltos que no forman parte del JSON que vos envias:

<table><thead><tr><th width="198">Nombre del campo</th><th>Info</th></tr></thead><tbody><tr><td>cae</td><td>Campo alfanumérico, con un espacio adicional, devuelto por AFIP, a modo e código de autorización electrónica de la transacción realizada</td></tr><tr><td>afip_qr</td><td>Campo alfanumérico, conteniendo el texto necesario para formar el QR </td></tr><tr><td>ctacte_status</td><td>Campo alfanumérico, conteniendo el estado del pago de ese comprobante dentro de la cuenta corriente. Los valores posibles son: PAGADA, IMPAGA , PAGO PARCIAL</td></tr><tr><td>status</td><td>Campo alfanumérico, conteniendo el estado de emisión de ese comprobante . Lo valores les son: "EMITIDO", "APROBADO Y EN COLA. SE EMITE EL dd/mm/aaaa", "EN COLA, ESPERANDO APROBACION", "ENVIADO A PROCESAR - CON ERROR"</td></tr><tr><td>afip_codigo_barras</td><td>Campo alfanumérico, conteniendo el texto necesario para formar el código de barras de AFIP (legacy)</td></tr><tr><td>vencimiento_cae</td><td>Fecha enviada por AFIP al momento de autorizar el comprobante. Formato: dd/mm/aaaa</td></tr><tr><td>vencimiento_pago</td><td>Fecha que indica la fecha de vencimiento del pago. Éste dato enviado por el cliente, o auto-calculado en base a la condición de pago estipulada en el perfil del cliente. Formato: dd/mm/aaaa</td></tr><tr><td>comprobante_<em>pdf</em>_url</td><td>Campo alfanumérico  al pdf en hoja A4 del comprobante.</td></tr><tr><td>micrositios</td><td>En este campo se te devolverá la URL del micrositio del cliente y la de url del micrositio de descarga, solo si tu cuenta tiene los micrositios habilitados. Para configurarlo, ingresá a nuestra plataforma web, menú > mi espacio de trabajo > mis micrositios</td></tr><tr><td>comprobante_ticket_url</td><td>La url al PDF con el comprobante en formato ticket para papel de 80mm</td></tr><tr><td>afip_observaciones</td><td>Campo alfanumerico con las observaciones que aplico AFIP/ARCA sobre ese comprobante. Es importente que las controles ya que muchas veces aprueban el comprobante pero te informan de ciertos errores en este campo para luego enviarte una comunicación.</td></tr></tbody></table>

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).







