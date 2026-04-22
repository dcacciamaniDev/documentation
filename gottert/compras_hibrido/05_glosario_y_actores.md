# Glosario y actores

Registro de terminos, areas, roles, sistemas y documentos mencionados durante el
relevamiento.

## Actores y areas

- Solicitante: persona dentro de la empresa que registra un `pedido de materiales`.
  No necesita conocer el producto interno del ERP ni la disponibilidad de stock.
- Responsable del PM: persona asignada al pedido de materiales que valida que los items
  del PM sean correctos.
- Lider del proyecto: persona que revisa y aprueba la solicitud del PM. No
  necesariamente pertenece a Suministros; puede ser, por ejemplo, un colaborador de
  Ingenieria que lidere el proyecto.
- Suministros: equipo que recibe el PM aprobado mediante una notificacion tipo check-in
  y define la proxima etapa de cada item.
- Almacen: area que revisa stock disponible para items derivados desde Suministros e
  informa cantidades necesarias a comprar cuando hay faltantes.
- Compras: area o etapa a la que pueden derivarse items del PM para continuar el
  circuito de compra.
- ComEx / Comercio Exterior: responsable de registrar recepcion y entrega para items
  derivados a la ruta `Logistica`, y de cerrar el item cuando corresponda.

## Sistemas

- Webapp de PM: aplicacion por la que ingresan pedidos de materiales. En la misma
  webapp existe una pagina de check-in donde Suministros recibe notificaciones de PM
  aprobados.
- ERP: sistema donde Suministros crea las ordenes de compra a partir de PM ingresados
  por webapp.

## Documentos

- Pedido de materiales: solicitud interna usada como entrada del proceso de compras.
  Puede corresponder a un bien, un servicio o un caso mixto.
- Seguimiento logistico: registro usado para items derivados a `Logistica`. Sirve para
  que ComEx registre recepcion, entrega y cierre del item.
- Orden de compra / OC: documento creado por Suministros en el ERP. Puede agrupar items
  provenientes de distintos PM.
- Reporte de pendientes de compra: reporte del ERP actual que permite consultar items
  pendientes de compra y filtrarlos por centro de costo o proveedor.

## Conceptos propios de Gottert

- Centro de costo: clasificacion obligatoria del `pedido de materiales`. Siglas
  mencionadas: `OT`, `PIR`, `STOCK`, `OS`.
- OT: centro de costo y proyecto, normalmente asociado a proyectos grandes. Ejemplo:
  fabricacion de una linea de pintura para Volkswagen. Puede tener ciclo largo, incluso
  de varios anos.
- PIR: `pedido interno de repuesto`. Se usa para comprar repuestos vinculados a
  asistencia tecnica de clientes. Tambien puede incluir repuesto y servicio tecnico. En
  este contexto funciona como centro de costo/proyecto.
- OS: centro de costo y proyecto usado para la unidad de negocios de servicios
  metalurgicos.
- STOCK: centro de costo usado para compras de uso comun de oficinas, herramientas u
  otros consumos que no pertenecen a una `OT`, `PIR` u `OS`.
- Codigo de producto del fabricante: identificador informado por el solicitante para
  describir lo requerido, aunque el producto no exista todavia en el ERP.
- Marca: dato informado por el solicitante para identificar el producto o necesidad.
- PM: abreviatura de `pedido de materiales`.
- Check-in de Suministros: notificacion o instancia recibida por Suministros luego de
  la aprobacion del PM, donde se define la proxima etapa de cada item.
- Estados actuales del PM: `pendiente`, `en proceso`, `completado`, `cancelado`.
- Ruteo por item: decision de Suministros que permite que distintos items del mismo PM
  vayan a Almacen, Logistica o Compras.
- Logistica: opcion del sistema actual para items que requieren gestion logistica por
  ComEx. No equivale necesariamente a dropshipping. Puede incluir recepcion en Gottert
  y posterior envio al cliente, o recepcion solo en Gottert.
- Linea de OC: item de una orden de compra. En el flujo actual puede provenir de un PM
  y conservar un centro de costo propio.
- OC multi-PM: orden de compra que agrupa items provenientes de distintos PM.
- Centro de costo por linea: regla necesaria cuando una OC contiene items de distintos
  PM y, por lo tanto, diferentes centros de costo dentro de la misma OC.
- Item pendiente de compra: item que aun requiere gestion de compra segun el ERP actual.
  Pendiente de relevar que estados exactos incluye.

## Terminos de Odoo relevantes

- RFQ: solicitud de cotizacion o presupuesto de compra.
- Purchase Order: orden de compra confirmada.
- Receipt: recepcion de proveedor.
- Vendor Bill: factura de proveedor.
- Bill Control: politica que define si se factura por cantidades pedidas o recibidas.
- 3-way matching: control entre compra, recepcion y factura.
- Dropship: envio directo del proveedor al cliente sin ingreso a stock propio.
