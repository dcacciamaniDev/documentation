# Brechas vs Odoo nativo

Comparacion entre el proceso actual de Gottert y el flujo nativo de compras de Odoo.

## Base nativa de referencia

- `mermaid/flujo_nativo_compras_odoo.md`
- `mermaid/flujo_nativo_compras_odoo_pdf.html`
- `mermaid/flujo_nativo_compras_odoo.pdf`

## Brechas confirmadas

### Brecha confirmada: doble carga webapp PM y ERP

- Estado: confirmada
- Etapa del flujo: ingreso de PM y creacion de OC
- Descripcion: el personal de Suministros copia manualmente en el ERP los datos que
  vienen desde la webapp de PM.
- Impacto operativo: hay doble carga, riesgo de error de transcripcion y posible
  perdida de trazabilidad entre PM, linea de PM, OC y linea de OC.
- Odoo nativo cubre: creacion manual de compras y APIs para integracion.
- Odoo nativo no cubre: la integracion actual entre la webapp de PM y el ERP.
- Alternativa sugerida: integrar la webapp con Odoo o migrar el PM a Odoo, evitando
  doble carga y preservando trazabilidad por linea.
- Tipo: Integracion
- Fuente: usuario.

## Brechas candidatas

### Brecha candidata: pedido de materiales previo a la compra

- Estado: necesidad funcional confirmada; pendiente de diseno
- Etapa del flujo: solicitud interna
- Descripcion: Gottert usa una solicitud interna llamada `pedido de materiales` como
  entrada del proceso. Puede ser por bienes, servicios o casos mixtos.
- Impacto operativo: el solicitante no necesita seleccionar un producto existente en
  ERP ni verificar stock; solo informa marca, codigo de fabricante, cantidad, fecha de
  necesidad y centro de costo.
- Odoo nativo cubre: RFQ, purchase order, recepciones, facturas de proveedor y controles
  de compra.
- Odoo nativo no cubre confirmado: el flujo actual tiene una solicitud interna previa
  registrada en una webapp, revisada por lider de proyecto y luego enviada a check-in
  de Suministros. Hay que analizar si se implementa con modulo custom, Odoo Studio,
  portal/webapp integrada o combinacion.
- Alternativa sugerida: analizar una capa de intake para `pedido de materiales`, dentro
  de Odoo o externa, que luego derive en busqueda de stock, creacion/normalizacion de
  producto, RFQ, servicio o imputacion al centro de costo correspondiente.
- Tipo: Pendiente
- Preguntas abiertas: como se asigna el lider del proyecto, si puede rechazar o pedir
  correcciones, si aprueba cabecera o lineas, y como se transforma cada linea en compra
  o consumo de stock.
- Fuente: usuario.

#### Respuestas recibidas

- Revisa la solicitud el lider del proyecto.
- El lider no necesariamente pertenece a Suministros; puede ser, por ejemplo, alguien
  de Ingenieria liderando el proyecto.
- Hoy el PM se registra en la webapp donde se generan los PM.
- Estados actuales: `pendiente`, `en proceso`, `completado`, `cancelado`.
- Cuando el lider aprueba, Suministros recibe una notificacion en la pagina de
  check-in de la misma webapp.

#### Hipotesis evaluada: usar la RFQ como PM

- Evaluacion preliminar: compatible solo parcialmente.
- Motivo: la RFQ nativa de Odoo es un documento de compra orientado a proveedor. En el
  flujo de Gottert, el PM es una solicitud interna previa que puede no tener proveedor,
  puede contener productos aun no existentes en ERP, puede tener lineas que se cubren
  con stock y puede tener lineas que van a Logistica o Compras.
- Riesgo: si el PM completo se modela como RFQ, se mezclan en un documento de compra
  lineas que tal vez no deben comprarse.
- Alternativa recomendada: mantener el PM como documento interno con lineas. Luego, por
  cada linea:
  - si hay stock, generar un pedido de consumo interno o movimiento interno vinculado
    al PM;
  - si falta stock o debe comprarse, generar RFQ/OC por proveedor con referencia a la
    linea de PM y centro de costo;
  - si va a Logistica, generar seguimiento logistico vinculado al PM.
- Conclusion preliminar: `PM completo = RFQ` no parece ser la mejor equivalencia.
  `Lineas comprables del PM -> RFQ/OC` si parece compatible con Odoo y reduce brecha.
  `Lineas con stock -> consumo interno` deberia modelarse por Inventario o con una
  personalizacion liviana.

### Brecha candidata: centros de costo OT, PIR, STOCK y OS

- Estado: significado funcional aclarado; pendiente de mapeo en Odoo
- Etapa del flujo: solicitud interna e imputacion contable/operativa
- Descripcion: cada pedido de materiales pertenece a un centro de costo identificado
  como `OT`, `PIR`, `STOCK` u `OS`.
- Impacto operativo: el centro de costo condiciona el motivo de compra, el proyecto o
  unidad afectada y probablemente la aprobacion, trazabilidad, presupuesto e imputacion.
- Odoo nativo cubre: cuentas analiticas, proyectos, etiquetas analiticas, compras por
  proyecto y trazabilidad configurable, segun version y modulos instalados.
- Odoo nativo no cubre confirmado: pendiente de validar el mapeo exacto entre centros
  de costo Gottert y estructuras nativas de Odoo, especialmente para proyectos largos.
- Alternativa sugerida: mapear cada sigla contra objetos nativos de Odoo antes de
  decidir desarrollo.
- Tipo: Pendiente
- Preguntas abiertas: como se crean, cierran y controlan presupuestariamente esos
  centros de costo/proyectos, y si el centro de costo define aprobadores o reglas.
- Fuente: usuario.

#### Respuestas recibidas

- En este contexto, `OT`, `PIR`, `STOCK` y `OS` se usan como centros de costo.
- `OT`, `OS` y `PIR` son proyectos.
- `STOCK` corresponde a stock comun, por ejemplo insumos de impresora o herramientas.
- Los proyectos tienen ciclo operativo propio.
- Las `OT` pueden ser de larga duracion; se menciono un ejemplo de hasta 4 anos.

### Brecha candidata: centro de costo por linea de OC

- Estado: pendiente de analisis
- Etapa del flujo: orden de compra e imputacion
- Descripcion: una orden de compra puede agrupar items provenientes de distintos PM.
  Como cada PM tiene asociado un centro de costo, las lineas de una misma OC pueden
  pertenecer a diferentes centros de costo.
- Impacto operativo: no alcanza con imputar la OC a un centro de costo de cabecera; la
  imputacion y trazabilidad deben mantenerse por linea/item.
- Odoo nativo cubre: lineas de orden de compra, cuentas analiticas y distribucion
  analitica por linea, segun configuracion y version.
- Odoo nativo no cubre confirmado: pendiente de validar si se necesita un vinculo
  explicito entre linea de PM, linea de OC y centro de costo Gottert.
- Alternativa sugerida: mapear `OT`, `OS`, `PIR` y `STOCK` a imputaciones analiticas o
  campos por linea de compra, y mantener referencia al PM/linea PM origen.
- Tipo: Pendiente
- Preguntas abiertas: si cada linea de OC puede tener una unica imputacion o varias, y
  si el costo debe reportarse por PM, centro de costo, proveedor, obra o combinaciones.
- Fuente: usuario.

### Brecha candidata: integracion webapp PM con ERP

- Estado: confirmada como brecha operativa
- Etapa del flujo: ingreso de PM y creacion de OC
- Descripcion: algunos PM ingresan por una webapp, pero Suministros entra al ERP para
  crear la orden de compra.
- Impacto operativo: puede existir doble carga o perdida de trazabilidad entre PM,
  item de PM, OC y linea de OC.
- Odoo nativo cubre: creacion manual de compras y APIs para integracion.
- Odoo nativo no cubre confirmado: hoy no hay integracion suficiente; Suministros copia
  manualmente datos desde la webapp al ERP.
- Alternativa sugerida: integrar webapp y ERP para que Suministros pueda crear RFQ/OC
  desde items aprobados del PM, preservando origen y centro de costo por linea.
- Tipo: Integracion
- Preguntas abiertas: que campos copia Suministros, que errores ocurren, y si la webapp
  debe integrarse con Odoo o ser reemplazada por PM dentro de Odoo.
- Fuente: usuario.

#### Respuestas recibidas

- El personal de Suministros copia los datos a mano en el ERP desde la webapp.

### Brecha candidata: reportes de pendientes de compra

- Estado: pendiente de analisis
- Etapa del flujo: seguimiento operativo y reporting
- Descripcion: el ERP actual permite consultar items pendientes de compra y filtrarlos
  por centro de costo o proveedor.
- Impacto operativo: Suministros y otras areas necesitan visibilidad sobre pendientes
  segun imputacion y proveedor, especialmente cuando una OC puede mezclar centros de
  costo y PM.
- Odoo nativo cubre: vistas de lista, filtros, agrupaciones, actividades y reportes
  sobre compras, si los datos necesarios estan modelados en los campos correctos.
- Odoo nativo no cubre confirmado: pendiente de validar si el concepto Gottert de
  `item pendiente de compra` coincide con RFQ, linea de OC, linea de PM, faltante de
  Almacen u otro estado intermedio.
- Alternativa sugerida: definir una vista/reporte de pendientes de compra que permita
  filtrar por centro de costo y proveedor, tomando como base las lineas de PM, RFQ u
  OC segun el modelo final.
- Tipo: Pendiente
- Preguntas abiertas: que estados entran en "pendiente de compra", quien usa el
  reporte, si debe mostrar cantidades faltantes y si incluye items aun no convertidos
  a OC.
- Fuente: usuario.

#### Respuestas recibidas

- Sin respuesta adicional registrada todavia.

### Brecha candidata: ruteo por item dentro de un mismo PM

- Estado: pendiente de analisis
- Etapa del flujo: check-in de Suministros
- Descripcion: Suministros decide la proxima etapa por cada item del PM. En un mismo PM
  pueden convivir items derivados a Almacen, Logistica y Compras.
- Impacto operativo: el documento cabecera no determina una unica ruta; cada linea
  necesita estado, responsable, destino operativo y posible cierre independiente.
- Odoo nativo cubre: ordenes de compra con lineas, rutas logisticas por producto,
  dropshipping y movimientos de stock, si los productos y rutas estan definidos.
- Odoo nativo no cubre confirmado: pendiente de validar si existe una solicitud previa
  multi-ruta por item antes de crear productos, compras o movimientos.
- Alternativa sugerida: modelar el PM con lineas ruteables, estados por item y acciones
  que generen consumo/reserva de stock, RFQ/OC o seguimiento logistico segun destino.
- Tipo: Pendiente
- Preguntas abiertas: si el ruteo puede cambiar luego, quien puede modificarlo, que
  estados existen por item y que trazabilidad se espera.
- Fuente: usuario.

### Brecha candidata: Almacen determina faltantes a comprar

- Estado: comportamiento confirmado; pendiente de diseno
- Etapa del flujo: Almacen
- Descripcion: cuando un item se deriva a Almacen, el personal verifica stock disponible
  y reserva/entrega las cantidades disponibles. Cuando falta stock, Almacen debe poder
  generar una RFQ desde el PM por las cantidades no cubiertas.
- Impacto operativo: la cantidad final a comprar puede diferir de la cantidad solicitada
  por el usuario, porque depende de la disponibilidad real de stock.
- Odoo nativo cubre: inventario, stock disponible, reservas, reabastecimiento y reglas
  de compra.
- Odoo nativo no cubre confirmado: pendiente de validar si el proceso requiere una
  accion especifica desde la linea del PM para reservar/entregar stock y generar RFQ
  por faltante.
- Alternativa sugerida: permitir que Almacen registre cantidad cubierta por stock,
  genere reserva/entrega interna, y cree RFQ por la cantidad faltante desde la misma
  linea del PM.
- Tipo: Pendiente
- Preguntas abiertas: si la RFQ queda en manos de Almacen, Suministros o Compras; si se
  crea automaticamente o mediante accion manual; y si requiere aprobacion posterior.
- Fuente: usuario.

#### Respuestas recibidas

- Almacen si reserva stock.
- Almacen entrega stock.
- Almacen deberia poder generar una RFQ desde el PM para las cantidades que no llega a
  suplir con stock.

### Brecha candidata: seguimiento logistico por ComEx

- Estado: pendiente de analisis
- Etapa del flujo: Logistica, recepcion, entrega y cierre de item
- Descripcion: los items derivados a `Logistica` requieren que el responsable de ComEx
  registre recepcion y entrega. No es necesariamente un dropshipping puro: puede
  recibirse en Gottert y luego enviarse al cliente, o recibirse solo en Gottert.
- Impacto operativo: la ruta logistica puede requerir controles de recepcion y entrega
  distintos de una recepcion de almacen o de un dropship nativo proveedor-cliente.
- Odoo nativo cubre: dropshipping proveedor-cliente y operaciones logisticas asociadas.
- Odoo nativo no cubre confirmado: pendiente de validar si la figura de seguimiento de
  Logistica, con recepcion y entrega registradas por ComEx, requiere un modelo o
  workflow adicional.
- Alternativa sugerida: crear o adaptar un estado/documento de seguimiento logistico,
  vinculado al item del PM, compra, recepcion, entrega y evidencia correspondiente.
- Tipo: Pendiente
- Preguntas abiertas: que datos contiene el seguimiento, que evidencia registra ComEx,
  que variantes logisticas existen y como se relaciona con factura del proveedor.
- Fuente: usuario.

## Clasificacion sugerida

Usar estas categorias al registrar cada brecha:

- `Configuracion`: se puede resolver con parametrizacion nativa.
- `Modulo Odoo`: requiere desarrollo dentro de Odoo.
- `App externa`: conviene resolverlo fuera de Odoo.
- `Integracion`: requiere intercambio de datos entre Odoo y otro sistema.
- `Proceso`: no requiere desarrollo, sino cambio operativo o definicion interna.
- `Pendiente`: falta informacion para clasificar.

## Plantilla de brecha

```md
### Brecha: <nombre corto>

- Estado: pendiente | confirmada | descartada
- Etapa del flujo: <etapa>
- Descripcion:
- Impacto operativo:
- Odoo nativo cubre:
- Odoo nativo no cubre:
- Alternativa sugerida:
- Tipo: Configuracion | Modulo Odoo | App externa | Integracion | Proceso | Pendiente
- Preguntas abiertas:
- Fuente:
```
