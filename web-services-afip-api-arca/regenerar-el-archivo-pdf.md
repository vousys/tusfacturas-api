---
description: >-
  La API de facturación electrónica ARCA de TusFacturasAPP te permite regenerar
  el archivo pdf las veces que necesites.
icon: code
---

# Regenerar el archivo PDF

La funcionalidad de regeneración de PDF permite **recrear un comprobante existente** utilizando el diseño y los datos actualmente configurados en tu cuenta de TusFacturasAPP. Esto es particularmente útil cuando has realizado cambios en la configuración visual de tus puntos de venta.

**¿Cuándo utilizarla?** Esta operación es ideal si has actualizado:

* El logo de tu empresa.
* La información de cabecera o pie de tus comprobantes.
* Cualquier otro elemento visual que afecte la presentación del PDF.

**¿Cómo realizar la Regeneración?** Puedes llevar a cabo esta operación de dos maneras:

* **Vía API:** Utilizando el método específico de regeneración de PDF, enviando la solicitud directamente a nuestro endpoint API.
* **Desde la Plataforma Web:**
  1. Navegá a **Menú > Facturación > Mis ventas**.
  2. Ubicá el comprobante que deseas actualizar.
  3. Al seleccionar el ícono de Herramientas correspondiente a dicho comprobante, encontrarás  la opción **"Regenerar PDF"**.

### Endpoint

{% hint style="info" %}
<mark style="color:green;">`POST`</mark> `https://www.tusfacturas.app/app/api/v2/facturacion/`<mark style="color:purple;">`regenerar_pdf`</mark>
{% endhint %}

💡 Cada vez que utilices este método, se contará como un request en tu suscripción. Los requests se cuentan por cada método que uses.

### Ejemplo del JSON&#x20;

{% code title="JSON" %}
```
{
"usertoken" :  "xxxx",
"apikey"    :  "xxxx",
"apitoken"  :  "xxxx",
"comprobante":  {
                "tipo":                     "NOTA DE DEBITO B",
                "operacion":                "V",
                "punto_venta":              "2",
                "numero":                   "6"
        }
}

```
{% endcode %}

#### Estructura del Body

| Name        | Type   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| usertoken   | string | tus credenciales de acceso                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| apitoken    | string | Tus credenciales de acceso                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| apikey      | string | Tus credenciales de acceso                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| comprobante | String | <p>Un objeto compuesto de los siguientes atributos: </p><p><strong>tipo:</strong> Campo alfanumérico. Longitud máx: 50 caracteres, conteniendo el tipo de comprobante a consultar. Ej: FACTURA A </p><p><strong>operacion :</strong> Campo alfanumérico. Longitud máx: 1 carácter. Valores permitidos (V o C) ya sea para ventas o compras.</p><p><strong>punto_venta</strong> Campo númerico para indicar el número del punto de venta.</p><p><strong>numero :</strong> Campo numérico. Longitud máx: 8. Indica el número del comprobante a consultar.</p><p></p> |

### Ejemplo del JSON de respuesta:

```
{
        "error" :  "N",
        "comprobante_pdf_url"    :  "http://www.prueba.com", 
        "comprobante_ticket_url": "https://www.dominio.com/url"
}
```

***

TusFacturasAPP es un [software de facturación](https://www.tusfacturas.app/software-de-facturacion-argentina.html) y un [software de gestión](https://www.tusfacturas.app/software-de-gestion-para-pymes.html)  diseñado para empresas que facturen en Argentina. Conoce más de [TusFacturasAPP](https://www.tusfacturas.app).

### ¿Aún te quedan dudas? ¡Contactános!

En caso que requieras asistencia o tengas alguna duda relacionada con tu plan API DEV,  envíanos un mensaje a api@tusfacturas.app o [contactanos](https://www.tusfacturas.app/contacto.html) por el chat que tenemos disponible en la web [www.tusfacturas.app](https://www.tusfacturas.app/quiero-probar-api-factura-electronica.html).
