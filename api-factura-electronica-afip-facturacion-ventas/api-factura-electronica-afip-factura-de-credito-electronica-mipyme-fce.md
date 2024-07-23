---
description: >-
  Emití con la API de TusFacturas.app, facturas, notas de débito y notas de
  crédito A,B y C de los comprobantes tipo Factura de crédito electrónica Mi
  Pyme.
---

# Comprobantes de tipo: Factura de Crédito Electrónica MiPyme (FCE)

TusFacturasAPP es un proveedor SaaS líder de servicios de facturación electrónica en Argentina, que permite a empresas de todos los tamaños emitir comprobantes fiscales válidos de manera rápida, segura y cumpliendo con todas las regulaciones de la AFIP.

### ¿Qué podes hacer con la API para facturación AFIP?

Integra fácilmente la facturación electrónica en tu software con la API de TusFacturasAPP. Emite comprobantes fiscales válidos desde tu sistema y obtén respuestas inmediatas de la AFIP.

<figure><img src="../.gitbook/assets/157.webp" alt="SDK AFIP. TusFacturasAPP API Factura Electronica AFIP. AFIP WS"><figcaption></figcaption></figure>

### ¿Cómo empiezo?

Te sugerimos revisar la guia de [¿Cómo empiezo?](../como-empiezo.md) . Una vez configurada tu cuenta y creado tu CUIT+Punto de venta (PDV) en [TusFacturasAPP](https://www.tusfacturas.app), podrás comenzar a emitir facturas electrónicas AFIP Argentina válidas.&#x20;

Comenza ya a cumplir con las regulaciones fiscales y brinda una experiencia de facturación digital eficiente a tus clientes. [Solicita acceso](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html) a nuestra API de facturación electrónica.A continuación te mostramos la estructura de los datos que se requieren para generar un comprobante de tipo exportación, ya sea NC, ND o FACTURA.

### ¿Qué son los Comprobantes MiPyme AFIP?

Los Comprobantes MiPyme AFIP son una modalidad de facturación electrónica simplificada, diseñada específicamente para **micro, pequeñas y medianas empresas (MiPyMEs)**.

#### **¿Qué los diferencia de las facturas electrónicas comunes?**

* **Beneficios fiscales:** Las MiPyMEs que emiten Comprobantes MiPyme pueden acceder a ciertos beneficios fiscales, como la **reducción de alícuotas de IVA** y la **exención de retenciones de Ganancias**.

#### **¿Quiénes pueden emitir Comprobantes MiPyme?**

Todas las MiPyMEs que se encuentran inscriptas en la AFIP y que cumplan con los requisitos establecidos por el organismo pueden emitir Comprobantes MiPyme.

#### **¿Cómo empezar a emitir Comprobantes MiPyme?**

Para empezar a emitir Comprobantes MiPyme, las MiPyMEs deben:

* **Inscribirse en el servicio "Factura Electrónica MiPyme"** en la AFIP.
* **Contratar un proveedor de servicios tecnológicos homologado** por la AFIP, como lo es [TusFacturas.app](https://www.tusfacturas.app)

Ten en cuenta que éste tipo de comprobantes MiPyme,  requieren de un tratamiento adicional gestionado desde la web de AFIP para su autorización/aceptación/anulación. Consultá con tu contador/a el procedimiento indicado en la ley.

Para más información acerca de los comprobantes MiPyme, sugerimos leer la información provista por  AFIP, en el [micrositio de Facturas de crédito MiPyme](https://servicioscf.afip.gob.ar/facturadecreditoelectronica/)

### API para Comprobantes MiPyme&#x20;

**En esta guía encontrarás:**

* Los requerimientos específicos para cada tipo de solicitud.
* Los datos exactos que debes enviar para generar nuevos comprobantes de venta.
* Documentación completa y ejemplos de código para una integración rápida y eficiente.

Consultá la descripción completa del servicio [API Facturación AFIP](./).

#### **Información importante sobre los Comprobantes MiPyme:**

* **Información adicional obligatoria:** Estos comprobantes requieren información adicional dentro del bloque "rg\_especiales".
* **Aplicabilidad:** Se utilizan solo para ciertos receptores a partir de un monto determinado, que varía según la operación.
* **Determina el tipo de comprobante:** Accede a [nuestra guía](api-factura-electronica-afip-or-como-se-si-emitir-una-factura-mipyme-o-una-comun.md) para saber si debes emitir una factura MiPyme o una factura común.

**Comenza a crear Comprobantes MiPyme hoy mismo y simplifica tu proceso de facturación electrónica.**

### Estructura del bloque "rg\_especiales"

El bloque de "rg\_especiales" debe especificar el [regimen al que pertenece](../parametros/tablas-de-referencia.md#regimenes-posibles-para-el-bloque-rg\_especiales) éste comprobante y enviar información asociada a éste regimen, dentro del bloque "datos".

{% code title="Ejemplo del JSON" %}
```
comprobante: {
   .... 
   "rg_especiales":   
  {   "regimen" : "RG 4004-E",
      "datos"  : 
            [
               {
                   "id"      :    2101,
                   "valor"  :    "12313123132133"
                },
                {
                  "id"      :    27,
                 "valor"  :    "SCA"
                 }
           ]
   } 
 }
```
{% endcode %}

#### Estructura del array "datos"

Cada item del array debe estar compuesto por los siguientes campos:

<table data-header-hidden><thead><tr><th width="214"></th><th width="151.66666666666669">REQUERIDO</th><th></th></tr></thead><tbody><tr><td><code>id</code></td><td><mark style="color:purple;">REQUERIDO</mark></td><td>Campo númerico, segun se detalla a continuación. </td></tr><tr><td><code>valor</code></td><td><mark style="color:purple;">REQUERIDO</mark></td><td>Campo alfanumérico.</td></tr></tbody></table>

Las opciones posibles de "Id" para enviar dentro del array de "datos" son las siguientes:

<table><thead><tr><th>Descripcion del campo</th><th width="112">Id a enviar</th><th width="145">¿Requerido?</th><th>Detalle</th></tr></thead><tbody><tr><td>CBU emisor</td><td>2101</td><td><mark style="color:purple;"><strong>REQUERIDO</strong></mark> <em>(EXCEPTO NC Y ND)</em></td><td>CBU numérico de 22 caracteres (salvo que envies el ALIAS del CBU)</td></tr><tr><td>Referencia Comercial</td><td>23</td><td>OPCIONAL</td><td>Texto. puede identificar una o varias Referencias Comerciales según corresponda - no repetir el valor.</td></tr><tr><td>CBU Alias del emisor</td><td>2102</td><td>OPCIONAL</td><td>El valor correcto es un ALIAS alfanumerico Longitud de 6 a 20 caracteres, letras de la 'a' a la 'Z', numeros del '0' al '9', caracteres especiales: punto ( . ) o guion medio ( - )</td></tr><tr><td>Anulación</td><td>22</td><td><mark style="color:purple;"><strong>REQUERIDO (SOLO PARA NC Y ND)</strong></mark></td><td>Solo debe ser enviado para las Notas de crédito/debito y el valor esperado es : S o N. Indica si el comprobante fue rechazado por el receptor.</td></tr><tr><td>Referencia de transferencia</td><td>27</td><td><mark style="color:purple;"><strong>REQUERIDO (solo para FACTURAS)</strong></mark></td><td>A partir del 1/4/2021 se deberá enviar éste campo con las siguiente siglas posibles: "SCA" o "ADC" . "SCA se usa para indicar: "TRANSFERENCIA AL SISTEMA DE CIRCULACION ABIERTA" y "ADC" para enviar "AGENTE DE DEPOSITO COLECTIVO"</td></tr><tr><td></td><td></td><td></td><td></td></tr></tbody></table>

{% hint style="info" %}
Datos a tener en cuenta:



* TusFacturasAPP no realiza validaciones sobre éstos campos. Todas las validaciones son realizadas por la propia AFIP en caso que corresponda.
* Si alguno de los items enviados posee un valor vacio, éste item no será procesado.


{% endhint %}

## Ejemplo de factura de crédito electrónica  MiPyme (FCE)



```json
JSON
{
   "usertoken":"xxxx",
   "apikey":"xxxx",
   "apitoken":"xxxxx",
   "cliente":{
      .....
   },
   "comprobante":{
      ......,
      "rg_especiales":{
         "regimen":"Factura de Crédito Electrónica MiPyMEs (FCE)",
         "datos":[
            {
               "id":2101,
               "valor":"1234567890123456789011"
            },
            {
               "id":23,
               "valor":"Prueba"
            },
            {
               "id":27,
               "valor":"SCA"
            }
         ]
      }
   }
}
```

### Nota de crédito electrónica A MiPyme (FCE)

En caso que debas anular un comprobante, la operación correcta es emitir una Nota de crédito. Sugerimos revisar la documentación de las [Notas de crédito / Notas de débito](api-factura-electronica-afip-notas-credito-debito.md) para más información.

{% hint style="info" %}
**Datos a tener en cuenta:**&#x20;

* Para éstas NC y ND,  **AFIP no requiere el envio del CBU ni ALIAS**
* Debes enviar dentro del bloque de "[rg\_especiales](./#estructura-de-rg-especiales)", el dato id #22 con el valor S o N según corresponda. Consultá con tu estudio contable para que te asesoren al respecto.
* Los comprobantes que se asocien deben haberse emitido en la misma moneda en que se esta emitiendo la nota de crédito/débito.
* La fecha del comprobante que asocies debe ser menor o igual a la fecha del comprobante que estas queriendo emitir. Tené en cuenta que AFIP realiza validaciones en cuanto a la fecha de los comprobantes que asocies, ya que no se permiten notas de crédito a comprobantes con  +15 días.
{% endhint %}

{% code title="Ejemplo JSON de una Nota de crédito " %}
```json
{
	"usertoken": "xxx",
	"apikey": "xxxx",
	"apitoken": "xxxx",
	"cliente": {
		.....
	},
	"comprobante": {
		.....,
        	"rg_especiales":   
            		{  
            		 "regimen" : "Factura de Crédito Electrónica MiPyMEs (FCE)",
                 	"datos"  : 
                           [ 
                            	{
                             	 "id"      :    22,
                             	"valor"  :    "S"
                             	} 
                	   ]
            		}, 
	         "comprobantes_asociados": [{
			"tipo_comprobante": "FACTURA DE CREDITO ELECTRONICA MiPyME (FCE) A",
			"punto_venta": "3",
			"numero": 1,
			"comprobante_fecha": "07/07/2019",
			"cuit": 1111111111111
		}]
	}
}

```
{% endcode %}

{% hint style="info" %}
Ten en cuenta que TusFacturas.app no realiza validaciones con respecto a los datos enviados referente a la RG MiPyme. Las validaciones se realizan exclusivamente del lado de AFIP, previa generación del comprobante.
{% endhint %}

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

[\
](https://app.gitbook.com/@tusfacturas/s/api-factura-electronica-afip/facturacion-nuevo-comprobante/factura-electronica-afip-exportacion)
