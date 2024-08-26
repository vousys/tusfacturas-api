---
description: >-
  Guía práctica para migrar a la API AFIP de facturación asincrónica . Acelera
  tus emisiones y optimiza tus procesos.
---

# Guía de migración a facturación asincrónico (encolado)

## ¿Que necesito hacer para migrar desde comprobantes instantáneos?

Si ya venias haciendo comprobantes instantáneos y queres migrar a la facturación asincrónica para acelerar los tiempos de procesamiento, estos son los puntos que deberías tener en cuenta:

1- Agrega un external\_reference a tu bloque de comprobantes y [asigná una dirección para el webhook, como se especificá aquí](../webhooks-notificaciones.md).

2- Modificá tu llamada actual a nuestra API, cambiando la dirección del método a: "facturacion/lotes"  -> "facturacion/lotes\_encola" o&#x20;

"facturacion/nuevo" -> "facturacion/nuevo\_encola

3- Crea un script del lado de tu servidor, para que reciba el JSON con los eventos que enviaremos [via webhook](../webhooks-notificaciones.md) y nos devuelva la confirmación. Al recibir la información, éste script, debe [emitir una consulta avanzada de comprobantes](consulta-avanzada-de-comprobantes-enviados.md#como-realizar-una-consulta-avanzada-por-external-reference), para obtener la info asociada al hook recibido y realizar con la respuesta, lo que antes hacías mientras esperabas la respuesta instantánea.

