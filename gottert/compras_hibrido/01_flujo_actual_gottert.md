# Flujo actual de compras de Gottert

Este documento ordena el proceso real de compras de Gottert a medida que se releva.

## Estado

Relevamiento iniciado. Tramos confirmados: solicitud interna mediante `pedido de
materiales`, validacion por lider del proyecto y ruteo por item desde Suministros.

## Flujo resumido

El flujo comienza cuando una persona de la empresa registra un `pedido de materiales`.
Ese pedido puede representar un bien o un servicio. El solicitante no necesita saber si
el producto existe en el ERP ni si hay stock disponible; solo debe describir la
necesidad con marca, codigo de fabricante, cantidad, fecha de necesidad y centro de
costo. Luego, el lider del proyecto valida que los items del PM sean correctos. Si
aprueba, el PM pasa a Suministros, donde se decide la proxima etapa de cada item: Almacen,
Logistica u ordenamiento hacia Compras.

Cuando los PM ingresan por una webapp, Suministros entra al ERP y crea la orden de
compra. Una misma OC puede agrupar items de diferentes PM. Por eso, aunque el PM tenga
un centro de costo asociado, la OC necesita conservar centro de costo por linea/item.

## Etapas del proceso

### 1. Necesidad de compra

Una persona dentro de Gottert identifica una necesidad. La necesidad puede ser:

- un bien;
- un servicio;
- un caso mixto, por ejemplo repuesto mas servicio tecnico.

En esta etapa todavia no se exige que el solicitante conozca el producto interno del
ERP, la disponibilidad de stock ni la estrategia de abastecimiento.

### 2. Solicitud interna

La solicitud interna se llama `pedido de materiales`.

Confirmado para parte del flujo actual: algunos PM ingresan por una webapp.

Datos que informa el solicitante:

- producto o necesidad requerida;
- marca;
- codigo de producto del fabricante;
- cantidad;
- fecha de necesidad;
- centro de costo.

Centros de costo mencionados:

- `OT`: proyectos grandes, por ejemplo fabricacion de una linea de pintura para
  Volkswagen.
- `PIR`: pedido interno de repuesto para asistencia tecnica a clientes. Puede incluir
  repuesto, servicio tecnico o ambos.
- `OS`: proyectos de la unidad de negocios de servicios metalurgicos.
- `STOCK`: compras para uso comun de oficinas, herramientas u otros consumos que no
  estan asociados a una `OT`, `PIR` u `OS`.

Regla clave: el solicitante carga la necesidad, no resuelve si corresponde usar stock,
crear producto, comprar, pedir cotizacion o contratar servicio.

Estados actuales del PM en la webapp:

- `pendiente`;
- `en proceso`;
- `completado`;
- `cancelado`.

### 3. Validacion del lider del proyecto

El PM es revisado por el lider del proyecto. Ese lider valida que la solicitud tenga
los items correctos.

El lider del proyecto no necesariamente pertenece a Suministros. Puede ser, por
ejemplo, un colaborador del equipo de Ingenieria que este como lider del proyecto.

Cuando el lider aprueba la solicitud, el PM pasa al equipo de `Suministros`.

Pendiente de relevar:

- como se asigna el lider/responsable del PM;
- si el responsable puede rechazar o pedir correcciones;
- si la aprobacion aplica al PM completo o tambien puede aplicar por item;
- como se relacionan los estados actuales con las etapas reales del proceso.

### 4. Check-in de Suministros y ruteo por item

Suministros recibe una notificacion en la pagina de check-in de la misma webapp donde
se generan los PM. En esa instancia debe seleccionar la proxima etapa de cada item del
PM.

Un mismo PM puede contener items con rutas diferentes:

- `Almacen`: el item se deriva a revision de stock.
- `Logistica`: el item se deriva al circuito logistico gestionado por ComEx.
- `Compras`: el item se deriva directo al circuito de compra.

Regla clave: el ruteo se define por item, no necesariamente por PM completo.

### 5. Almacen y determinacion de faltantes

Si Suministros selecciona `Almacen`, el personal de almacen verifica cuantas cantidades
de stock hay disponibles.

Almacen reserva y entrega las cantidades disponibles de stock.

Si el stock disponible no cubre la necesidad, Almacen introduce las cantidades
necesarias a comprar. El personal de Almacen deberia poder generar una RFQ partiendo
del PM para las cantidades de items que no llega a suplir con stock.

Pendiente de relevar:

- como queda registrado el faltante;
- si la RFQ generada por Almacen queda a cargo de Almacen, Suministros o Compras;
- si hay validacion posterior del responsable del PM.

### 6. Logistica, recepcion y entrega

Para los items de `Logistica`, se crea un registro de seguimiento logistico pendiente.

El responsable de ComEx registra tanto la recepcion como la entrega. Esta ruta no es
necesariamente un dropshipping puro: el item podria recibirse en Gottert y luego
enviarse al cliente, o podria recibirse solo en Gottert.

Pendiente de relevar:

- cuando se crea la compra asociada a la ruta Logistica;
- que variantes logisticas existen dentro de esta ruta;
- que evidencia usa ComEx para registrar recepcion y entrega;
- que significa cerrar el item en terminos administrativos y contables.

### 7. Pedido de cotizacion o busqueda de proveedor

Por completar. Confirmado hasta ahora: algunos items del PM pueden ir directo a
`Compras`, y para PM ingresados por webapp Suministros entra al ERP para crear la OC.
Hoy Suministros copia manualmente los datos desde la webapp hacia el ERP.

### 8. Comparacion y seleccion

Por completar.

### 9. Aprobacion

Por completar.

### 10. Orden de compra

Suministros crea la orden de compra en el ERP.

Reglas confirmadas:

- la OC puede contener items de distintos PM;
- cada PM tiene asociado un centro de costo: `OT`, `OS`, `PIR` o `STOCK`;
- como una OC puede mezclar items de distintos PM, sus lineas pueden pertenecer a
  diferentes centros de costo;
- la trazabilidad e imputacion de centro de costo deben conservarse por linea/item de
  la OC, no solo a nivel cabecera.

Pendiente de relevar:

- si Suministros crea una RFQ previa o directamente una OC;
- si la agrupacion de items se hace por proveedor, fecha de necesidad, centro de costo
  u otro criterio;
- si una linea de OC siempre corresponde a una unica linea de PM;
- si una linea de PM puede dividirse en varias lineas de OC;
- como se refleja en el ERP el origen PM de cada linea.

### 11. Recepcion fisica o logistica

Por completar.

### 12. Control documental

Por completar.

### 13. Factura del proveedor

Por completar.

### 14. Pago y cierre

Por completar.

## Reportes operativos actuales

El ERP actual dispone de reportes para consultar items pendientes de compra.

Filtros confirmados:

- centro de costo;
- proveedor.

Esta capacidad debe considerarse requisito funcional para el flujo hibrido futuro,
especialmente porque una misma OC puede agrupar items de distintos PM y distintos
centros de costo.

## Excepciones conocidas

Por completar.

## Evidencia y notas relacionadas

- Ver `00_notas_crudas.md`.
