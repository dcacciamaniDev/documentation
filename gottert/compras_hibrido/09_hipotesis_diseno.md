# Hipotesis de diseno

Registro de alternativas de diseno para el flujo hibrido Gottert + Odoo.

## PM como RFQ

### Pregunta

Para achicar la brecha `pedido de materiales previo a la compra`, se evaluo si seria
compatible que el PM sea la RFQ.

La idea seria que esa RFQ se convierta:

- en OC para los items que no tengan stock;
- en pedido de consumo interno para los items que si tengan stock.

### Evaluacion preliminar

La compatibilidad es parcial.

La RFQ nativa de Odoo esta orientada a compra y proveedor. En el flujo de Gottert, el PM
es una solicitud interna previa que puede contener lineas con destinos distintos:

- stock disponible;
- faltante a comprar;
- Logistica;
- Compras directa.

Por eso, modelar el PM completo como RFQ puede forzar dentro de un documento de compra
lineas que no necesariamente deben comprarse.

### Alternativa recomendada

Mantener el PM como documento interno con lineas y estados por linea.

Desde cada linea:

- si hay stock, generar reserva y entrega interna;
- si falta stock o debe comprarse, permitir que Almacen genere RFQ/OC por el faltante;
- si corresponde Logistica, generar seguimiento logistico;
- conservar siempre referencia a PM, linea de PM y centro de costo.

### Conclusion

`PM completo = RFQ` no parece recomendable como modelo principal.

`Lineas comprables del PM -> RFQ/OC` si parece compatible con Odoo y reduce la brecha.

`Lineas con stock -> pedido de consumo interno` deberia resolverse con Inventario de
Odoo y posiblemente una personalizacion liviana para mantener trazabilidad e imputacion
por centro de costo.

## Opciones para implementar comportamiento tipo PM

### Opcion A: modulo custom de Odoo para PM

Crear un modulo propio dentro de Odoo con modelos como:

- `pedido.materiales`;
- `pedido.materiales.linea`;
- estados de cabecera;
- estados por linea;
- responsable del PM;
- ruteo por linea: Almacen, Compras, Logistica;
- centro de costo por linea;
- referencias a RFQ/OC, movimientos internos y seguimiento logistico.

Ventajas:

- maxima trazabilidad dentro de Odoo;
- reglas de negocio cerca de Inventario, Compras y Contabilidad;
- evita doble carga si reemplaza o integra la webapp;
- permite generar RFQ/OC y movimientos internos desde lineas de PM.

Desventajas:

- requiere desarrollo y mantenimiento;
- hay que disenar bien permisos, estados y acciones por linea;
- si se sobredesarrolla, puede duplicar funciones nativas de Odoo.

Evaluacion preliminar: opcion mas fuerte si el PM es central para Gottert.

### Opcion B: Odoo Studio o customizacion liviana

Usar modelos simples, campos custom, aprobaciones, actividades y vistas para representar
el PM sin crear un modulo profundo.

Ventajas:

- menor costo inicial;
- mas rapido para prototipar;
- util para validar el flujo con usuarios.

Desventajas:

- puede quedarse corto para ruteo por linea, generacion automatica de RFQ/OC,
  movimientos internos y seguimiento logistico;
- mas riesgo de logica dispersa;
- puede ser dificil de mantener si el flujo crece.

Evaluacion preliminar: buena opcion para prototipo o MVP, no necesariamente para el
flujo completo final.

### Opcion C: webapp externa integrada con Odoo

Mantener una webapp para capturar PM y conectarla con Odoo por API.

La webapp gestionaria:

- carga simple por solicitantes;
- responsable y aprobacion inicial;
- adjuntos y comentarios;
- estado inicial del PM.

Odoo gestionaria:

- stock;
- consumo interno;
- RFQ/OC;
- recepciones;
- facturas;
- reportes operativos y contables.

Ventajas:

- experiencia de usuario mas simple para solicitantes;
- menor exposicion del ERP a usuarios no expertos;
- flexible si hay muchas validaciones fuera de Odoo.

Desventajas:

- riesgo de doble fuente de verdad;
- requiere integracion robusta;
- si el ruteo, stock y compras viven en Odoo, mucha logica terminaria duplicada o
  sincronizada.

Evaluacion preliminar: viable si la webapp actual ya esta muy instalada, pero conviene
que Odoo sea la fuente de verdad para estados operativos posteriores.

### Opcion D: enfoque hibrido recomendado

Usar Odoo como fuente de verdad para el PM, con un modulo custom liviano, y opcionalmente
mantener una interfaz externa solo para carga simplificada.

Propuesta:

- PM y lineas viven en Odoo;
- solicitantes cargan desde portal/webapp o formulario simple;
- responsable valida PM;
- Suministros rutea por linea;
- Almacen define cantidad cubierta por stock y faltante;
- lineas con stock generan reserva y entrega interna;
- lineas faltantes generan RFQ/OC, incluso desde Almacen cuando el faltante se detecta
  ahi;
- lineas de Logistica generan seguimiento logistico;
- reportes salen de Odoo filtrando por centro de costo, proveedor, PM y estado.

Evaluacion preliminar: mejor balance entre Odoo nativo y personalizacion controlada.
