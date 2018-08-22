---
description: >-
  Mediante éste método podrás generar comprobantes de venta o de compra. Los
  mismos quedarán almacenados de manera automática en nuestra plataforma, para
  que puedas consultarlos en cualquier momento.
---

# Nuevo comprobante de Venta

{% hint style="info" %}
Poder utilizar la API debes [estar registrado](https://www.tusfacturas.com.ar/registrarme-factura-electronica.html). 

Mientras estés en etapa de testing, configurá tu CUIT con un punto de venta irreal \(Ej: 679\), y usa ese CUIT de prueba para facturar, la respuesta que recibirás es la misma que si facturas  contra AFIP, solo que los campos CAE y Vencimiento del CAE te retornaran vacios.  Una vez que hayas probado todos los métodos, crea el nuevo CUIT+punto de venta y lo enlazas con AFIP.

Ten en cuenta que al registrarte, te asignamos un plan gratuito que te permite emitir 5 comprobantes por mes y una vez vencido tu período de prueba, debes contratar algún plan API de los que tenemos disponibles aquí .

En caso que requieras 10 días más para el desarrollo, contáctanos a tusfacturas@vousys.com
{% endhint %}

{% api-method method="post" host="https://www.tusfacturas.com.ar/app/api/" path="v2/facturacion/nuevo" %}
{% api-method-summary %}
Nuevo comprobante de Venta
{% endapi-method-summary %}

{% api-method-description %}
Charset: UTF-8   
Tipo de dato esperado: JSON  
  
Éste metodo te permite generar comprobantes de venta, ya sea Facturas electrónicas AFIP, como Notas de débito o de crédito.  
Nuestra plataforma te permite emitir comprobantes de tipo A, B, C, E, M  
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="usertoken" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apisecret" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="apikey" type="string" required=true %}
Tus credenciales de acceso
{% endapi-method-parameter %}

{% api-method-parameter name="comprobante" type="object" required=true %}
**fecha**    Campo fecha. Para facturación afip deberá ser la fecha del día. Formato esperado: dd/mm/aaaa. Ejemplo: 13/05/2018   
**tipo**    Campo alfabético según tabla de referencia de Tipos de comprobantes\(\*\*\*\).    
**operacion**    Campo alfanumérico. Longitud 1 caracter. Indica si envia una factura de venta \(V\) o de compra \(C\). Valores Permitidos: V, C Ejemplo: V   
**idioma**    Campo numérico. Longitud 1 caracter. Indica el idioma en que se imprimira el PDF del comprobante. Valores Permitidos: 1 = Español, 2= Ingles    
**punto\_venta**    Campo numérico entero. Longitud máxima 4 digitos.   
**moneda**    Campo alfanumérico de 3 Digitos según tabla de referencia de Monedas .  
**cotizacion**    Campo numérico con 2 decimales. Puede obtener la cotización del día según AFIP desde nuestro método de consulta de cotización Ejemplo: 15.20 **numero**    El numero del comprobante a generar. Campo numérico entero. Longitud máxima 8 digitos. La numeración será validada internamente previa generación del comprobante contra AFIP. Ejemplo: 4567 **periodo\_facturado\_desde**     Campo fecha. Contenido opcional. Formato esperado: dd/mm/aaaa.   
**periodo\_facturado\_hasta**    Campo fecha. Contenido opcional. Formato esperado: dd/mm/aaaa.  
**rubro**    Campo alfanumérico. Longitud máxima 255 caracteres. Indica el rubro al cual pertenecerá el comprobante. Ésta información no saldrá impresa en el comprobante.   
**rubro\_grupo\_contable**    Campo alfanumérico. Longitud máxima 255 caracteres. Indica el grupo contable al que pertenece el rubro. Ésta información no saldrá impresa en el comprobante.   
**abono**: Campo alfabético, longitud máxima 1 caracter. Valores permitidos S \(si\) o N \(no\). Indica si el comprobante a generar es un abono recurrente.  
**abono\_frecuencia**: Campo numerico sin decimales. Indica la frecuencia en meses con la que debe generarse la recurrencia del abono.  
**abono\_hasta**: Campo fecha \(mm/yyyy\). Longitud maxima 7. Indica el mes y año hasta el cual debe generarse el abono recurrente.  
**abono\_actualiza\_precios**: Campo alfabético, longitud máxima 1 caracter. Valores permitidos S \(si\) o N \(no\). Indica si cada vez que se genera el abono, se actualiza los precios de los productos contra el precio actual de la lista de precios.  
**detalle**  Lista de conceptos a facturar. Objeto JSON Según estructura que se detalla a continuación  
**fex**    Solo para comprobantes de tipo E. Según estructura detallada en: Factura electronica de exportacion".   
**bonificacion**    Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor aplicado en concepto de bonificación sin IVA Ejemplo: 12.67. Tener en cuenta para el cálculo que la bonificación se aplica sobre el primer subtotal SIN IVA y se lo gravará con el importe de IVA que le corresponda.   
**leyenda\_gral**    Campo alfanumérico. Longitud máxima 255 caracteres. Contenido opcional. Es una leyenda general que saldrá impresa en el bloque central de productos del comprobante Ejemplo: Aplica plan 12 cuotas sin interes.   
**comentario**: Campo alfanumerico, opcional. Longitud máxima: 255 caracteres. Éste campo no saldrá impreso en la factura.  
**percepciones\_iibb**    Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario de la percepción de ingresos brutos realizada Ejemplo: 142.67   
**percepciones\_iva**    Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario de la percepción de IVA realizada Ejemplo: 42.67   
**exentos**    Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario en concepto de exentos. Solo para comprobantes A y M Ejemplo: 72.67   
**nogravados**    Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario en concepto de no gravados. Solo para comprobantes A y M Ejemplo: 62.67 **impuestos\_internos**    Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario en concepto de impuestos internos Ejemplo: 2.67   
**total**    Campo numérico con 2 decimales. separador de decimales: punto. Indica el valor monetario de la sumatoria de conceptos incluyendo IVA e impuestos. Ejemplo: 12452.67
{% endapi-method-parameter %}

{% api-method-parameter name="cliente" type="object" required=true %}
**documento\_tipo**:   Valores Permitidos: CUIT , DNI **documento\_nro**:    Campo numérico, sin puntos ni guiones.    
**razon\_social** :   Campo alfanumérico. Longitud máxima 255 caracteres.    
**email**:    Campo alfanumérico. Longitud máxima 255 caracteres.   domicilio:    Campo alfanumérico. Longitud máxima 255 caracteres.   
**provincia**:    Campo numérico según tabla de referencia\(\*\).    
**envia\_por\_mail**:    Indica Si/No para el envio del comprobante por e-mail. Valores Permitidos: S , N **condicion\_pago**:    Campo numérico que indica la cantidad de dias en los cuales vence el plazo de pago. Valores Permitidos: 0,30,60,90    
**condicion\_iva**:    Campo numérico que indica la condicion de iva, según tabla de referencia Condiciones ante el IVA\(\*\*\).  
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Si el comprobante se ha podido generar sin problemas  se devolverá la variable "error" = "N".  
En caso de detectar error, la variable "error" contendrá una "S" y "errores" una lista con todos los errores encontrados   
  
Importante:  
  
- El CAE es el Código de Autorización Electrónico que otorga AFIP como confirmación de la creación del comprobante. Es un dato importante para almacenar como respuesta.  
  
- Los CAE tienen fecha de vencimiento.  
  
- Contemplar en la respuesta que el número de CAE es un texto.  
  
  
{% endapi-method-response-example-description %}

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```javascript
{
    "error":     "N",
     "errores": [ ""],    
     "rta":      "El comprobante NOTA DE DEBITO B 0002-00000006 (MI CUIT) se ha guardado correctamente",    
     "cae":      "65301278726386",    
     "vencimiento_cae":"07\/08\/2015",    
     "vencimiento_pago":"27\/08\/2015",    
     "comprobante_pdf_url": "https://www.tusfacturas.com.ar/app/comprobantes/30111111111-1292963535-0002-00000006.pdf"
  }  
  
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
Ten en cuenta a la hora de calcular el total, que las bonificaciones están gravadas con IVA 
{% endhint %}

### Ejemplo de JSON que debes enviar

```text
{
"usertoken" :  "jajajja8c8bf67c884e1405e26c03c85",
"apikey"    :  "9991",
"apitoken"  :  "kkakak208a17cdfc4e4741437baddaa6",
"cliente"   :
                {   "documento_tipo":       "DNI",
                    "documento_nro":        "1292963535",
                    "razon_social":         "Pirulo",
                    "email":                "test@test.com",
                    "domicilio":            "Av Sta Fe 123",
                    "provincia":            "2",
                    "envia_por_mail":       "S",
                    "condicion_pago":       "30",
                    "condicion_iva":        "CF"
                },

"comprobante":  {

                "fecha":                    "28\/07\/2015",
                "tipo":                     "NOTA DE DEBITO B",
                "moneda":                   "DOL",
               "idioma":                   "1",
                "cotizacion":               "15.20",
                "operacion":                "V",
                "punto_venta":              "2",
                "numero":                   "6",
                "periodo_facturado_desde":  "27\/07\/2015",
                "periodo_facturado_hasta":  "30\/07\/2015",
                "rubro":                    "Servicios web",
                "rubro_grupo_contable":     "servicios",
                "abono": "S",
                "abono_frecuencia": "2",
                "abono_hasta":"10/2019",
                "abono_actualiza_precios": "N",
                "detalle":
                            [
                                {
                                    "cantidad":"1",
                                    "afecta_stock": "N",
                                    "producto":
                                            {"descripcion":     "PAPAS",
                                             "unidad_bulto":    "10",
                                             "lista_precios":   "MI LISTA DE PRECIOS",
                                             "codigo":          "",
                                             "precio_unitario_sin_iva":"100.45",
                                             "alicuota":      "21",
                                             "unidad_medida": "7",
                                             "actualiza_precio": "S"
                                             },
                                    "leyenda":"blanca, cepillada"
                                },


                                {
                                    "cantidad":"1.5",
                                    "afecta_stock": "N",
                                    "producto":
                                            {"descripcion":     "HUEVOS",
                                             "unidad_bulto":    "30",
                                             "lista_precios":   "MAPPLETS",
                                             "codigo":          "MPH",
                                             "precio_unitario_sin_iva":"50",
                                             "alicuota":      "10.5",
                                             "unidad_medida": "7",
                                             "actualiza_precio": "N"
                                             },
                                    "leyenda":""
                                },

                                {
                                    "cantidad":"2",
                                    "afecta_stock": "S",
                                    "producto":
                                            {"descripcion":     "ZANAHORIA",
                                             "unidad_bulto":    "50",
                                             "lista_precios":   "MI LISTA DE PRECIOS",
                                             "codigo":          "ZNH1",
                                             "precio_unitario_sin_iva":"200",
                                             "alicuota":      "21",
                                             "unidad_medida": "7"
                                             },
                                    "leyenda":""
                                }

                            ],
                "bonificacion":             "120",
                "leyenda_gral":             "Segun Orden de compra III1333",
                "comentario":               "Factura correspondiente al servicio XX",
                "percepciones_iibb":        "0",
                "percepciones_iva":         "0",
                "exentos":                  "0",
                "nogravados":               "0",
                "impuestos_internos":       "0",
                "total":                    "543.22"
        }
}


```

### Estructura de  "Cliente"

Para poder generar el comprobante, debes enviar un detalle de todos los datos del cliente según se informa a continuación.

```text
{   
"documento_tipo":       "DNI",
"documento_nro":        "1292963535",
"razon_social":         "Pirulo",
"email":                "test@test.com",
"domicilio":            "Av Sta Fe 123",
"provincia":            "2",
"envia_por_mail":       "S",
"condicion_pago":       "30",
"condicion_iva":        "CF"
}
```

{% hint style="info" %}
Si el cliente ya existia en la base de datos de www.tusfacturas.com.ar será actualizado con los nuevos datos, salvo Tipo y Nro de documento y condicion ante el IVA
{% endhint %}

Información de los campos a enviar:

| `documento_tipo` | Valores Permitidos: **CUIT , DNI** **Ejemplo: DNI** |
| :--- | :--- |
| `documento_nro` | Campo numérico, sin puntos ni guiones. **Ejemplo: 30111222334** |
| `razon_social` | Campo alfanumérico. Longitud máxima 255 caracteres. **Ejemplo: Pirulo S.A** |
| `email` | Campo alfanumérico. Longitud máxima 255 caracteres. **Ejemplo: tusfacturas@vousys.com** |
| `domicilio` | Campo alfanumérico. Longitud máxima 255 caracteres. **Ejemplo: Av. Santa Fe 123** |
| `provincia` | Campo numérico según [tabla de referencia\(\*\)](../tablas-de-referencia.md#provincias). **Ejemplo: 2** |
| `envia_por_mail` | Indica Si/No para el envio del comprobante por e-mail. Valores Permitidos: **S , N** **Ejemplo: S** |
| `condicion_pago` | Campo numérico que indica la cantidad de dias en los cuales vence el plazo de pago. Valores Permitidos: **0,30,60,90**  **Ejemplo: 30** |
| `condicion_iva` | Campo numérico que indica la condicion de iva, según [tabla de referencia Condiciones ante el IVA\(\*\*\)](../tablas-de-referencia.md#condiciones-ante-el-iva). Valores Permitidos: **CF, RI, M, E**  **Ejemplo: RI** |

### Estructura de "Detalle de conceptos"

El detalle de conceptos se compone de una lista de cada uno de los productos que vas a facturar.

La estructura de cada concepto a enviar es la siguiente:

{% code-tabs %}
{% code-tabs-item title="JSON" %}
```text
{
	"cantidad": "1.5",
	"afecta_stock": "N",
	"producto": {
		"descripcion": "HUEVOS",
		"unidad_bulto": "30",
		"lista_precios": "MAPPLETS",
		"codigo": "MPH",
		"precio_unitario_sin_iva": "50",
		"alicuota": "10.5",
		"unidad_medida": "7",
		"actualiza_precio":"S"
	},
	"leyenda": ""
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Los campos que debes enviar son los siguientes:

| `cantidad` | Campo numérico con 2 decimales. Separador de decimales: punto. **Ejemplo: 1.50** |
| :--- | :--- |
| `afecta_stock` | Campo alfanumérico de 1 posición. Valores posibles: "S" \(si\), "N" \(no\)  **Ejemplo: S** |
| `producto` | Según estructura de producto |
| `leyenda` | Campo alfanumérico. Longitud máxima 100 caracteres. Contenido opcional. Será una descripción que acompañe al producto.  **Ejemplo: Blanca, cepillada** |



### Estructura de "Concepto /  Producto"

{% hint style="info" %}
Si el producto ya existia en la base de datos de nuestra plataforma, para la lista de precios indicada, será actualizado con los nuevos datos.
{% endhint %}

```text
{
"descripcion":     "HUEVOS",
"unidad_bulto":    "30",
"lista_precios":   "MAPPLETS",
"codigo":          "MPH",
"precio_unitario_sin_iva":"50",
"alicuota":      "10.5",
"unidad_medida": "7",
"actualiza_precio": "N"
}
```

Los campos que debes enviar son los siguientes:

| `descripcion` | Campo alfanumérico. Longitud máxima 255 caracteres. **Ejemplo: Papa blanca** |
| :--- | :--- |
| `unidad_bulto` | Campo numérico entero requerido. Indica la cantidad de unidades que componen un bulto. Valor minimo esperado: 1 **Ejemplo: 12** |
| `lista_precios` | Campo alfanumérico. Longitud máxima 255 caracteres. Nombre de la lista de precios a la cual pertenece. No saldrá impreso en la factura pero es requerido. **Ejemplo: Verdura Orgánica** |
| `codigo` | Campo alfanumérico. Longitud máxima 10 caracteres. campo Opcional **Ejemplo: ABX780** |
| `precio_unitario_sin_iva` | Campo numérico con 2 decimales. separador de decimales: punto **Ejemplo: 645.67** |
| `alicuota` | Indica la alicuota de IVA con la que grava ese producto. Valores Permitidos: **27, 21 , 10.5 ,  0  y -1 \( para exento\)** **Ejemplo: 10.5** |
| `unidad_medida` | Campo numérico que indica la unidad de medida, según[ tabla de referencia Unidades de Medida\(\*\*\). ](../tablas-de-referencia.md#productos-unidades-de-medida-afip) **Ejemplo: 7** |
| `actualiza_precio` | Indica si se actualiza el precio del producto, en la base productos, tomando como valor de referencia el enviado en el comprobante. Campo Alfabético, de 1 caracter. Valores permitidos: S \(si\) N \(no\).          **Ejemplo: S** |
|  |  |



