---
description: >-
  Conecta tu plataforma y factura en ARCA/AFIP con la API de factura electrónica
  más fácil de Argentina.
icon: code
---

# Referencia API AFIP ARCA

### API ARCA – Integra tu sistema con los Web Services de ARCA fácilmente para facturar tus ventas.

La **API de facturación electrónica para ARCA de TusFacturasAPP** te permite interactuar de forma directa y eficiente con los **web services de AFIP/ARCA**, facilitando la emisión de comprobantes electrónicos desde tu software.

#### ¿Qué es un comprobante electrónico?

En el contexto de nuestra API, se denomina **"comprobante"** a cualquier documento digital vinculado a operaciones comerciales, tales como:

* Facturas electrónicas (de venta o compra), recibos C y liquidaciones.
* Notas de crédito y débito
* Pedidos
* Presupuestos
* Remitos&#x20;

Esto permite a tu sistema manejar toda la documentación fiscal y comercial en formato electrónico, cumpliendo con las exigencias legales vigentes.

### Endpoint principal de la API ARCA:

{% hint style="info" %}
<mark style="color:purple;">**POST**</mark>

`https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">**`metodo-elegido`**</mark>
{% endhint %}

Este endpoint permite el envío de comprobantes en distintos modos de operación, según las necesidades de tu sistema:

#### ⚙️ Modos de envío disponibles

* [**Envío instantáneo**](api-factura-electronica-afip-facturacion-nuevo-comprobante.md)**:**\
  Envía un comprobante y recibe la respuesta al instante. Ideal para sistemas que requieren confirmación inmediata. Sujeto a la disponibilidad del servicio de **AFIP o ARCA**.
* [**Envío asincrónico**](api-factura-electronica-afip-facturacion-nuevo-comprobante-1.md)**:**\
  Envía el comprobante a una cola de procesamiento. Recibirás una notificación por **webhook** una vez procesado. Recomendado para sistemas que manejan grandes volúmenes.
* [**Lotes instantáneos**](api-factura-electronica-afip-api-facturacion-por-lotes.md)**:**\
  Permite enviar varios comprobantes en un único lote y recibir una única respuesta inmediata. También depende de la disponibilidad del servicio de AFIP o ARCA.

> 🔧 Nuestra API ARCA está diseñada para desarrolladores que buscan una integración rápida, robusta y conforme a las normativas de facturación electrónica en Argentina.



### Estructura del JSON  a enviar

Tipo de datos: **JSON ,** Charset: **UTF-8**

Request: Body

| Name        | Type   | Description                                                 |
| ----------- | ------ | ----------------------------------------------------------- |
| usertoken   | string | Tus credenciales de acceso                                  |
| apitoken    | string | Tus credenciales de acceso                                  |
| apikey      | string | Tus credenciales de acceso                                  |
| comprobante | object | Estructura de "comprobante" según se informa a continuación |
| cliente     | object | Estructura de "Cliente", según se informa a continuación    |

### JSON de ejemplo para emitir comprobantes electrónicos

A continuación te mostramos un **ejemplo completo en formato JSON** que incluye todas las opciones disponibles para personalizar tus **comprobantes electrónicos** con la API de TusFacturasAPP.

> ⚠️ **Importante**: No todos los campos son obligatorios. Los datos requeridos varían según el [**tipo de comprobante**](../web-services-afip-api-arca/) que desees emitir (factura, nota de crédito, remito, etc.).

Para obtener una guía detallada de los campos específicos por tipo de comprobante, visitá nuestra [página de ejemplos por tipo de comprobante](../web-services-afip-api-arca/).

Este ejemplo te servirá como referencia para construir tus requests correctamente y evitar errores comunes al integrarte con los **web services de AFIP/ARCA**.

{% code title="JSON" %}
```json
{
   "usertoken":"xxxxxx",
   "apikey":"xxxx",
   "apitoken":"xxxxxx",
   "cliente":{
      "documento_tipo":"DNI",
      "documento_nro":"1292963535",
      "razon_social":"Pirulo",
      "nombre_fantasia": "",
      "email":"test@test.com",
      "domicilio":"Av Sta Fe 123",
      "provincia":"2",
      "envia_por_mail":"S",
      "condicion_pago":"214",
      "condicion_pago_otra":"Cobrado en ventanilla",
      "condicion_iva":"CF",
      "condicion_iva_operacion":"CF",
      "reclama_deuda": "S",
      "reclama_deuda_dias": 5,
      "reclama_deuda_repite_dias": 10,       
      "rg5329":"N"
   },
   "comprobante":{
      "fecha":"28\/07\/2015",
      "tipo":"NOTA DE DEBITO B",
      "moneda":"DOL",
      "idioma":"1",
      "cotizacion":"15.20",
      "operacion":"V",
      "punto_venta":"2",
      "numero":"6",
      "datos_informativos": {
            "paga_misma_moneda": "N"
      },
      "periodo_facturado_desde":"27\/07\/2015",
      "periodo_facturado_hasta":"30\/07\/2015",
      "vencimiento":"30\/08\/2015",
      "rubro":"Servicios web",
      "external_reference":"ABC123",
      "tags":[
         "etiqueta1",
         "etiqueta2"
      ],
      "rubro_grupo_contable":"servicios",
      "abono":"S",
      "abono_frecuencia":"2",
      "abono_hasta":"10/2019",
      "abono_actualiza_precios":"N",
      "detalle":[
         {
            "cantidad":"1",
            "afecta_stock":"N",
            "bonificacion_porcentaje":"0",
            "producto":{
               "descripcion":"PAPAS",
               "unidad_bulto":"10",
               "lista_precios":"MI LISTA DE PRECIOS",
               "codigo":"",
               "precio_unitario_sin_iva":"100.45",
               "alicuota":"21",
               "impuestos_internos_alicuota":0,
               "unidad_medida":"7",
               "actualiza_precio":"S",
               "rg5329":"N"
            },
            "leyenda":"blanca, cepillada"
         },
         {
            "cantidad":"1.5",
            "bonificacion_porcentaje":"0",
            "afecta_stock":"N",
            "producto":{
               "descripcion":"HUEVOS",
               "unidad_bulto":"30",
               "lista_precios":"MAPPLETS",
               "codigo":"MPH",
               "precio_unitario_sin_iva":"50",
               "alicuota":"10.5",
               "impuestos_internos_alicuota":0,
               "unidad_medida":"7",
               "actualiza_precio":"N",
               "rg5329":"N"
            },
            "leyenda":""
         },
         {
            "cantidad":"2",
            "bonificacion_porcentaje":"0",
            "afecta_stock":"S",
            "producto":{
               "descripcion":"ZANAHORIA",
               "unidad_bulto":"50",
               "lista_precios":"MI LISTA DE PRECIOS",
               "codigo":"ZNH1",
               "precio_unitario_sin_iva":"200",
               "alicuota":"21",
               "impuestos_internos_alicuota":0,
               "unidad_medida":"7",
               "actualiza_precio":"S",
               "rg5329":"N"
            },
            "leyenda":""
         }
      ],
      "rg_especiales":{
         "regimen":"Factura de Cr\u00e9dito Electr\u00f3nica MiPyMEs (FCE)",
         "datos":[
            {
               "id":2101,
               "valor":"0170215820000005295250"
            },
            {
               "id":23,
               "valor":"HANDYWAY CARGO S.A"
            },
            {
               "id":27,
               "valor":"SCA"
            }
         ]
      },
      "comprobantes_asociados":[
         {
            "tipo_comprobante":"FACTURA C",
            "punto_venta":"3",
            "numero":"00000349",
            "comprobante_fecha":"03/03/2022",
            "cuit":27285051466
         }
      ],
      "comprobantes_asociados_periodo":{
         "fecha_desde":"20/11/2020",
         "fecha_hasta":"20/12/2020"
      },
      "pagos":{
         "formas_pago":[
            {
               "descripcion":"VISA DB",
               "importe":0.6
            },
            {
               "descripcion":"MercadoPago",
               "importe":50
            }
         ],
         "total":50.6
      },
      "tributos":[
         {
            "tipo":6,
            "regimen":1,
            "base_imponible":1000,
            "alicuota":10,
            "total":100
         }
      ],
      "exentos":"0",
      "impuestos_internos":"0",
      "impuestos_internos_base":"0",
      "impuestos_internos_alicuota":"0",
      "bonificacion":"120",
      "leyenda_gral":"Segun Orden de compra III1333",
      "comentario":"Factura correspondiente al servicio XX",
      "total":"573.22"
   }
}
```
{% endcode %}

### Ejemplos de comprobantes según su tipo y letra

Con TusFacturasAPP podrás emitir comprobantes electrónicos ARCA, clasificados según su **tipo (Factura, Nota de Crédito, etc.)** y **letra (A, B, C, E, M)**.

Explorá los distintos escenarios de facturación que podés implementar, adaptados a las normativas fiscales vigentes de AFIP:

#### ✅ Tipos de comprobantes disponibles:

* **Factura A / B / C / E / M / MiPyme**
* **Nota de Crédito A / B / C / E / MiPyme**&#x20;
* **Nota de Débito A / B / C / E / MiPyme**
* **Presupuestos**
* **Pedidos**
* **Remitos**
* **Recibos C**
* **Liquidaciones A y B**

Cada ejemplo incluye los campos requeridos y opcionales, además de los valores específicos para cada categoría. Esto te permitirá implementar la facturación electrónica de forma ágil y segura desde cualquier sistema.

{% content-ref url="../web-services-afip-api-arca/" %}
[web-services-afip-api-arca](../web-services-afip-api-arca/)
{% endcontent-ref %}

### Datos para tener en cuenta:

{% hint style="info" %}
**PDF**

* La URL del PDF que recibis es temporal,  solo sirve para el día que la consultas.
* La URL del ticket sera devuelta para todos los modelos de PDF que seleccionas desde tu punto de venta, con excepción del modelo "1.1 - Modelo Viejo".
* Es importante que descargues toda la información junto con el contenido del pdf y lo almacenes en tu plataforma, ya que si si tu cuenta o suscripción no se encuentran vigentes, no podrás volver a obtenerlo.  AFIP no genera archivos en PDF, por lo que tampoco podrás obtenerlo desde ahi.
* Tene en cuenta que a partir del 01-07-2021, todo comprobante A que se emitan a un monotributista deberá llevar la siguiente leyenda: "_El crédito fiscal discriminado en el presente comprobante, sólo podrá ser computado a efectos del Régimen de Sostenimiento e Inclusión Fiscal para Pequeños Contribuyentes de la Ley Nº 27.618"._ **Éste valor no debe ser enviado,** ya que saldrá automáticamente impreso en los PDF que se generen desde nuestra plataforma.



**CAE (Código de Autorización electrónica de AFIP)**

* El CAE es el Código de Autorización Electrónico que otorga AFIP, como confirmación de la creación del comprobante. Es un dato importante para almacenar como respuesta.
* Los CAE tienen fecha de vencimiento y se devuelve en formato dd/mm/aaaa
* Por cuestiones de compatibilidad, el número de CAE se envia como texto con un espacio al final, el cual sugerimos eliminar de tu lado.



**AFIP CÓDIGO DE BARRAS / QR**

* Por cuestiones de compatibilidad, el texto que se retorna en el campo  afip\_qr, se envía con un espacio al final, el cual sugerimos eliminar de tu lado.
* El campo afip\_codigo\_barras dejará de ser enviado a partir del 01/01/2024
* Cuando la respuesta es exitosa, podes obtener el texto que se necesita para armar el código QR, en caso que generes el PDF desde tu lado .



**NOTAS DE DÉBITO Y CRÉDITO**

* Las notas de débito y crédito requieren que envies obligatoriamente los comprobantes asociados (o su período asociado). Conocé más [desde aquí](api-factura-electronica-afip-notas-credito-debito.md)



**FECHA**

* Una vez emitido un comprobante (factura, nota de crédito o débito) en AFIP/ARCA con una fecha determinada, no podrás emitir otro comprobante del mismo punto de venta con una fecha anterior. Esta restricción es impuesta por AFIP/ARCA y no puede ser modificada, incluso mediante la emisión de notas de crédito o débito.
* AFIP/ARCA ademas, tiene otra validación para la fecha del comprobante:&#x20;
  * Para actividades vinculadas a servicios, AFIP/ARCA te permitirá facturar con una anterioridad de hasta 10 días, si no has emitido ningún comprobante con fecha posterior a esa.
  * Para actividades relacionadas a la comercialización de bienes,  el plazo es de 5 días hacia atrás, si no has emitido ningún comprobante con fecha posterior a esa.



**REDONDEO DE NÚMEROS / SUMATORIAS / TOTALES**

* Usamos punto (.) como separador decimal y no utilizamos separador de miles.
*   Nuestra plataforma gestiona los precios unitarios de productos y servicios con 3 decimales, mientras que los totales se calculan con 2 decimales. Debido a esto, pueden surgir pequeñas diferencias de facturación en aquellas empresas que trabajan con precios finales (IVA incluido).

    Para garantizar la precisión fiscal, aplicamos el método de redondeo "Round half even" (redondeo bancario), siguiendo estrictamente los lineamientos de ARCA.

    En el siguiente artículo sobre [ajustes, redondeos y precios sin IVA](https://ayuda.tusfacturas.app/es/articles/12548047-redondeos-ajustes-y-precios-sin-iva) te explicamos cómo funciona mediante un ejemplo práctico.
* Siempre debes enviar los valores en positivo (mayor o igual a cero), nunca con valores negativos.
* **TusFacturas.app NO válida la totalidad de los datos enviados como asi tampoco las sumatorias de los ítems que estas enviando para facturar. Es tu responsabilidad corroborar y validar éstos datos antes de enviarlos.**
* **AFIP recibe únicamente totales**, no el detalle de los items que facturas, ya que para los comprobantes de tipo "A" , "B" , "C" y "M" , Factura de crédito electrónica, TusFacturas.app utiliza el método de facturación mediante webservice AFIP "WSFEv1" ( Factura electrónica sin detalle de productos ).



**MICROSITIOS**

* Las URL de los micrositios solo te serán devueltas con datos, si los mismos se encuentran habilitados en tu cuenta.  Éstas URL no cambian y le permiten a tu cliente acceder a un portal neutro a descargar la factura y/o a consultar su historial de facturas emitidas.
* Para configurar los micrositios, ingresa a nuestra plataforma web, menú > mi espacio de trabajo > mis micrositios. Conocé más de los micrositios [desde aquí](https://www.tusfacturas.app/).



**EDICIÓN / ELIMINACIÓN DE COMPROBANTES**&#x20;

* **Aquellos comprobantes que hayan impactado en AFIP, no podrán ser eliminados. Sólo pueden ser anulados contablemente generando una** [**nota de crédito**](api-factura-electronica-afip-notas-credito-debito.md#que-es-una-nota-de-credito-nc-electronica)**.**
* Ningún comprobante puede ser modificado una vez creado.



**TEXTOS**

* La información debe estar encodeada con UTF-8 para evitar errores.



**OBSERVACIONES**

* El campo de "observaciones" contiene las observaciones  enviadas por AFIP/ARCA sobre esa operación, dado que los comprobantes pueden ser aprobados pero aún así, observados. Sugerimos almacenar ésta información y revisarla.



ERRORES

* Revisa el código de estado HTTP: Confirma siempre que recibas una respuesta HTTP 200. Esto garantiza que tu solicitud llegó y fue procesada correctamente.
* Valida el campo de error: Controla el campo `"error"` en la respuesta. Su valor será `"S"` si hubo un problema o `"N"` si la operación se realizó con éxito, y dentro de `"errores"` encontraras el detalle del error.



**RATE LIMIT**

* El código de estado HTTP: 429 indica que tu aplicación está excediendo el límite de solicitudes permitido por segundo. Esto se debe a las reglas de seguridad de nuestra plataforma, diseñadas para proteger la estabilidad del sistema.



**CONCURRENCIA**

* Espera la respuesta de la API antes de enviar la siguiente solicitud.
* Si el proceso es paralelo, incorporar un delay mínimo (por ejemplo, 100ms) entre las peticiones para evitar que ingresen en el mismo segundo.



**NUMERACIÓN**

* La numeración es correlativa por punto de venta + Tipo de comprobante.





**⚠️ IMPORTANTE - Consideraciones Legales:**

En Argentina, todas las operaciones comerciales deben estar debidamente facturadas y declaradas ante AFIP/ARCA según lo establece la normativa vigente.\
Mantener "doble contabilidad" o facturas no declaradas:\
\- Constituye evasión fiscal (Ley 24.769)\
\- Puede resultar en sanciones económicas significativas\
\- Puede derivar en acciones penales\
\- Pone en riesgo la continuidad de tu negocio
{% endhint %}

### 🔁 ¿Qué devuelve la API ARCA de TusFacturasAPP?

La **respuesta que recibís al emitir un comprobante electrónico** depende del **método de invocación** que elijas en la integración con la API de TusFacturasAPP.

#### 📌 Modalidades de invocación y sus respuestas

* **🕒 Envío instantáneo**\
  Recibís inmediatamente la respuesta con todos los datos del comprobante autorizado por AFIP o ARCA. Ideal para integraciones en tiempo real.
* **⏳ Envío asincrónico**\
  La respuesta inicial solo confirma que el comprobante fue recibido para su procesamiento. Más tarde, cuando se autorice, **te notificamos por webhook** con la respuesta final y los datos fiscales completos.
* **📦 Envío por lotes**\
  Podés enviar varios comprobantes a la vez. Recibís una respuesta agrupada que incluye el resultado individual de cada comprobante (siempre sujeta al estado del servicio de AFIP/ARCA).

### 📊 ¿Dónde puedo ver las ventas generadas?

Desde la plataforma web de **TusFacturasAPP**, podés consultar y administrar fácilmente los comprobantes electrónicos emitidos. Accedé desde el panel principal a:

* **Menú > Facturación > Mis ventas**: para ver todas las ventas ya emitidas.
* **Menú > Facturación > Ventas programadas**: para consultar las ventas aún pendientes de emisión automática o manual.

Desde estas secciones podrás **visualizar, filtrar, descargar o anular** los comprobantes emitidos, todo desde una única interfaz centralizada.



### ✅ ¿Cómo verificar si un comprobante fue emitido correctamente en ARCA?

Además del panel de TusFacturasAPP  y cuando estes en producción, también podés corroborar que un comprobante fue autorizado por **AFIP/ARCA** de forma oficial:

1. Ingresando a la web de AFIP con tu **CUIT y clave fiscal**.
2. Usando el servicio “**Mis Comprobantes**” en el menú de servicios habilitados. Contempla que ARCA pone a disposición la información al día anterior.
3. Utilizando la herramienta oficial de [**Constatación de Comprobantes Electrónicos**](https://servicioscf.afip.gob.ar/publico/comprobantes/cae.aspx), donde podes ingresar el CUIT del emisor, tipo y número de comprobante. Conoce más desde la guía de [Constatación de comprobantes en AFIP.](https://ayuda.tusfacturas.app/es/articles/10844438-constatacion-de-comprobantes-en-afip)

> 🧩 Esta verificación es útil para control fiscal o para mostrarle al cliente final que su comprobante fue validado correctamente.
>
>

### Definición de datos a enviar para generar ventas:

### Estructura del bloque: "Comprobante"

<table><thead><tr><th width="237.1885936052475">Nombre del campo</th><th width="150.8396361895644" align="center">Es requerido?</th><th>Comentarios</th></tr></thead><tbody><tr><td>fecha</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo fecha. Formato esperado: dd/mm/aaaa. Ejemplo: 13/05/2018.  Si usas el metodo asincrónico, la fecha será el día que queres que se emita. Una vez emitido un comprobante (factura, nota de crédito o débito) en AFIP/ARCA con una fecha determinada, no podrás emitir otro comprobante del mismo punto de venta con una fecha anterior. Esta restricción es impuesta por AFIP/ARCA y no puede ser modificada, incluso mediante la emisión de notas de crédito o débito.</td></tr><tr><td>tipo</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfabético según <a href="../parametros/tablas-de-referencia.md#tipos-de-comprobantes">tabla de referencia de Tipos de comprobantes</a></td></tr><tr><td>operacion</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta (V) o de compra (C). Valores Permitidos: V, C Ejemplo: V</td></tr><tr><td>idioma</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico. Longitud 1 caracter. Indica el idioma en que se imprimira el PDF del comprobante. Valores Permitidos: 1 = Español, 2= Ingles</td></tr><tr><td>punto_venta</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico entero. Longitud máxima 5 digitos.</td></tr><tr><td>moneda</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico de 3 Digitos según <a href="../parametros/tablas-de-referencia.md#monedas">tabla de referencia de Monedas</a> .</td></tr><tr><td>cotizacion</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td><p>Número decimal con 3 lugares decimales. Representa el valor en pesos argentinos de una moneda extranjera. Se obtiene en tiempo real a través de nuestra API de cotización ARCA. </p><p>Si moneda = PES, la cotizacion debe ser siempre 1.</p><p>Si facturas en otra moneda, debes indicar un dato valido, ya que ARCA lo validara.</p><p>Ejemplo: 15.20. Solo aplicable a monedas distintas al peso argentino.</p></td></tr><tr><td>numero</td><td align="center">OPCIONAL</td><td>El numero del comprobante a generar. Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante contra AFIP. Si el nro de comprobante NO es enviado, traeremos la próxima numeración . Ejemplo: 4567</td></tr><tr><td>vencimiento</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo fecha, formato esperado: dd/mm/aaaa. </td></tr><tr><td>periodo_facturado_desde</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo fecha. Formato esperado: dd/mm/aaaa. Opcional solo para quienes facturen productos y asi lo indiquen en la configuración de su CUIT+punto de venta. Obligatorio para quienes facturen Servicios o Productos y Servicios.</td></tr><tr><td>periodo_facturado_hasta</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo fecha. Formato esperado: dd/mm/aaaa. Opcional solo para quienes facturen productos y así lo indiquen en la configuración de su CUIT+punto de venta.Obligatorio para quienes facturen Servicios o Productos y Servicios.</td></tr><tr><td>rubro</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico que no sale impreso en el pdf. Se utiliza para los reportes que brinda nuestra plataforma web y no es requerido por AFIP. Longitud máxima 255 caracteres. Indica el rubro al cual pertenecerá el comprobante. </td></tr><tr><td>rubro_grupo_contable</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico que no sale impreso en el pdf. Se utiliza para los reportes que brinda nuestra plataforma web y no es requerido por AFIP/ARCA. Longitud máxima 255 caracteres. Indica el grupo contable al que pertenece el rubro.  </td></tr><tr><td>abono</td><td align="center">OPCIONAL (Solo disponible para ventas)</td><td>Campo alfabético, longitud máxima 1 caracter. Valores permitidos S (si) o N (no). Indica si el comprobante a generar es un abono recurrente.</td></tr><tr><td>abono_frecuencia</td><td align="center"><mark style="color:purple;">REQUERIDO SOLO SI ENVIA ABONO</mark></td><td>Campo numerico sin decimales. Indica la frecuencia en meses con la que debe generarse la recurrencia del abono.</td></tr><tr><td>abono_hasta</td><td align="center"><mark style="color:purple;">REQUERIDO SOLO SI ENVIA ABONO</mark></td><td>Campo fecha (mm/yyyy). Longitud maxima 7. Indica el mes y año hasta el cual debe generarse el abono recurrente.</td></tr><tr><td>abono_actualiza_precios</td><td align="center"><mark style="color:purple;">REQUERIDO SOLO SI ENVIA ABONO</mark></td><td>Campo alfabético, longitud máxima 1 caracter. Valores permitidos S (si) o N (no). Indica si cada vez que se genera el abono, se actualiza los precios de los productos contra el precio actual de la lista de precios.</td></tr><tr><td><mark style="color:blue;">detalle</mark></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Lista de conceptos a facturar. <a href="referencia-api-afip-arca.md#estructura-de-detalle-de-conceptos">Objeto JSON</a>, según estructura que se detalla a continuación</td></tr><tr><td><mark style="color:blue;">fex</mark></td><td align="center"><mark style="color:purple;">REQUERIDO PARA COMPROBANTES E</mark></td><td>Solo para comprobantes de tipo E. Objeto JSON, según estructura detallada en: <a href="api-factura-electronica-afip-factura-electronica-afip-exportacion.md">Factura electronica de exportacion".</a></td></tr><tr><td>bonificacion</td><td align="center">OPCIONAL</td><td><p>Campo numérico positivo con 2 decimales. separador de decimales: punto. Indica el valor aplicado en concepto de bonificación sin IVA Ejemplo: 12.67. </p><p>Tener en cuenta para el cálculo que la bonificación se aplica sobre el primer subtotal SIN IVA (generalmente el del 21%) y se lo gravará con el importe de IVA que le corresponda.</p></td></tr><tr><td>leyenda_gral</td><td align="center">OPCIONAL</td><td><p>Campo alfanumérico. Longitud máxima 500 caracteres. Contenido opcional. Es una leyenda general / observación comercial, que saldrá impresa en el bloque central del PDF, al final del último producto. </p><p>Si queres que parte del texto salga en una linea nueva, agrega: #@# , si queres enviar el "%", en su lugar envía: #&#x26;#.</p><p>Ejemplo: Aplica plan 12 cuotas, con un 10#&#x26;# de interes.</p></td></tr><tr><td>comentario</td><td align="center">OPCIONAL</td><td>Campo alfanumerico, opcional. Longitud máxima: 255 caracteres. Éste campo no saldrá impreso en la factura.</td></tr><tr><td><mark style="color:blue;">tributos</mark></td><td align="center"><mark style="color:purple;">SOLO SI APLICA</mark></td><td>Objeto JSON, con la lista de percepciones y otros impuestos, según se detalla su estructura a continuación.</td></tr><tr><td>impuestos_internos</td><td align="center">OPCIONAL</td><td>Si envias impuestos internos en cada uno de los items, debes Indicar el valor monetario correspondiente a la sumatoria los impuestos internos detallados en cada uno de los items que incluis. Campo numérico positivo con 2 decimales. separador de decimales: punto. Ejemplo: 42.67</td></tr><tr><td>impuestos_internos_base</td><td align="center">OPCIONAL</td><td>Si envías impuestos internos en cada uno de los items, debes indicar la sumatoria de la base imponible sobre la cual se calcularon los impuestos internos. Campo numérico positivo con 2 decimales. separador de decimales: punto. Ejemplo: 42.67</td></tr><tr><td>impuestos_internos_alicuota</td><td align="center">OPCIONAL</td><td>La alícuota sobre la cual se calcularon los impuestos internos de cada uno de los items que incluiste. Por cada comprobante se permite una única alícuota de impuestos internos. Campo numérico positivo con 2 decimales. separador de decimales: punto. Ejemplo: 42.67</td></tr><tr><td>total</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico positivo con 2 decimales. separador de decimales: punto. Indica el valor monetario de la sumatoria de conceptos incluyendo IVA e impuestos. Ejemplo: 12452.67</td></tr><tr><td><mark style="color:blue;">comprobantes_asociados</mark></td><td align="center"><mark style="color:orange;">SOLO PARA NC O ND</mark></td><td>Lista de comprobantes asociados. Requerido únicamente para NC o ND de tipo A,B,C,M. <a href="referencia-api-afip-arca.md#estructura-de-comprobantes-asociados">Objeto JSON</a> Según estructura que se detalla a continuación</td></tr><tr><td><mark style="color:blue;">rg_especiales</mark></td><td align="center"><mark style="color:orange;">SOLO SI APLICA ALGUNA RG</mark></td><td>Lista de datos adicionales requeridos por AFIP, según la RG a la que aplique el comprobante. <a href="referencia-api-afip-arca.md#estructura-de-rg-especiales">Objeto JSON</a> Según estructura que se detalla a continuación</td></tr><tr><td>external_reference</td><td align="center"><mark style="color:purple;">SOLO PARA VENTAS ASINCRÓNICAS</mark></td><td>Dato alfanumérico de hasta 255 caracteres (solo se permiten letras, números, guión bajo y guión medio), que se utiliza para referenciar a éste comprobante, dentro de tu sistema. Es opcional, salvo que utilices los métodos de envió a la cola de procesamiento. No se realiza validación de éste campo, para verificar que el mismo no exista.</td></tr><tr><td><mark style="color:blue;">tags</mark></td><td align="center">OPCIONAL</td><td>Dato que no sale impreso en el PDF, solo para gestion interna ya que se visualiza en la consulta del comprobante desde la plataforma web. Objeto JSON, según estructura que se detalla a continuación.</td></tr><tr><td>datos_informativos</td><td align="center">OPCIONAL</td><td>Objeto JSON, según estructura que se detalla a continuación.</td></tr></tbody></table>

### Estructura del bloque: "Cliente" y "Proveedor"

Para poder generar el comprobante debes enviar un detalle de todos los datos  según se informa a continuación. Si vas  a enviar una venta, debes enviar el bloque "cliente", en cambio si vas a enviar una compra para almacenar en nuestra plataforma, debes enviar el bloque "proveedor".

```json
comprobante: {
   .... 
   cliente: {   
      "documento_tipo":       "DNI",
      "documento_nro":        "1292963535",
      "razon_social":         "Pirulo",
      "nombre_fantasia":      "",
      "email":                "test@test.com",
      "domicilio":            "Av Sta Fe 123",
      "provincia":            "2",
      "codigo":               "CLO2",
      "envia_por_mail":       "S",
      "condicion_pago":       "214",
      "condicion_pago_otra":  "Cobrado en ventanilla",
      "condicion_iva":        "CF",
      "condicion_iva_operacion":        "CF",
      "reclama_deuda":        "S",
      "reclama_deuda_dias":   5,
      "reclama_deuda_repite_dias": 10,  
      "rg5329":                "N"
   }
}
```

En caso de enviar una compra, el nombre del bloque debe cambiar a "proveedor" en lugar de  "cliente"

```
comprobante: {
   .... 
   proveedor: {   
      "documento_tipo":       "DNI",
      "documento_nro":        "1292963535",
      "razon_social":         "Pirulo",
      "email":                "test@test.com",
      "domicilio":            "Av Sta Fe 123",
      "provincia":            "2",
      "codigo":               "CLO2",
      "envia_por_mail":       "S",
      "condicion_pago":       "214",
      "condicion_pago_otra":  "Cobrado en ventanilla",
      "condicion_iva":        "CF"
   }
}
```



#### Información de los campos a enviar:

<table data-header-hidden><thead><tr><th align="center">NOMBRE DEL CAMPO</th><th width="144.66666666666669" align="center">REQUERIDO?</th><th>INFO</th></tr></thead><tbody><tr><td align="center"><strong><code>documento_tipo</code></strong></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Valores Permitidos: <strong>CUIT , DNI, PASAPORTE, OTRO</strong><br><strong>Ejemplo: DNI</strong></td></tr><tr><td align="center"><code>documento_nro</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico, sin puntos ni guiones. Max 11 dígitos.<br><strong>Ejemplo: 30111222334</strong></td></tr><tr><td align="center"><code>razon_social</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico. Longitud máxima 255 caracteres.<br><strong>Ejemplo: Pirulo S.A</strong></td></tr><tr><td align="center"><code>email</code></td><td align="center">OPCIONAL</td><td>Campo alfanumérico. Longitud máxima 255 caracteres. Máximo 15 direcciones separadas por coma.<br><strong>Ejemplo: tusfacturas@vousys.com</strong></td></tr><tr><td align="center"><code>domicilio</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico. Longitud máxima 255 caracteres. <br><strong>Ejemplo: Av. Santa Fe 123</strong></td></tr><tr><td align="center"><code>provincia</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico según <a href="../parametros/tablas-de-referencia.md#provincias">tabla de referencia(*)</a>.<br><strong>Ejemplo: 2</strong></td></tr><tr><td align="center"><code>envia_por_mail</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Indica Si/No para el envio del comprobante por e-mail. Valores Permitidos: <strong>S , N</strong><br><strong>Ejemplo: S</strong></td></tr><tr><td align="center"><code>condicion_pago</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td><p>Campo numérico según <a href="../parametros/tablas-de-referencia.md#condiciones-de-venta">tabla de referencia</a>. Si envias la condición de pago "Otra" (214) se debe enviar obligatoriamente el campo <strong>condicion_pago_otra</strong> " con la descripción de dicha condición.</p><ul><li><strong>Ejemplo: "211"</strong></li></ul><p><strong>Éste dato  informativo sale impreso en el PDF</strong>  </p></td></tr><tr><td align="center">condicion_pago_otra</td><td align="center">OPCIONAL</td><td>Campo alfanumérico. Longitud máxima 100 caracteres. <strong>Ejemplo: Cobrado en ventanilla.</strong></td></tr><tr><td align="center"><code>condicion_iva</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico que indica la condición de iva, según <a href="../parametros/tablas-de-referencia.md#condiciones-frente-al-iva">tabla de referencia Condiciones ante el IVA</a>Valores Permitidos: <strong>CF, RI, M, E</strong><br><strong>Ejemplo: RI</strong></td></tr><tr><td align="center">condicion_iva_operacion</td><td align="center">OPCIONAL</td><td>Éste campo entra en vigencia a partir del 15/04/2025 mediante la RG 5616/2024 de AFIP/ARCA. Deberá consignarse la condición frente al IVA en que se realiza la operación. De no enviarse éste campo se enviará lo que se especifique en el campo "condicion_iva".</td></tr><tr><td align="center">codigo</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanúmerico de hasta 20 caracteres para referenciar a ese cliente. Éste dato debería ser único dentro de tu plataforma pero TusFacturasAPP  no realiza dicha verificación. Si existiera +1 con el mismo código podrías sufrir problemas al actualizar los datos. <strong>Ejemplo: "CLI2394"</strong></td></tr><tr><td align="center">rg5329</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td><p>Este campo te permite indicar si tu cliente es pasible de <a href="../faqs-or-rg5329.md">percepción IVA RG5329</a>.</p><p>Valores posibles: "S" o "N".</p></td></tr><tr><td align="center">reclama_deuda</td><td align="center">OPCIONAL</td><td>Indica SI/No para el envio del <a href="https://www.tusfacturas.app/caracteristicas-de-tus-facturas-electronica-clientes.html">recordatorio de pago</a> al cliente. Opciones validas: "S" o "N"</td></tr><tr><td align="center">reclama_deuda_dias</td><td align="center">OPCIONAL</td><td>En caso de haber habilitado el recordatorio de pago atrasado, se debe indicar cuantos dias pasados la fecha de vencimiento del comprobante se desea comenzar a recordar el pago adeudado. Se espera recibir un valor numerico indicando el número de días)</td></tr><tr><td align="center">reclama_deuda_repite_dias</td><td align="center">OPCIONAL</td><td>En caso de haber habilitado del recordatorio de pago atrasado, se debe indicar la frecuencia de cada cuantos dias se desea volver a recordar. Se espera recibir un valor numérico, indicando el número de días.</td></tr><tr><td align="center">nombre_fantasia</td><td align="center">OPCIONAL</td><td>Campo alfanumérico. Longitud máxima 255 caracteres.<br><strong>Ejemplo: Pirulo y Amigos</strong></td></tr></tbody></table>

{% hint style="info" %}
**Datos a tener en cuenta:**

* Si el cliente ya existe en tu base de clientes/proveedores en TusFacturasAPP por código o tipo + número de documento, la info será actualizada con los nuevos datos que envies, con excepción de los campos:  tipo de documento, número de documento y condición ante el IVA.
* Si queres enviar un comprobante a un consumidor final, sin especificar su nombre y DNI,  consulta la siguiente documentación de "[Facturas a Consumidor final sin especificar datos](facturas-a-consumidor-final-sin-especificar-datos.md)"
* Para casos de clientes del exterior, que posean **pasaporte**, tene en cuenta que AFIP/ARCA sólo permite el envío de números.&#x20;
* Te recomendamos utilizar el método de [consulta de CUITs](../consultas-varias-a-servicios-afip-arca/api-factura-electronica-afip-clientes-consultar-cuit-en-constancia-de-inscripcion.md) antes de emitir facturas, ya que el CUIT de tu cliente podría no estar activo, lo que podría generar inconvenientes con el fisco.
* Si no vas a gestionar los cobros de las facturas que emitas con TusFacturasAPP, env'a siempre el campo "reclama\_deuda": "N", ya que sino nuestra plataforma le enviará un email a tu cliente recordandole todas las facturas impagas.
* Si queres indicar en TusFacturasAPP que este comprobante ademas fue abonado, debes enviar el bloque de "pagos" con la información requerida, ya que el campo "condicion\_pago" es solo informativo. &#x20;
* En caso que no desees llevar el estado de pagado/impago en la plataforma, debes enviar el campo "reclama\_deuda" en "N", ya que sino la plataforma le recordará por e-mail a tu cliente de todos los comprobantes que adeuda.
{% endhint %}

### Estructura del bloque: "Detalle de conceptos"

El detalle de conceptos se compone de una lista de cada uno de los productos o servicios que vas a facturar. Cada producto o servicio único que incluyas en tu cmoprobante se considera un concepto diferente. Por ejemplo, si vendes 10 unidades de un producto, solo contarían como un concepto. **El límite máximo de conceptos por comprobante es de 130**.

{% hint style="info" %}
Nuestra plataforma gestiona los precios unitarios de productos y servicios con 3 decimales, mientras que los totales se calculan con 2 decimales. Debido a esto, pueden surgir pequeñas diferencias de facturación en aquellas empresas que trabajan con precios finales (IVA incluido).

Para garantizar la precisión fiscal, aplicamos el método de redondeo "Round half even" (redondeo bancario), siguiendo estrictamente los lineamientos de ARCA.

En el siguiente artículo sobre [ajustes, redondeos y precios sin IVA](https://ayuda.tusfacturas.app/es/articles/12548047-redondeos-ajustes-y-precios-sin-iva) te explicamos cómo funciona mediante un ejemplo práctico.
{% endhint %}

La estructura **de la lista de conceptos** a enviar es la siguiente:

{% code title="JSON" %}
```json
comprobante: {
   .... 
   detalle: [{
									"cantidad": "1.5",
									"afecta_stock": "N",
									"bonificacion_porcentaje": "0",
									"incluir_lista_precios_venta": "N",
									"leyenda": "",
									"producto": {
										"descripcion": "HUEVOS",
										"unidad_bulto": "30",
										"lista_precios": "MAPPLETS",
										"codigo": "MPH",
										"precio_unitario_sin_iva": "50",
										"impuestos_internos_alicuota": 0,
										"alicuota": "10.5",
										"unidad_medida": "7",
										"actualiza_precio":"S",
										"rg5329": "S"
									}
       				},
       				{
								"cantidad": "3",
								"afecta_stock": "S",
								"bonificacion_porcentaje": "50",
								"incluir_lista_precios_venta": "N",
								"leyenda": "En paquetes de 190gr",
								"producto": {
										"descripcion": "PALITOS SALADOS",
										"unidad_bulto": "30",
										"lista_precios": "SNACKS",
										"codigo": "PLi",
										"precio_unitario_sin_iva": "50",
										"impuestos_internos_alicuota": 0,
										"alicuota": "10.5",
										"unidad_medida": "7",
										"actualiza_precio":"S",
										"rg5329": "N"
									}
       				}
      ]
   } 
```
{% endcode %}

Los campos que debes enviar en cada concepto de la lista del bloque "detalle" son los siguientes:

<table data-header-hidden><thead><tr><th width="242.66666666666666">NOMBRE DEL CAMPO</th><th width="157" align="center">REQUERIDO?</th><th></th></tr></thead><tbody><tr><td><code>cantidad</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico positivo con 2 decimales. Separador de decimales: punto.<br><strong>Ejemplo: 1.50</strong></td></tr><tr><td><code>afecta_stock</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico de 1 posición. Valores posibles: "S" (si), "N" (no)<br><strong>Ejemplo: S</strong></td></tr><tr><td><mark style="color:blue;"><code>producto</code></mark></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Según estructura de producto que se detalla a continuación.</td></tr><tr><td><code>leyenda</code></td><td align="center">OPCIONAL</td><td>Campo alfanumérico. Longitud máxima 1000 caracteres. Contenido opcional. Será una descripción que acompañe al producto.<br><strong>Ejemplo: Blanca, cepillada</strong></td></tr><tr><td>bonificacion_porcentaje</td><td align="center">OPCIONAL</td><td>Si se ha aplicado un porcentaje de descuento sobre éste concepto, debe ser enviado. Es un campo númerico positivo con 2 decimales. El separador de decimales esperado es el punto. Ej: 25</td></tr><tr><td>incluir_lista_precios_venta</td><td align="center"><mark style="color:purple;">REQUERIDO</mark> <mark style="color:purple;">SOLO PARA COMPRAS</mark></td><td><p>Si estas enviando una compra, podes indicar que éste producto que compraste, se incorpore como un producto mas a los de tu lista de precios de venta. De esa manera podrás <a href="../productos/gestion-de-stock.md">gestionar el stock</a> tanto por la API como por la plataforma web.</p><p>Valores esperados: "S" o "N" </p><p>Ej: "S" </p></td></tr></tbody></table>

### Estructura de "producto"

Cada producto o servicio que envies sera almacenado en la lista de precios que se mantiene en nuestra plataforma, ademas de generar el comprobante requerido. A continuación podrás conocer que datos debes enviar:

<pre class="language-json"><code class="lang-json">{
    "descripcion":     "HUEVOS",
<strong>    "unidad_bulto":    "30",
</strong>    "lista_precios":   "MAPPLETS",
    "codigo":          "MPH",
    "precio_unitario_sin_iva":"50",
    "alicuota":      "10.5",
    "unidad_medida": "7",
    "impuestos_internos_alicuota": 0,
    "actualiza_precio": "N",
    "rg5329": "N"
}
</code></pre>



{% hint style="info" %}
**Datos a tener en cuenta:**

* Si el producto ya existía en tu base de productos de nuestra plataforma ( se valida que sea la misma lista de precios, código de producto y/o descripción del mismo), el mismo será actualizado por completo, con los nuevos datos que envíes, solo  si indicas que deseas actualizar el precio con el campo "actualiza\_precio":"S".  En caso de no querer actualizar el producto, si el mismo ya existía, se facturará con el nuevo precio y descripción que envíes, pero mantendrá sus datos anteriores.
*   Nuestra plataforma gestiona los precios unitarios de productos y servicios con 3 decimales, mientras que los totales se calculan con 2 decimales. Debido a esto, pueden surgir pequeñas diferencias de facturación en aquellas empresas que trabajan con precios finales (IVA incluido).

    Para garantizar la precisión fiscal, aplicamos el método de redondeo "Round half even" (redondeo bancario), siguiendo estrictamente los lineamientos de ARCA.

    En el siguiente artículo sobre [ajustes, redondeos y precios sin IVA](https://ayuda.tusfacturas.app/es/articles/12548047-redondeos-ajustes-y-precios-sin-iva) te explicamos cómo funciona mediante un ejemplo práctico.
* Si el comprobante que envías a facturar es de tipo C, todos los productos/conceptos que factures no deben llevar IVA y deberás enviar cada concepto con su precio final
* Si el comprobante que envías, es de tipo A o B, los productos o servicios que envíes a facturar, deben ser enviados siempre SIN IVA, porque el IVA se calcula del lado de nuestra plataforma en base al campo "alicuota" que envías. Conocé más de los tipos de comprobantes, [desde aquí ](que-tipos-de-comprobante-debo-puedo-emitir.md)
* En caso que alguno de tus conceptos cuente con un signo porcentual (%) en el nombre (ej:  Promo 20% OFF)  deberás reemplazarlo por los siguientes caracteres: **#\&#**&#x20;
* En caso que alguno de tus conceptos cuente con una nueva línea, en su nombre, o porque deba imprimirse en 2 líneas, deberás generar el salto de línea donde desees, ingresando los caracteres:  **#@#**&#x20;
* **Cómo calcular el IVA:**
  *   Si necesitas calcular cuánto vale tu producto sin IVA, te dejamos un cálculo rápido:&#x20;

      Precio del producto con 21% de IVA = 121

      Para saber el precio sin el 21% de IVA debes hacer:  121 / 1.21  = 100
  * Si quisieras saber cuanto es el precio de tu producto + 21% de IVA, debes hacer el siguiente cálculo:

&#x20;            Precio del producto sin 21% de IVA = 100

&#x20;            Para saber el precio con el 21% de IVA debes hacer:  100 x 1.21 = 121


{% endhint %}

Detalle de los campos a enviar:

<table data-header-hidden><thead><tr><th width="335.66666666666663">NOMBRE DEL CAMPO</th><th width="145" align="center">REQUERIDO?</th><th>INFO</th></tr></thead><tbody><tr><td><code>descripcion</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico. Longitud máxima 255 caracteres y mínima de 4 caracteres.<br><strong>Ejemplo: Papa blanca</strong></td></tr><tr><td><code>unidad_bulto</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico entero requerido. Indica la cantidad de unidades que componen un bulto. Éste dato se usa únicamente para los remitos para calcular la cantidad de bultos.  Valor minimo esperado: 1<br><strong>Ejemplo: 12</strong></td></tr><tr><td><code>lista_precios</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico. Longitud mínima de 4 caracteres y máxima 255 caracteres. Nombre de la lista de precios a la cual pertenece. No saldrá impreso en la factura pero es requerido.<br><strong>Ejemplo: Verdura Orgánica</strong></td></tr><tr><td><code>codigo</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanúmerico de hasta 20 caracteres para referenciar a ese producto. Éste dato debería ser único dentro de tu plataforma pero TusFacturasAPP no realiza dicha verificación. Si existiera +1 con el mismo código podrías sufrir problemas al actualizar los datos.<br><strong>Ejemplo: ABX780</strong></td></tr><tr><td><code>precio_unitario_sin_iva</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico positivo con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></td></tr><tr><td><code>alicuota</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td><p>Indica la alícuota de IVA con la que grava ese producto. Valores Permitidos:</p><p><strong>27, 21 , 10.5 , 0 , -1 ( para exento), -2 (no gravados)</strong><br><strong>Ejemplo: 10.5</strong></p></td></tr><tr><td><code>unidad_medida</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico que indica la unidad de medida, según<a href="../parametros/tablas-de-referencia.md#productos-unidades-de-medida-afip"> tabla de referencia Unidades de Medida(**).</a><br><strong>Ejemplo: 7</strong></td></tr><tr><td><code>actualiza_precio</code></td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Indica si se actualiza el precio del producto y sus datos adicionales (como ser la unidad de medida, código, unidades por bulto y otros datos adicionales), tomando como valor de referencia,la información enviada en el comprobante. Campo Alfabético, de 1 carácter. Valores permitidos: S (si) N (no). <strong>Ejemplo: S</strong></td></tr><tr><td><code>impuestos_internos_alicuota</code></td><td align="center">OPCIONAL</td><td>La alícuota que se cobra en concepto de impuestos internos para éste producto. Se permite una única alícuota por comprobante. Campo numérico positivo, con 2 decimales. ej: 10.5</td></tr><tr><td>rg5329</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td><p>Este campo te permite indicar si tu producto percibe la percepción IVA RG5329.</p><p>Valores posibles: "S" o "N".</p><p>Si envias el valor en "S", debes enviar el campo "actualiza_precio" tambien en "S".</p><p>Conocé cuando aplicar la RG5329 <a href="../faqs-or-rg5329.md">desde aquí</a></p></td></tr></tbody></table>

### Estructura del bloque "Comprobantes Asociados"

Los comprobantes asociados son requeridos a la hora de emitir una Nota de crédito o nota de débito. Encontrá la estructura e información de éste bloque desde la sección: [Notas de crédito/Notas de débito](api-factura-electronica-afip-notas-credito-debito.md)

### Estructura del bloque: "tributos"&#x20;

Cuando debas enviar percepciones de IVA o Ingresos Brutos (IIBB), incluye un array con la siguiente estructura dentro del bloque "comprobante". El límite es de 7 percepciones por comprobante.

Ejemplo:&#x20;

<pre class="language-json"><code class="lang-json">		 
<strong> "tributos": [	
</strong>			{
				"tipo" : 7,
				"regimen": 22,
				"base_imponible": 2000,
				"alicuota": 20,
				"total": 400				
			}, 		
			{
				"tipo" : 6,
				"regimen": 3,
				"base_imponible": 1000,
				"alicuota": 3,
				"total": 30
			}, 		
			{
				"tipo" : 6,
				"regimen": 3,
				"base_imponible": 1000,
				"alicuota": 1.5,
				"total": 15	
			},
			{
				"tipo" : 6,
				"regimen": 1,
				"base_imponible": 1000,
				"alicuota": 10,
				"total": 100
			}
		],  
</code></pre>

#### Información de los campos a enviar dentro de cada "tributo":

<table><thead><tr><th width="248">nombre del campo</th><th width="133.66666666666669">REQUERIDO</th><th>Valores esperados</th></tr></thead><tbody><tr><td>tipo</td><td><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico, según tabla de referencia <a data-mention href="../parametros/tablas-de-referencia.md#bloque-tributos-greater-than-tipos-de-percepcion-a-aplicar">#bloque-tributos-greater-than-tipos-de-percepcion-a-aplicar</a></td></tr><tr><td>regimen</td><td><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico, según tabla de referencia: <a data-mention href="../parametros/tablas-de-referencia.md#bloque-tributos-greater-than-regimen-de-percepcion">#bloque-tributos-greater-than-regimen-de-percepcion</a></td></tr><tr><td>base_imponible</td><td><mark style="color:purple;">REQUERIDO</mark></td><td> Campo numérico positivo con hasta 2 decimales, donde se indica la base imponible sobre la cual se aplica la percepción.</td></tr><tr><td>alicuota</td><td><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico con hasta 2 decimales, donde se indica la alícuota de dicha percepción</td></tr><tr><td>total</td><td><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico positivo de hasta 2 decimales, con el importe total de la percepción a aplicar.</td></tr></tbody></table>

### Estructura de "RG Especiales"&#x20;

Si la empresa, opera bajo alguna RG particular, se deberá enviar un array con los datos adicionales, según se especifican en la [tabla de Datos adicionales para RG Especiales](../parametros/tablas-de-referencia.md#datos-opcionales-para-rg-especiales).

Ten en cuenta que solo podrás aplicar a un solo [regimen](../parametros/tablas-de-referencia.md#datos-opcionales-para-rg-especiales) , por cada comprobante que emitas.

{% code title="JSON" %}
```
comprobante: {
   .... 
   "rg_especiales":   
  {   "regimen" : "RG 4004-E",
      "datos"  : 
               [{
                   "id"      :    18,
                   "valor"  :    "PRUEBA "
                },
                {
                  "id"      :    19,
                 "valor"  :    "PRUEBA (2) "
                 }]
   } 
 }
```
{% endcode %}

#### Datos a tener en cuenta:

{% hint style="info" %}
* TusFacturasAPP no realiza validaciones sobre éstos campos. Todas las validaciones son realizadas por la propia AFIP en caso que corresponda.
* Si alguno de los items enviados posee un valor vacio, éste item no será procesado.
{% endhint %}

#### Información de los campos a enviar en el array de "datos":

<table data-header-hidden><thead><tr><th width="214"></th><th width="151.66666666666669">REQUERIDO</th><th></th></tr></thead><tbody><tr><td><code>id</code></td><td><mark style="color:purple;">REQUERIDO</mark></td><td>Campo númerico. Valores esperados según Tabla de referencia: <a href="../parametros/tablas-de-referencia.md#regimenes-posibles-para-el-bloque-rg_especiales"> Datos Opcionales para RG Especiales</a></td></tr><tr><td><code>valor</code></td><td><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico.</td></tr></tbody></table>

### Estructura de "pagos"    <a href="#estructuradepagos" id="estructuradepagos"></a>

Si quisieras reflejar junto al envío del comprobante, el pago parcial o total del mismo, debes enviar un bloque, dentro del comprobante, llamado "**pagos**" con la estructura como se detalla a continuación. Dado que la plataforma gestiona la contabilidad en las cuentas corrientes en pesos, el importe que envies debe corresponder al total de tu comprobante en pesos argentinos.

**Éste bloque es opcional.**

Los pagos que informes, se usan solo para la gestión interna de nuestra plataforma y tu cliente no lo verá reflejado en el PDF del comprobante que emitiste, ya que el único objetivo que tiene éste bloque es nutrir la cuenta corriente de tu cliente, con el pago realizado.

#### Datos a tener en cuenta:

{% hint style="info" %}
* **NO** podrás enviar los siguientes medios de pago: cheques y detalle de retenciones.
* Se realizará una validación del total que se indique, contra la sumatoria de los medios de pago detallados, previo al guardado del comprobante.
* El total de los pagos **NO** debe superar el importe total del comprobante, pero si puede ser inferior, para indicar que el comprobante recibió un pago parcial.
{% endhint %}

#### Información de los campos que componen el **bloque "pagos"**

<table><thead><tr><th>Nombre del campo</th><th width="141.66666666666669" align="center">REQUERIDO</th><th>Detalle</th></tr></thead><tbody><tr><td>formas_pago</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>array con multiples items, según estructura que se detalla a continuación</td></tr><tr><td>total</td><td align="center"><mark style="color:purple;">REQUERIDO</mark></td><td>Campo numérico positivo con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></td></tr></tbody></table>

#### Información de los campos que componen el **array de  "formas\_pago"**

| Nombre del campo |                   Requerido                  | Detalle                                                                                                                                                                                 |
| ---------------- | :------------------------------------------: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| descripcion      | <mark style="color:purple;">REQUERIDO</mark> | El nombre del medio de pago elegido para cancelar el comprobante. 255 caracteres max. En caso que el medio de pago, no exista en nuestra plataforma, será dado de alta automáticamente. |
| importe          | <mark style="color:purple;">REQUERIDO</mark> | <p>Campo numérico positivo con 2 decimales. separador de decimales: punto<br><strong>Ejemplo: 645.67</strong></p>                                                                       |

#### Ejemplo del JSON a enviar.

{% code title="JSON" %}
```
comprobante: {
   .... 
   "pagos" : 
   {
	"formas_pago" : [ 
			{"descripcion" : "VISA DB", "importe" : 0.6},
			{"descripcion" : "MercadoPago", "importe" : 50}
			], 
	"total": 50.6
   }, 
 }
```
{% endcode %}



### Estructura de "tags"

Si quisieras enviar tags para agregar a tus comprobantes, a modo de etiqueta informativa, debes enviar un array con el nombre de cada una de éstas.

Cada tag, debe ser un campo alfanumérico de hasta 255 caracteres y puedes enviar hasta 50 tags por comprobante.

#### Ejemplo del JSON a enviar.

{% code title="JSON" %}
```
comprobante: {
   .... 
   "tags" :  [ "etiqueta1", "etiqueta2"],   
 }
```
{% endcode %}

### Estructura de "datos\_informativos"

Dentro de este bloque deberá enviarse según corresponda, la información requerida por AFIP/ARCA en carácter informativo. Éstos datos no tienen ninguna relevancia dentro de la gestión de TusFacturasAPP.

#### Ejemplo del JSON a enviar.

{% code title="JSON" %}
```
comprobante: {
   .... 
   "datos_informativos" :  {
         "paga_misma_moneda": "N"
      } ,   
 }
```
{% endcode %}

#### Información de los campos que componen el **bloque "datos\_informativos"**

<table><thead><tr><th>Nombre del campo</th><th align="center">Requerido</th><th>Detalle</th></tr></thead><tbody><tr><td><pre><code>paga_misma_moneda
</code></pre></td><td align="center">OPCIONAL</td><td><p>Éste dato entra en vigencia el 15/04/2025 según la RG5616/2024 y deberá enviarse "N" para indicar "No informa" o "S" para indicar "Si". </p><p>En caso de enviarse con el valor "S", la moneda enviada debe ser diferente al Peso Argentino y la cotización debe ser la oficial provista por AFIP/ARCA desde <a href="../consultas-varias-a-servicios-afip-arca/cotizacion-monedas-afip.md">éste método</a></p></td></tr></tbody></table>

### 💡 Soporte y Recursos

¿Tenes preguntas sobre la API? Visita nuestro Centro de Ayuda en [ayuda.tusfacturas.app](https://ayuda.tusfacturas.app) para acceder a guías paso a paso y solución de problemas o escribnos a api@tusfacturas.app

