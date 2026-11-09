---
description: >-
  TusFacturasAPP: Consulta rápida y precisa de comprobantes AFIP. Integra
  nuestra API en tu sistema y optimiza tus procesos.
icon: magnifying-glass
---

# Consulta simple de ventas

Devuelve un comprobante ya enviado, emitido o en cola, con todos sus datos: estado, CAE, vencimiento del CAE, PDF, QR y observaciones de ARCA. Se busca por tipo de comprobante, punto de venta y número.

#### Endpoint

{% hint style="success" icon="rectangle-api" %}
<mark style="color:purple;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:blue;">`consulta`</mark>
{% endhint %}

{% hint style="info" %}
&#x20;🪙 **Consumo de créditos:** este método no consume créditos.&#x20;
{% endhint %}

#### ¿Consulta simple o avanzada?

| Necesitás                                                          | Usá                                                                                                                   |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------- |
| Un comprobante puntual del que sabes tipo, punto de venta y número | Consulta simple (esta página)                                                                                         |
| Todos los comprobantes de una fecha                                | [Consulta avanzada por fecha](../web-services-afip-api-arca/consulta-avanzada-por-fecha.md)                           |
| Los comprobantes de un rango de números                            | [Consulta avanzada por rango](../web-services-afip-api-arca/consulta-avanzada-por-numero.md)                          |
| Buscar por tu propio identificador (`external_reference`)          | [Consulta avanzada por external reference](../web-services-afip-api-arca/consulta-avanzada-por-external-reference.md) |

Usos típicos: confirmar si un comprobante enviado en modo asincrónico ya tiene CAE, recuperar el PDF o el QR, o revisar las observaciones de ARCA.

#### Estructura del request

| Campo         | Tipo   | Requerido | Descripción                                              |
| ------------- | ------ | --------- | -------------------------------------------------------- |
| `apikey`      | string | Sí        | Credencial de acceso. [Cómo obtenerla](../como-empiezo/) |
| `apitoken`    | string | Sí        | Credencial de acceso                                     |
| `usertoken`   | string | Sí        | Credencial de acceso                                     |
| `comprobante` | objeto | Sí        | Datos del comprobante a buscar. Ver tabla siguiente      |

**Bloque "comprobante"**

| Campo         | Tipo     | Requerido | Descripción                                                                                                      |
| ------------- | -------- | --------- | ---------------------------------------------------------------------------------------------------------------- |
| `tipo`        | string   | Sí        | Tipo de comprobante, según la [tabla de referencia](../parametros/tablas-de-referencia.md). Ejemplo: `FACTURA B` |
| `operacion`   | string   | Sí        | `V` para ventas, `C` para compras                                                                                |
| `punto_venta` | numérico | Sí        | Hasta 4 dígitos. Ejemplo: `2`                                                                                    |
| `numero`      | numérico | Sí        | Número del comprobante, hasta 8 dígitos. Ejemplo: `6`                                                            |

#### Ejemplo del request

```json
{
  "usertoken": "xxxx",
  "apikey": "xxxx",
  "apitoken": "xxxx",
  "comprobante": {
    "tipo": "NOTA DE DEBITO B",
    "operacion": "V",
    "punto_venta": "2",
    "numero": "6"
  }
}
```

Ejemplos de código en cURL, PHP, Python, Node.js y Ruby: [Consulta por tipo y número de comprobante](../web-services-afip-api-arca/consulta-simple-tipo-numero.md).

#### Respuesta

Devuelve el comprobante con la misma estructura con que se envió, más los campos que agregan ARCA y TusFacturasAPP.

```json
{
  "error": "N",
  "errores": [],
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
Los links a los PDF (`comprobante_pdf_url` y `comprobante_ticket_url`) son temporales. Descargá el PDF y guardá toda la información en tu plataforma apenas la obtengas: solo vas a poder acceder a ella mientras tu suscripción esté activa y la normativa de facturación de Argentina indica que debes almacenar las facturas por hasta 10 años.
{% endhint %}

**Campos que agrega la respuesta**

| Campo                    | Descripción                                                                                                                                                                                                                                |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `error`                  | `N` si la consulta funcionó, `S` si hubo errores                                                                                                                                                                                           |
| `errores`                | Lista de errores. Vacía si `error` es `N`                                                                                                                                                                                                  |
| `status`                 | Estado de emisión. Valores posibles: `EMITIDO`, `APROBADO Y EN COLA. SE EMITE EL dd/mm/aaaa`, `EN COLA, ESPERANDO APROBACION`, `ENVIADO A PROCESAR - CON ERROR`, `PROGRAMADO - PROCESADO CON ERRORES`                                      |
| `cae`                    | Código de autorización electrónico otorgado por ARCA. Puede venir con un espacio al final: aplicá trim antes de guardarlo. Solo disponible si tu CUIT está enlazado con ARCA                                                               |
| `vencimiento_cae`        | Vencimiento del CAE informado por ARCA. Formato dd/mm/aaaa. Solo disponible si tu CUIT está enlazado con ARCA                                                                                                                              |
| `afip_qr`                | Texto para generar el QR del comprobante. Solo disponible si tu CUIT está enlazado con ARCA                                                                                                                                                |
| `afip_observaciones`     | Observaciones de ARCA sobre el comprobante. Revisalas siempre: ARCA puede aprobar el comprobante e informar acá un problema que después te notifica                                                                                        |
| `afip_codigo_barras`     | Texto para generar el código de barras (formato anterior al QR)                                                                                                                                                                            |
| `ctacte_status`          | Estado del pago en la cuenta corriente: `PAGADA`, `IMPAGA` o `PAGO PARCIAL`                                                                                                                                                                |
| `vencimiento_pago`       | Vencimiento del pago. Lo enviás vos o se calcula según la condición de pago del cliente. Formato dd/mm/aaaa                                                                                                                                |
| `comprobante_pdf_url`    | Link al PDF en hoja A4. Es temporal: descargalo a tu servidor                                                                                                                                                                              |
| `comprobante_ticket_url` | Link al PDF en formato ticket para papel de 80 mm. Es temporal: descargalo a tu servidor                                                                                                                                                   |
| `micrositios`            | URL del micrositio del cliente y del micrositio de descarga, si tu cuenta los tiene habilitados (plataforma web > Menú > Mi espacio de trabajo > Mis micrositios). La URL del micrositio del cliente no vence y no cambia para ese cliente |

#### ¿Aún te quedan dudas? ¡Contactanos!

Si necesitás asistencia con tu plan API DEV, escribinos a [api@tusfacturas.app](mailto:api@tusfacturas.app) o por el [chat de nuestra web](https://www.tusfacturas.app/contacto.html).

