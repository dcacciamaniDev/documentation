# Candidatos de personalizacion

Registro de posibles soluciones para completar el flujo de compras hibrido de Gottert.

## Principio de diseno

Priorizar Odoo nativo cuando cubra el caso razonablemente bien. Personalizar solo
cuando haya una brecha clara de proceso, control, integracion, trazabilidad o
experiencia operativa.

## Configuracion nativa posible

- Mapear `OT`, `PIR`, `STOCK` y `OS` contra estructuras nativas de Odoo, como cuentas
  analiticas, proyectos, unidades de negocio, etiquetas analiticas o campos de
  imputacion, segun corresponda.

## Nuevos modulos dentro de Odoo

### Candidato: modulo custom PM Gottert

- Tipo: Modulo Odoo
- Problema que resuelve: implementar el PM como documento interno propio, con ruteo por
  linea y generacion de documentos nativos de Odoo cuando corresponda.
- Etapa del flujo: solicitud interna, Suministros, Almacen, Compras y Logistica
- Datos necesarios: cabecera de PM, lineas de PM, lider/responsable, centro de costo,
  solicitante, estados, ruta por linea, stock cubierto, faltante a comprar,
  documentos generados y trazabilidad.
- Usuarios afectados: solicitantes, responsables de PM, Suministros, Almacen, Compras,
  ComEx, Administracion y responsables de centro de costo.
- Riesgos: sobredesarrollo, duplicacion de funciones nativas, permisos mal definidos o
  estados por linea demasiado complejos.
- Dependencias: definicion funcional final del PM, mapeo de centros de costo,
  integracion con Compras, Inventario y reportes.
- Prioridad: alta
- Estado: idea
- Fuente: evaluacion de alternativas.

### Candidato: pedido de materiales

- Tipo: Modulo Odoo
- Problema que resuelve: permitir que cualquier solicitante cargue una necesidad sin
  elegir necesariamente un producto ERP ni verificar stock.
- Etapa del flujo: solicitud interna
- Datos necesarios: marca, codigo de fabricante, cantidad, fecha de necesidad, centro
  de costo, descripcion del bien o servicio, lider del proyecto, estado del PM y estado
  por item.
- Usuarios afectados: solicitantes, compras, almacen, administracion y responsables de
  centro de costo.
- Riesgos: duplicacion de productos, solicitudes incompletas, reglas de aprobacion
  insuficientes o desalineacion con stock/compras.
- Dependencias: definicion de centros de costo, lideres/responsables, estados del pedido y
  criterios para convertir una solicitud en consumo de stock, RFQ, servicio o rechazo.
- Prioridad: media
- Estado: idea
- Fuente: usuario.

### Candidato: PM como documento interno generador de RFQ y consumo

- Tipo: Modulo Odoo
- Problema que resuelve: achicar la brecha con Odoo sin forzar que el PM completo sea
  una RFQ.
- Etapa del flujo: solicitud interna, Almacen y Compras
- Datos necesarios: lineas de PM, disponibilidad de stock, cantidad reservada,
  cantidad entregada, cantidad a comprar, proveedor si aplica, centro de costo y estado
  por linea.
- Usuarios afectados: solicitantes, responsables de PM, Suministros, Almacen y Compras.
- Riesgos: si se modela directamente como RFQ, se pueden incluir lineas que no
  corresponden a compra; si se separa demasiado, se puede perder trazabilidad.
- Dependencias: definicion de documento de consumo interno y reglas para generar RFQ/OC
  desde Almacen solo por faltantes o items no cubiertos por stock.
- Prioridad: alta
- Estado: idea
- Fuente: usuario.

### Candidato: pedido de consumo interno desde PM

- Tipo: Modulo Odoo
- Problema que resuelve: reservar y entregar stock disponible para atender lineas del
  PM sin generar una compra.
- Etapa del flujo: Almacen
- Datos necesarios: linea de PM, producto, cantidad solicitada, cantidad reservada,
  cantidad entregada, ubicacion origen, destino/centro de costo, responsable y estado.
- Usuarios afectados: Almacen, Suministros y responsables de centro de costo.
- Riesgos: consumo sin correcta imputacion, movimientos de stock sin trazabilidad al PM
  o stock reservado pero no entregado.
- Dependencias: definicion de si el consumo interno sera transferencia interna,
  movimiento a ubicacion de consumo, entrega a proyecto/obra o documento custom.
- Prioridad: alta
- Estado: idea
- Fuente: usuario.

### Candidato: ruteo por item del PM

- Tipo: Modulo Odoo
- Problema que resuelve: permitir que Suministros seleccione una proxima etapa distinta
  para cada item de un mismo PM.
- Etapa del flujo: check-in de Suministros
- Datos necesarios: item del PM, ruta seleccionada, responsable, fecha de decision,
  observaciones, estado por item.
- Usuarios afectados: Suministros, Almacen, Compras, ComEx y solicitantes.
- Riesgos: divergencia entre estado de cabecera y estado de items, duplicacion de
  compras o faltantes sin seguimiento.
- Dependencias: definicion de estados y acciones automaticas por ruta.
- Prioridad: alta
- Estado: idea
- Fuente: usuario.

### Candidato: gestion de faltantes desde Almacen

- Tipo: Modulo Odoo
- Problema que resuelve: registrar cuanto stock reserva/entrega Almacen y generar RFQ
  por la cantidad faltante.
- Etapa del flujo: Almacen
- Datos necesarios: stock disponible, cantidad solicitada, cantidad reservada, cantidad
  entregada, cantidad faltante a comprar, ubicacion, responsable y RFQ generada.
- Usuarios afectados: Almacen, Suministros y Compras.
- Riesgos: inconsistencias con stock real si no se integra con reservas o movimientos
  nativos, o RFQs duplicadas por el mismo faltante.
- Dependencias: integracion con Inventario de Odoo, definicion del movimiento/entrega
  interna y accion para generar RFQ desde PM.
- Prioridad: alta
- Estado: idea
- Fuente: usuario.

### Candidato: seguimiento logistico por ComEx

- Tipo: Modulo Odoo
- Problema que resuelve: controlar items derivados a `Logistica`, donde ComEx registra
  recepcion y entrega, incluso cuando no se trata de dropshipping puro.
- Etapa del flujo: Logistica
- Datos necesarios: item del PM, proveedor, destino, fecha esperada, recepcion,
  entrega, evidencia, responsable de ComEx y estado de cierre.
- Usuarios afectados: Suministros, Compras, ComEx y responsables de obra/cliente.
- Riesgos: duplicar controles nativos de inventario o dropshipping, o cerrar items sin
  evidencia suficiente.
- Dependencias: definicion de vinculo con OC, recepcion, entrega y factura de proveedor.
- Prioridad: media
- Estado: idea
- Fuente: usuario.

## Aplicaciones externas

### Candidato: formulario externo de pedido de materiales

- Tipo: App externa
- Problema que resuelve: capturar solicitudes de usuarios no especializados sin
  exponerles complejidad de ERP, productos internos o stock.
- Etapa del flujo: solicitud interna
- Datos necesarios: marca, codigo de fabricante, cantidad, fecha de necesidad, centro
  de costo, descripcion y adjuntos si aplican.
- Usuarios afectados: solicitantes y equipo que clasifica o deriva la solicitud.
- Riesgos: integracion incompleta con Odoo, doble carga, perdida de trazabilidad.
- Dependencias: API o integracion con Odoo, reglas de sincronizacion y estados.
- Prioridad: media
- Estado: idea
- Fuente: usuario.

### Candidato: webapp externa integrada para carga de PM

- Tipo: App externa
- Problema que resuelve: ofrecer una interfaz simple para solicitantes sin exponerles
  la complejidad del ERP.
- Etapa del flujo: carga inicial del PM
- Datos necesarios: solicitante, centro de costo, marca, codigo de fabricante,
  cantidad, fecha de necesidad, descripcion y adjuntos.
- Usuarios afectados: solicitantes, responsables de PM y Suministros.
- Riesgos: doble fuente de verdad, sincronizacion incompleta, estados inconsistentes
  entre webapp y Odoo.
- Dependencias: API con Odoo y decision sobre donde vive el PM como dato maestro.
- Prioridad: media
- Estado: idea
- Fuente: evaluacion de alternativas.

## Integraciones

### Candidato: integracion PM webapp con ERP

- Tipo: Integracion
- Problema que resuelve: eliminar la copia manual actual y preservar trazabilidad desde
  PM webapp hasta OC/linea de OC en ERP.
- Etapa del flujo: ingreso de PM y creacion de OC
- Datos necesarios: PM, linea de PM, centro de costo, producto/descripcion, cantidad,
  fecha de necesidad, ruta definida por Suministros y estado.
- Usuarios afectados: solicitantes, responsables de PM y Suministros.
- Riesgos: inconsistencias entre webapp y ERP, errores de transcripcion, OCs creadas
  sin origen trazable o items duplicados.
- Dependencias: API de la webapp, API/modelos del ERP y definicion de estados.
- Prioridad: alta
- Estado: brecha confirmada, solucion en analisis
- Fuente: usuario.

### Candidato: trazabilidad PM-linea OC-centro de costo

- Tipo: Modulo Odoo
- Problema que resuelve: permitir que una OC agrupe items de distintos PM y que cada
  linea conserve su PM origen y centro de costo.
- Etapa del flujo: orden de compra
- Datos necesarios: linea de PM origen, centro de costo, cantidad, proveedor, OC, linea
  de OC e imputacion analitica.
- Usuarios afectados: Suministros, Compras, Administracion, Contabilidad y responsables
  de centro de costo.
- Riesgos: imputaciones incorrectas si el centro de costo queda solo en cabecera o si
  se pierde la relacion con el PM origen.
- Dependencias: definicion de mapeo entre `OT`, `OS`, `PIR`, `STOCK` y estructura
  contable/analitica de Odoo.
- Prioridad: alta
- Estado: idea
- Fuente: usuario.

## Automatizaciones o reportes

### Candidato: reporte de items pendientes de compra

- Tipo: Reporte
- Problema que resuelve: mantener visibilidad operativa sobre items pendientes de
  compra con filtros por centro de costo y proveedor.
- Etapa del flujo: seguimiento operativo
- Datos necesarios: item pendiente, PM origen, centro de costo, proveedor, cantidad,
  fecha de necesidad, estado, OC/RFQ relacionada si existe.
- Usuarios afectados: Suministros, Compras, responsables de centro de costo y
  Administracion.
- Riesgos: que el reporte no refleje correctamente items aun no convertidos a OC, o que
  pierda trazabilidad si el centro de costo no esta por linea.
- Dependencias: definicion exacta de `pendiente de compra`, modelo de PM, lineas de OC
  e imputacion por centro de costo.
- Prioridad: alta
- Estado: idea
- Fuente: usuario.

## Plantilla de candidato

```md
### Candidato: <nombre corto>

- Tipo: Configuracion | Modulo Odoo | App externa | Integracion | Reporte | Automatizacion
- Problema que resuelve:
- Etapa del flujo:
- Datos necesarios:
- Usuarios afectados:
- Riesgos:
- Dependencias:
- Prioridad: baja | media | alta
- Estado: idea | en analisis | recomendado | descartado
- Fuente:
```
