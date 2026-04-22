# Reportes actuales

Registro de reportes existentes en el ERP actual que deben preservarse, reemplazarse o
redisenarse en el flujo hibrido.

## Items pendientes de compra

El ERP actual dispone de reportes para consultar items pendientes de compra.

Filtros confirmados:

- centro de costo;
- proveedor.

## Importancia para el flujo hibrido

Este reporte es relevante porque:

- los PM pueden ingresar por webapp;
- Suministros crea OCs en el ERP;
- una OC puede agrupar items de distintos PM;
- una OC puede tener lineas de distintos centros de costo;
- el seguimiento operativo necesita visibilidad por centro de costo y proveedor.

## Requisito a preservar

El flujo hibrido deberia permitir consultar items pendientes de compra filtrando por:

- centro de costo;
- proveedor.

Pendiente de definir si el reporte se construira sobre:

- lineas de PM;
- faltantes definidos por Almacen;
- RFQ;
- lineas de OC;
- una vista consolidada de pendientes.

## Preguntas abiertas

- Que estados se consideran `pendiente de compra`?
- El reporte incluye items sin proveedor asignado?
- El reporte incluye items ya incluidos en una OC pero no recibidos?
- El reporte incluye items de PM aprobados pero aun no comprados?
- El reporte muestra cantidades solicitadas, faltantes, compradas y recibidas?
- Quienes usan el reporte y con que frecuencia?
- El reporte se exporta o se usa solo dentro del ERP?

