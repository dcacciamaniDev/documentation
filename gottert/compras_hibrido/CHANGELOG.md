# Changelog

## 2026-04-21

- Se crea la carpeta de relevamiento `gottert/compras_hibrido`.
- Se agregan archivos base para notas crudas, flujo actual, brechas, candidatos de
  personalizacion, preguntas abiertas y glosario.
- Se registra el `pedido de materiales` como entrada del flujo actual de Gottert.
- Se documentan datos minimos de la solicitud: marca, codigo de fabricante, cantidad,
  fecha de necesidad y centro de costo.
- Se documentan centros de costo iniciales: `OT`, `PIR`, `STOCK`, `OS`.
- Se agregan brechas candidatas y candidatos de personalizacion relacionados con la
  capa de solicitud previa a la compra.
- Se registra la validacion del PM por responsable asignado.
- Se registra el paso del PM aprobado a Suministros mediante notificacion tipo
  check-in.
- Se documenta el ruteo por item hacia Almacen, dropshipping o Compras.
- Se registra que Almacen verifica stock e informa cantidades faltantes a comprar.
- Se registra el `pendiente de entrega` para items de dropshipping y el cierre por
  Comercio Exterior.
- Se crea `06_pedido_de_materiales.md` como detalle funcional del PM.
- Se corrige la ruta antes descripta como dropshipping: en el sistema actual se llama
  `Logistica`.
- Se registra que `Logistica` no necesariamente es dropshipping puro.
- Se registra que ComEx informa tanto recepcion como entrega para items de Logistica.
- Se registra que algunos PM ingresan por webapp y Suministros crea la OC en ERP.
- Se registra que una OC puede contener items de distintos PM.
- Se registra que una OC puede tener lineas con distintos centros de costo.
- Se crea `07_orden_de_compra.md` para documentar agrupacion, trazabilidad e imputacion
  por linea de OC.
- Se registra que el ERP actual tiene reportes de items pendientes de compra filtrables
  por centro de costo y proveedor.
- Se crea `08_reportes_actuales.md` para registrar reportes que deben preservarse o
  redisenarse.
- Se registra la hipotesis de usar PM como RFQ.
- Se concluye preliminarmente que el PM completo no deberia ser una RFQ, pero que las
  lineas comprables del PM si podrian generar RFQ/OC.
- Se agrega la alternativa de pedido de consumo interno para lineas cubiertas con stock.
- Se crea `09_hipotesis_diseno.md`.
- Se agregan opciones para implementar el comportamiento tipo PM: modulo custom de
  Odoo, customizacion liviana, webapp externa integrada y enfoque hibrido recomendado.
- Se registran respuestas a preguntas abiertas por brecha.
- Se documenta que el lider del proyecto revisa y aprueba el PM.
- Se documentan estados actuales del PM en la webapp: `pendiente`, `en proceso`,
  `completado`, `cancelado`.
- Se documenta que Suministros recibe el PM aprobado en la pagina de check-in de la
  misma webapp.
- Se aclara que `OT`, `PIR`, `STOCK` y `OS` funcionan como centros de costo en este
  contexto.
- Se confirma que Suministros copia manualmente datos desde la webapp al ERP.
- Se confirma que Almacen reserva y entrega stock para items del PM.
- Se registra que Almacen deberia poder generar una RFQ desde el PM por las cantidades
  faltantes que no puede suplir con stock.
