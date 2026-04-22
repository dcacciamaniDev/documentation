# Notas crudas

Registro cronologico de informacion recibida sobre el flujo actual de compras de
Gottert.

## 2026-04-21

### Contexto inicial

- Se va a relevar el flujo actual de trabajo de Gottert relacionado con compras.
- El objetivo posterior es construir un flujo de compras hibrido.
- La solucion futura deberia usar la mayor cantidad posible del flujo nativo de Odoo.
- Las brechas podrian resolverse con:
  - configuracion nativa de Odoo;
  - nuevos modulos dentro de Odoo;
  - aplicaciones externas por fuera de Odoo;
  - integraciones entre Odoo y sistemas externos.

### Fuente

- Usuario, pedido inicial de registro.

### Pedido de materiales como entrada del flujo

- Dentro de la empresa, las personas realizan una solicitud llamada `pedido de materiales`.
- Aunque se llame pedido de materiales, la solicitud puede corresponder a un bien o a
  un servicio.
- Al cargar la solicitud, el solicitante indica el producto o necesidad requerida.
- El solicitante informa:
  - marca;
  - codigo de producto del fabricante;
  - cantidad;
  - fecha de necesidad;
  - centro de costo.
- El solicitante no necesita saber si el producto ya existe en la base de datos del ERP.
- El solicitante no necesita saber si hay stock disponible o no.
- La solicitud pertenece a un centro de costo.
- Centros de costo mencionados:
  - `OT`;
  - `PIR`;
  - `STOCK`;
  - `OS`.
- `OT` se usa para proyectos grandes. Ejemplo mencionado: fabricacion de una linea de
  pintura para Volkswagen.
- `PIR` significa `pedido interno de repuesto`. Se usa cuando se requiere comprar un
  repuesto para un cliente que pidio una asistencia tecnica.
- Un `PIR` tambien puede incluir un repuesto y un servicio tecnico.
- `OS` se usa para proyectos de la unidad de negocios de servicios metalurgicos.
- `STOCK` se usa cuando lo comprado es para uso comun de oficinas, herramientas u otros
  consumos que no estan dentro de una `OT`, `PIR` u `OS`.

### Fuente

- Usuario, descripcion del primer tramo del flujo actual.

### Validacion y ruteo del pedido de materiales

- El `PM` significa `pedido de materiales`.
- El PM tiene asignado un responsable.
- El responsable valida que el PM tenga los items correctos.
- Una vez que el responsable aprueba el PM, el PM pasa al equipo de `Suministros`.
- El equipo de Suministros recibe una notificacion tipo `check-in`.
- En esa notificacion o instancia de check-in, Suministros debe seleccionar cual es la
  proxima etapa de cada item del PM.
- En un mismo PM puede haber items con destinos diferentes:
  - items que van a `Almacen`;
  - items que van directo a la obra mediante `dropshipping`;
  - items que van directo a `Compras`.
- Si Suministros selecciona `Almacen`, el personal de almacen verifica cuantas
  cantidades de stock hay disponibles.
- Cuando falta stock, Almacen introduce las cantidades necesarias a comprar.
- Para los items de `dropshipping`, se crea un registro de `pendiente de entrega`.
- El registro de pendiente de entrega permite que el responsable de comercio exterior
  valide la recepcion y cierre el item.

### Fuente

- Usuario, descripcion de validacion del PM, check-in de Suministros y ruteo por item.

### Aclaracion sobre la ruta Logistica

- Aclaracion posterior: para los items que antes se habian descrito como
  `dropshipping`, el nombre correcto en el sistema actual es `Logistica`.
- No es necesariamente un dropshipping puro.
- En la ruta `Logistica`, el responsable de ComEx registra tanto la recepcion como la
  entrega.
- La operacion puede ocurrir de distintas formas:
  - se puede recibir en Gottert y luego enviarse al cliente;
  - se puede recibir solo en Gottert;
  - puede haber otros casos logisticos que no equivalen a entrega directa
    proveedor-cliente.
- Por lo tanto, `dropshipping` debe tratarse como una posible analogia futura con Odoo,
  no como el nombre correcto del proceso actual de Gottert.

### Fuente

- Usuario, aclaracion sobre items de Logistica y rol de ComEx.

### PM desde webapp y creacion de orden de compra en ERP

- Hay PM que ingresan por una webapp.
- Para esos PM, el equipo de Suministros entra al ERP y crea una orden de compra.
- La orden de compra puede tener items provenientes de distintos PM.
- Cada PM tiene asociado un centro de costo: `OT`, `OS`, `PIR` o `STOCK`.
- Como una OC puede agrupar items de distintos PM, la OC puede estar compuesta por
  lineas/items que pertenecen a diferentes centros de costo.
- La imputacion por centro de costo debe entenderse a nivel item/linea de la OC, no
  necesariamente como un unico dato de cabecera de la OC.

### Fuente

- Usuario, descripcion de PM ingresados por webapp y armado de ordenes de compra por
  Suministros en ERP.

### Respuestas a preguntas abiertas por brecha

#### Brecha: pedido de materiales previo a la compra

- El lider del proyecto revisa la solicitud.
- El lider del proyecto no necesariamente pertenece al equipo de Suministros.
- El lider puede ser, por ejemplo, un colaborador del equipo de Ingenieria que este
  como lider del proyecto.
- Actualmente el PM se registra en la webapp donde se generan los pedidos de
  materiales.
- Estados actuales de la solicitud:
  - `pendiente`;
  - `en proceso`;
  - `completado`;
  - `cancelado`.
- Una vez que el lider del proyecto aprueba la solicitud, al equipo de Suministros le
  llega una notificacion en la pagina de check-in de la misma webapp.
- En esa pagina de check-in, Suministros decide que hacer con los items del PM.

#### Brecha: centros de costo OT, PIR, STOCK y OS

- `OT`, `PIR`, `STOCK` y `OS` tienen diferentes significados operativos, pero en este
  contexto se usan como centros de costo.
- `OT` y `OS` son proyectos.
- `PIR` tambien es un proyecto.
- `STOCK` corresponde a items de stock comun, por ejemplo insumos de impresora o
  herramientas.
- Los proyectos tienen su propio ciclo operativo.
- Las `OT` pueden ser de larga duracion; se menciono como ejemplo una OT que podria
  durar 4 anos.

#### Brecha: integracion webapp PM con ERP

- El personal de Suministros copia manualmente los datos en el ERP desde la webapp.
- Esto confirma que hoy existe doble carga entre webapp y ERP.

#### Brecha: reportes de pendientes de compra

- Sin respuesta adicional registrada en este mensaje.

### Respuesta sobre Almacen y faltantes

- Para la brecha `Almacen determina faltantes a comprar`, se confirma que Almacen si
  reserva stock.
- Almacen tambien entrega stock.
- El personal de Almacen deberia ser capaz de generar una RFQ partiendo del PM.
- La RFQ generada por Almacen deberia corresponder a las cantidades de items que no
  llega a suplir con el stock disponible.

### Fuente

- Usuario, aclaracion sobre reserva, entrega y generacion de RFQ desde Almacen.

### Reportes de pendientes de compra

- El ERP actual dispone de reportes para consultar items pendientes de compra.
- En esos reportes se pueden filtrar los items pendientes de compra por centro de
  costo.
- Tambien se pueden filtrar los items pendientes de compra por proveedor.
- Esta capacidad de reporting es parte del flujo operativo actual y deberia preservarse
  o redisenarse en el flujo hibrido futuro.

### Fuente

- Usuario, descripcion de reportes actuales del ERP.
