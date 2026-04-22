# Preguntas abiertas

Dudas pendientes para completar el relevamiento del flujo actual y poder disenar el
flujo de compras hibrido.

## Pendientes

- Que areas participan hoy en el proceso de compras?
- Que documentos se usan antes, durante y despues de la compra?
- Donde se registra hoy cada parte del proceso?
- Que aprobaciones existen y quien las realiza?
- Que controles se hacen al recibir mercaderia o servicios?
- Como se vincula la recepcion con la factura del proveedor?
- Que casos no se pueden resolver bien con el proceso actual?
- Que sistemas externos intervienen?
- El centro de costo define aprobadores, presupuesto o reglas diferentes?
- Para servicios, tambien se informa marca y codigo de fabricante, o se usa una
  descripcion libre?
- El `codigo de producto del fabricante` es obligatorio?
- Se adjuntan cotizaciones, imagenes, planos, emails u otra evidencia al pedido?
- Hay prioridades o urgencias ademas de la fecha de necesidad?
- Una misma solicitud puede tener multiples lineas?
- Que pasa si el producto solicitado ya existe en stock?
- Como se asigna el responsable del PM?
- El responsable del PM aprueba la cabecera completa o puede aprobar/rechazar items por
  separado?
- Que ocurre si el responsable del PM encuentra items incorrectos?
- La notificacion tipo check-in de Suministros se genera automaticamente al aprobar el
  responsable?
- Que opciones exactas puede elegir Suministros para cada item?
- El ruteo por item puede modificarse despues de elegido?
- Que pasa con un item enviado directo a Compras?
- Cuando Almacen detecta faltante, el faltante vuelve a Suministros o va directo a
  Compras?
- Que datos contiene el registro de seguimiento de `Logistica`?
- Que evidencia usa ComEx para registrar recepcion?
- Que evidencia usa ComEx para registrar entrega?
- En que casos la ruta Logistica implica recibir en Gottert y luego enviar al cliente?
- En que casos la ruta Logistica implica recibir solo en Gottert?
- Hay casos de entrega directa proveedor-cliente dentro de Logistica?
- Que datos de la webapp ve Suministros al crear la OC en ERP?
- Suministros crea RFQ primero o crea directamente una OC?
- Con que criterio se agrupan items de distintos PM en una misma OC?
- Una OC puede mezclar centros de costo solo si comparte proveedor?
- Una linea de PM puede dividirse entre varias OCs?
- Una linea de OC puede agrupar varias lineas de PM?
- Como se registra hoy el centro de costo en cada item de OC?
- El centro de costo de una linea de OC se usa para contabilidad, reporting,
  presupuesto, aprobaciones o todo eso?
- Que estados se consideran `pendiente de compra` en el ERP actual?
- El reporte de pendientes muestra items antes de crear OC, despues de crear OC o ambos?
- El filtro por proveedor aplica cuando el proveedor ya esta definido o tambien muestra
  items sin proveedor?
- Quienes usan el reporte de pendientes de compra?
- El reporte muestra cantidades solicitadas, faltantes, compradas, recibidas o todas?
- El `pedido de consumo interno` deberia reservar stock, transferirlo, entregarlo a una
  ubicacion de proyecto/obra o consumirlo contablemente?
- El consumo interno debe impactar presupuesto o costos por `OT`, `OS`, `PIR` o
  `STOCK`?
- Las lineas con stock y las lineas a comprar pueden cerrarse de forma independiente
  dentro del mismo PM?
- La RFQ que genera Almacen por faltante queda a cargo de Almacen, Suministros o
  Compras?
- La generacion de RFQ desde Almacen debe ser automatica o por accion manual?
- La RFQ generada por Almacen requiere aprobacion adicional antes de enviarse o
  confirmarse?

## Respondidas

- Tipos de compras iniciales: el `pedido de materiales` puede representar bienes,
  servicios o casos mixtos.
- Informacion minima del pedido: marca, codigo de fabricante, cantidad, fecha de
  necesidad y centro de costo.
- El solicitante no necesita saber si el producto existe en el ERP.
- El solicitante no necesita saber si hay stock.
- Centros de costo mencionados: `OT`, `PIR`, `STOCK`, `OS`.
- El PM tiene un lider/responsable asignado.
- El lider del proyecto valida que el PM tenga los items correctos.
- Luego de la aprobacion del lider del proyecto, el PM pasa a Suministros.
- Suministros recibe una notificacion tipo check-in.
- Suministros define la proxima etapa por item.
- En un mismo PM puede haber items derivados a Almacen, Logistica y Compras.
- Si un item va a Almacen, Almacen verifica stock e informa cantidades necesarias a
  comprar si falta stock.
- Almacen reserva stock.
- Almacen entrega stock.
- Almacen deberia poder generar una RFQ desde el PM para las cantidades que no puede
  suplir con stock.
- La opcion que antes se habia descrito como dropshipping se llama `Logistica` en el
  sistema actual.
- `Logistica` no necesariamente es dropshipping puro.
- En la ruta Logistica, ComEx registra tanto la recepcion como la entrega.
- Hay PM que ingresan por una webapp.
- Suministros entra al ERP y crea una orden de compra para PM ingresados por webapp.
- Una OC puede tener items de distintos PM.
- Cada PM tiene asociado un centro de costo `OT`, `OS`, `PIR` o `STOCK`.
- Una misma OC puede tener lineas/items pertenecientes a distintos centros de costo.
- El PM se registra actualmente en la webapp donde se generan los PM.
- Estados actuales del PM: `pendiente`, `en proceso`, `completado`, `cancelado`.
- La solicitud del PM la revisa el lider del proyecto.
- El lider del proyecto no necesariamente pertenece a Suministros; puede ser un
  colaborador de Ingenieria u otra area que lidere el proyecto.
- Cuando el lider aprueba la solicitud, Suministros recibe una notificacion en la
  pagina de check-in de la misma webapp.
- En el contexto del PM, `OT`, `PIR`, `STOCK` y `OS` son centros de costo.
- `OT`, `OS` y `PIR` son proyectos; `STOCK` corresponde a stock comun.
- Las `OT` pueden ser proyectos de larga duracion, incluso de varios anos.
- Suministros copia manualmente los datos desde la webapp al ERP.
- El ERP actual tiene reportes de items pendientes de compra.
- Los pendientes de compra pueden filtrarse por centro de costo.
- Los pendientes de compra pueden filtrarse por proveedor.
- Hipotesis evaluada: el PM completo podria parecerse a una RFQ, pero la equivalencia
  es parcial porque el PM puede contener lineas que no se compran.
- Alternativa preliminar: PM como documento interno; lineas comprables generan RFQ/OC y
  lineas con stock generan pedido de consumo interno.
