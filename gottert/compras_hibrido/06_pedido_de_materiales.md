# Pedido de materiales

Detalle funcional del `PM` de Gottert.

## Definicion

`PM` significa `pedido de materiales`.

Aunque el nombre mencione materiales, el PM puede incluir:

- bienes;
- servicios;
- combinaciones de repuestos y servicios.

Algunos PM ingresan por una webapp. Suministros luego entra al ERP para crear la orden
de compra correspondiente cuando el item sigue el camino de compra.

## Datos informados por el solicitante

- Producto o necesidad requerida.
- Marca.
- Codigo de producto del fabricante.
- Cantidad.
- Fecha de necesidad.
- Centro de costo: `OT`, `PIR`, `STOCK` u `OS`.

El solicitante no necesita saber si el producto existe en el ERP ni si hay stock.

## Responsable del PM

Cada PM tiene un responsable/lider asignado.

El lider del proyecto revisa la solicitud y valida que el PM tenga los items correctos.
Ese lider no necesariamente pertenece a Suministros; puede ser, por ejemplo, un
colaborador de Ingenieria que este liderando el proyecto.

Una vez aprobado, el PM pasa al equipo de Suministros.

## Estados actuales

En la webapp actual, la solicitud puede tener estos estados:

- `pendiente`;
- `en proceso`;
- `completado`;
- `cancelado`.

## Check-in de Suministros

Suministros recibe una notificacion en la pagina de check-in de la misma webapp donde
se generan los PM.

En esa instancia, Suministros selecciona la proxima etapa de cada item del PM.

Un mismo PM puede tener items con rutas diferentes:

- `Almacen`;
- `Logistica`;
- `Compras`.

## Ruta Almacen

Cuando un item se deriva a `Almacen`, el personal de almacen verifica cuantas
cantidades de stock hay disponibles.

Almacen reserva y entrega el stock disponible.

Si falta stock, Almacen introduce las cantidades necesarias a comprar. Ademas, el
personal de Almacen deberia poder generar una RFQ desde el PM por las cantidades de
items que no llega a suplir con stock.

Hipotesis de diseño para el flujo hibrido:

- la parte cubierta con stock podria generar reserva y entrega interna vinculada al PM;
- la parte faltante podria generar RFQ/OC desde Almacen hacia el circuito de compra;
- ambas salidas deberian conservar el centro de costo de la linea del PM.

Puntos pendientes:

- si la RFQ por faltante queda a cargo de Almacen, Suministros o Compras;
- si la cantidad faltante genera automaticamente una RFQ o si Almacen la crea mediante
  accion manual;
- si Suministros revisa la decision de Almacen antes de comprar.

## Ruta Logistica

Cuando un item se deriva a `Logistica`, se crea un registro de seguimiento logistico.

El responsable de ComEx registra tanto la recepcion como la entrega, y cierra el item
cuando corresponde.

Esta ruta no es necesariamente dropshipping puro. Puede cubrir casos como:

- recibir en Gottert y luego enviar al cliente;
- recibir solo en Gottert;
- otros casos logisticos pendientes de relevar.

Puntos pendientes:

- que datos tiene el seguimiento logistico;
- que evidencia se usa para registrar la recepcion;
- que evidencia se usa para registrar la entrega;
- como se vincula el seguimiento logistico con la compra, el proveedor, la obra y la
  factura.

## Ruta Compras

Algunos items pueden ir directo a `Compras`.

Para PM ingresados por webapp, Suministros crea la orden de compra en el ERP. La OC
puede agrupar items de distintos PM.

Como cada PM tiene asociado un centro de costo, las lineas de una misma OC pueden
pertenecer a distintos centros de costo.

Evaluacion preliminar: no conviene tratar el PM completo como una RFQ nativa, porque el
PM puede contener lineas que se cubren con stock o Logistica. Si parece compatible que
las lineas que efectivamente deben comprarse generen RFQ/OC.

Puntos pendientes:

- si Compras crea una RFQ, una OC directa o realiza primero una busqueda/cotizacion;
- si debe validar producto existente o crear uno nuevo;
- si requiere aprobacion adicional antes de emitir OC.
- como se vincula cada linea de OC con su PM/linea PM de origen;
- si el centro de costo se registra como dato de linea, imputacion analitica u otro
  campo.

## Estados candidatos del PM

Estos estados son candidatos inferidos a partir del relevamiento inicial; todavia no
estan confirmados como nombres reales del proceso.

- Borrador o cargado por solicitante.
- Pendiente de validacion del lider del proyecto.
- Aprobado por lider del proyecto.
- En check-in de Suministros.
- Ruteado por item.
- En Almacen.
- En Compras.
- En Logistica / seguimiento logistico.
- Cerrado parcial.
- Cerrado total.
