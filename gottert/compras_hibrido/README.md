# Gottert - compras hibrido

Carpeta de trabajo para registrar el flujo actual de compras de Gottert y preparar,
mas adelante, un flujo hibrido basado en Odoo nativo mas las personalizaciones
necesarias.

## Objetivo

Centralizar la informacion que se vaya relevando sobre el proceso real de compras:
personas, documentos, sistemas, aprobaciones, excepciones, controles, integraciones y
dolores operativos.

La informacion registrada aca se usara luego para:

- comparar el flujo actual de Gottert contra el flujo nativo de Odoo;
- detectar brechas funcionales;
- decidir que conviene resolver con configuracion nativa;
- decidir que requiere nuevos modulos de Odoo;
- decidir que podria resolverse con aplicaciones externas;
- armar el futuro diagrama de compras hibrido.

## Archivos

- `00_notas_crudas.md`: registro cronologico de todo lo que el usuario vaya pasando.
- `01_flujo_actual_gottert.md`: version ordenada del proceso actual.
- `02_brechas_vs_odoo_nativo.md`: diferencias, faltantes y puntos de ajuste contra Odoo estandar.
- `03_candidatos_personalizacion.md`: ideas de modulos, automatizaciones o apps externas.
- `04_preguntas_abiertas.md`: dudas pendientes para completar el relevamiento.
- `05_glosario_y_actores.md`: actores, areas, sistemas, documentos y conceptos propios de Gottert.
- `06_pedido_de_materiales.md`: detalle funcional del PM, sus validaciones y ruteo por item.
- `07_orden_de_compra.md`: detalle de como Suministros arma OCs en ERP desde items de PM.
- `08_reportes_actuales.md`: reportes actuales del ERP que deben preservarse o redisenarse.
- `09_hipotesis_diseno.md`: alternativas evaluadas para achicar brechas con Odoo
  nativo, incluyendo opciones de implementacion para el comportamiento tipo PM.
- `CHANGELOG.md`: cambios relevantes hechos en esta carpeta.

## Regla de trabajo

Primero se registra la informacion recibida sin forzar conclusiones. Despues se
normaliza en los documentos tematicos, dejando claro que es dato confirmado, inferencia
o pregunta abierta.
