---
description: >-
  Utilizá el servicio de notificaciones para obtener información, en tiempo
  real, cada vez que ocurre un evento.
---

# Webhooks (notificaciones)

{% hint style="info" %}
**ATENCIÓN!** Éste servicio, se encontrará disponible, a partir del 01/04/2022
{% endhint %}

![](.gitbook/assets/image.png)

## ¿Qué es un WebHook?

Un `webhook` es una notificación que se envía de un servidor a otro, mediante una llamada `HTTP POST` al ocurrir un determinado evento.

TusFacturasAPP te enviará un webhook, siempre que se produzca uno o más eventos registrados,  evitando pérdida de datos siempre que se presente alguna situación.

## Dirección del webhook

La dirección del webhook, se configura dentro de tu CUIT+PDV. Para eso deberás ingresar al MENÚ > Mi espacio de trabajo > Cuits + PDV y editando el registro de tu CUIT, podrás agregarlo.&#x20;

La dirección que establezcas para el webhook, no debe contener un redirect y debe encontrarse funcionando. Si la misma se encuentra fuera de servicio por más de 24hs será ignorada por completo y no se te notificará nada más, hasta que indiques una nueva URL.

El formato esperado es: _https://www.dominio.com/script-nombre_

## **¿Qué te notificaremos vía  webhook?**

Vas a recibir por POST, un JSON con la siguiente estructura, para que puedas relacionar mediante el external\_reference que nos enviaste, al comprobante en cuestión:

{% code title="JSON" %}
```
{
	"creado": "18/03/2022 15:58:11",
	"evento": "encolado",
	"recurso": "facturacion",
	"external_reference": "17032",
	"intento": 1,
	"msg": [],
	"hook_id": "xxxxx"
} 
```
{% endcode %}

### Tipos de evento posibles, por recurso

|   recurso   |   evento  | info                                                                                                                                                       |
| :---------: | :-------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| facturacion |  encolado | Éste evento te informa, que el comprobante que enviaste, se encuentra ya en la cola de procesamiento, para ser emitido en la fecha que indicaste.          |
| facturacion |  emitido  | Éste evento te informa que el comprobante que enviaste, se ha facturado correctamente.                                                                     |
| facturacion |   error   | Éste evento te informa que el comprobante que enviaste, no se ha podido procesar y recibrás dentro del atributo "msg", la lista con los errores detectados |
| facturacion | eliminado | Éste evento te informa que se ha eliminado un comprobante.                                                                                                 |
|     test    |    test   | Se utilizará éste evento para probar la url de tu webhook                                                                                                  |
|             |           |                                                                                                                                                            |

## Reintentos

Cuando recibís una notificación en tu plataforma, TusFacturasAPP espera una respuesta para validar que la recibiste correctamente. Para eso, debes devolver un `HTTP STATUS 200 (OK)`. Si no se envía esta respuesta, se entenderá que no ha recibido la notificación y se realizará un nuevo intento de envío hasta que reciba la respuesta.

|      Evento     | Plazo después del último envío | Tiempo de espera de tu confirmación |
| :-------------: | ------------------------------ | ----------------------------------- |
|      Envío      | -                              | 20 segundos                         |
|  Primer intento | 5 minutos                      | 5 segundos                          |
| Segundo intento | 30 minutos                     | 5 segundos                          |
|  Tercer intento | 3 horas                        | 5 segundos                          |
|  Cuarto intento | 6 horas                        | 5 segundos                          |
|  Quinto intento | 12 horas                       | 5 segundos                          |

#### Ejemplo de reintentos

Hook 0 \_\_\_\_\_\_\_\_\_\_\_\_\_ enviado el 22/03/2022 a las 10:00

Hook 1 \_\_\_\_\_\_\_\_\_\_\_\_\_ será enviado el 22/03/2022 a las 10:05

Hook 2 \_\_\_\_\_\_\_\_\_\_\_\_\_ será enviado el 22/03/2022 a las 10:35

Hook 3 \_\_\_\_\_\_\_\_\_\_\_\_\_ será enviado el 22/03/2022 a las 13:35

Hook 4 \_\_\_\_\_\_\_\_\_\_\_\_\_ será enviado el 22/03/2022 a las 19:35

Hook 5 \_\_\_\_\_\_\_\_\_\_\_\_\_ será enviado el 23/03/2022 a las 07:35



#### Ejemplo en php de como devolver un http (200)

```
<?php
    http_response_code(200);
?>
```

## &#x20;Una vez que recibo el webhook, ¿Qué hago?

Una vez recibido el webhook, deberás  realizar las consultas respectivas para obtener los datos generados.

&#x20;A continuación te mostramos la documentación asociada del método que debes consultar, según el recurso del que recibís el webhook.

|   Recurso   |                                                                      Documentación                                                                     |
| :---------: | :----------------------------------------------------------------------------------------------------------------------------------------------------: |
| facturacion |  [consulta avanzada por external\_reference](consulta-avanzada-de-comprobantes-enviados.md#como-realizar-una-consulta-avanzada-por-external-reference) |
|             |                                                                                                                                                        |
|             |                                                                                                                                                        |



## FAQs&#x20;

#### ¿Dónde configuro mi webhook?

La dirección del webhook, se configura dentro de tu CUIT+PDV. Para eso deberás ingresar al MENÚ > Mi espacio de trabajo > Cuits + PDV y editando el registro de tu CUIT, podrás agregarlo. Tené en cuenta que la dirección del hook, debe ser válida.

#### En caso de que la dirección de mi webhook, presente inconvenientes y falle el webhook, ¿se realizan reintentos hasta completar la notificación?

Si. Te sugerimos consultar el apartado de "[reintentos](webhooks-notificaciones.md#reintentos)", de ésta misma página.

####

####