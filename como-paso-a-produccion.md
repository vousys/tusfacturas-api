---
description: >-
  API de facturación electrónica ARCA: Cómo pasar a Producción: Recomendaciones
  y Pasos a Seguir
---

# 🚀 ¿Cómo paso a producción?

Una vez finalizadas las pruebas y antes de pasar a producción, podes optar por mantener la misma cuenta de desarrollo o crear una nueva, ya sea para vos o para tu cliente. **Recomendamos conservar tu cuenta de desarrollador** para futuras pruebas y mejoras.

Si decidís reutilizar la misma cuenta, segui estos pasos para asegurarte de que no queden registros de prueba en el entorno de producción:

1.  **Elimina los comprobantes de prueba**

    * Accede a la plataforma web.
    * Dirígete a **Menú > Facturación > Mis ventas**.
    * Elimina **todos** los comprobantes asociados al **CUIT/Punto de Venta (PDV)**.


2.  **Contrata una suscripción de tipo "API"**

    1. Accede a la plataforma web.
    2. Dirígete a **Menú > Mi cuenta > Cambiar o renovar mi plan actual**.
    3. Consulta los [planes API](https://www.tusfacturas.app/tarifas-tusfacturas-planes-api-factura-electronica.html) disponibles y vigentes en nuestra web.
    4. Tene en cuenta que si tu plan API DEV se encuentra activo y vigente por unos dias más, la suscripción que adquieras comenzará al finalizar ésta. En ese caso, podes escribirnos a api@tusfacturas.app y lo solucionamos.


3. #### **Enlaza con AFIP/ARCA y Configura el Punto de Venta**

* Configura el **punto de venta** de tu cliente accediendo a:\
  **Menú > Mi espacio de trabajo > Puntos de venta (CUITs/PDV) > Crear nuevo**.
* Si emitirás **factura electrónica con AFIP/ARCA**, sigue los pasos del instructivo de enlace que recibirás por e-mail después de dar de alta el punto de venta.
* Una vez completada la vinculación, accede a:\
  **Menú > Facturación > Recuperar numeración desde AFIP/ARCA**.

Este proceso actualizará el numerador interno con la numeración oficial **una única vez**, asegurando que tu configuración esté lista para la emisión de comprobantes en producción.

Siguiendo estos pasos, garantizarás una transición ordenada y sin registros de prueba en el entorno de producción.
