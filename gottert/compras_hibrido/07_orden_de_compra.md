# Orden de compra

Detalle funcional de la orden de compra en el flujo actual de Gottert.

## Creacion desde PM

Para los PM que ingresan por una webapp, el equipo de Suministros entra al ERP y crea
la orden de compra.

Actualmente, Suministros copia manualmente los datos desde la webapp al ERP.

Pendiente de relevar si Suministros:

- crea primero una RFQ;
- crea directamente una OC;
- agrupa items antes de crear el documento;
- usa algun asistente o solo carga manual en ERP.

## Agrupacion de items

Una orden de compra puede tener items provenientes de distintos PM.

Esto implica que la OC no representa necesariamente un unico PM ni un unico centro de
costo.

## Centro de costo por item

Cada PM tiene asociado un centro de costo:

- `OT`;
- `OS`;
- `PIR`;
- `STOCK`.

Como una misma OC puede agrupar items de distintos PM, cada linea/item de la OC puede
pertenecer a un centro de costo diferente.

Regla funcional confirmada: la trazabilidad del centro de costo debe conservarse por
linea/item de OC.

## Trazabilidad necesaria

Para el futuro flujo hibrido, una linea de OC deberia poder responder:

- de que PM viene;
- de que linea de PM viene;
- a que centro de costo pertenece;
- quien la solicito;
- quien valido el PM;
- como fue ruteada por Suministros;
- si paso por Almacen, Compras o Logistica;
- que cantidad se compro finalmente.

## Mapeo posible con Odoo

Pendiente de analisis. Candidatos:

- usar distribucion analitica o cuenta analitica por linea de compra;
- agregar referencia a PM y linea de PM en la linea de compra;
- crear acciones desde PM para generar RFQ/OC manteniendo trazabilidad;
- integrar la webapp con Odoo para evitar doble carga.

## Reportes relacionados

El ERP actual tiene reportes de items pendientes de compra. Esos reportes permiten
filtrar por:

- centro de costo;
- proveedor.

Para conservar esta capacidad, el futuro modelo debe permitir consultar pendientes a
nivel item/linea, incluso cuando una OC agrupe distintos PM y distintos centros de
costo.

## Preguntas abiertas

- Que campos transcribe Suministros manualmente desde la webapp al ERP?
- El criterio principal para agrupar items en una OC es proveedor, fecha, PM, centro de
  costo u otro?
- Una linea de PM puede dividirse en varias lineas de OC?
- Una linea de OC puede agrupar varias lineas de PM?
- El centro de costo por linea se usa para contabilidad, presupuesto, reporting o
  aprobaciones?
- Hay restricciones para mezclar `OT`, `OS`, `PIR` y `STOCK` en una misma OC?
- Que estados se consideran pendientes de compra para los reportes actuales?
- El reporte toma datos de PM, OC, proveedor o una tabla intermedia del ERP?
