# EVOF — Correcciones y regresión local

**Fecha:** 25 de octubre de 2026. **Revisión:** v0.4.2 correctiva local, sobre el workbook v0.4.1. **Resultado: 51/51 comprobaciones PASS.** Los cinco fallos R01–R05 reportados antes de la corrección ya no se reproducen en el motor local. Esto no equivale a validación en Excel 365 ni a liberación productiva.

## Criterios confirmados por la usuaria

1. Recuperación marcada como confirmada pero sin fecha válida: **excluir y señalar**. No reducir el faltante ni bloquear globalmente las otras alternativas por esa recuperación.
2. Comparar costos después de filtrar confirmación, plazo, calificación cuando aplica y presupuesto.
3. Si las candidatas cumplen y cuestan lo mismo: **mostrar empate para revisión humana**, sin priorizar por orden de filas ni fecha más temprana.

Los costos y compromisos vacíos se consideran desconocidos. Un cero explícito numérico se conserva como valor informado; la prueba no verifica que esa captura represente un costo real. Una candidata con datos incompletos no puede habilitar recomendación; una alternativa independiente con datos completos puede seguir evaluándose.

## Cambios realizados

| Falla | Corrección | Evidencia representativa |
|---|---|---|
| R01: recuperación sin fecha descontada | Validar tipo, rango y día entero de fecha de recuperación y necesidad. Excluir si falta y mostrar aviso en MRP_Cambio. | Recuperación 45 sin fecha: reconocida 0 y faltante 105. |
| R02: expedite sin fecha factible | Validar fechas antes de comparar plazo. | Fecha ausente: DATOS REQUERIDOS y ninguna recomendación de esa opción. |
| R03: precio vacío tratado como cero | Validar precio y cargos antes de sumar. Propagar COSTO REQUERIDO. | Precio ausente no produce USD 850 como si el material fuera gratuito. |
| R04: compromisos vacíos tratados como cero | Exigir línea base y presupuesto numéricos para evaluar costo proyectado y elegibilidad presupuestal. | Línea base ausente no habilita EVALUAR EXPEDITE. |
| R05: prioridad fija de expedite | Comparar costos de las candidatas elegibles; empate explícito. | Expedite USD 8,460 vs alterno USD 7,020: EVALUAR ALTERNO. |

Se ajustaron 30 fórmulas de las áreas afectadas y sus dependencias, más textos de guía y reglas. No se agregaron hojas ni alternativas. Los costos, fechas y cantidades fuente del escenario original permanecen iguales en el archivo entregado. Se ajustó el alto de filas y la envoltura de textos afectados para que los estados sean legibles.

La factibilidad técnica y el costo se mantienen separados: una fecha y confirmación válidas no suplen un precio o presupuesto faltante. `Alternativas!N` expone la acción pendiente. La recomendación final usa únicamente candidatas que cumplen todos los criterios. El indicador de menor costo a tiempo puede incluir una opción potencial; su texto aclara que no es autorización de compra.

## Validación ejecutada

| Grupo | Ejecutadas | PASS | FAIL |
|---|---:|---:|---:|
| prior-13-reexecuted | 13 | 13 | 0 |
| additional-valid-cases | 13 | 13 | 0 |
| fault-injection-coverage | 1 | 1 | 0 |
| robustness-and-decision | 5 | 5 | 0 |
| correction-boundaries | 19 | 19 | 0 |
| **Total** | **51** | **51** | **0** |

Los 32 controles anteriores se repitieron sobre el Excel corregido. Se añadieron 19 comprobaciones de borde para los cambios y los criterios elegidos. Las repeticiones del ejecutor no se suman. Los casos son comprobaciones agrupadas, no 51 flujos independientes ni una regresión exhaustiva.

El escenario base conserva demanda 135, stock remanente 30 y faltante 105. El expedite sigue en USD 6,310 y la proyección en USD 26,310 frente a presupuesto de USD 25,000. Con recuperación confirmada y oportuna de 45, el faltante sigue en 60, el expedite en USD 3,970 y la proyección en USD 23,970.

### Pruebas de borde adicionales

| ID | Caso | Resultado |
|---|---|---|
| E01 | Recuperación sin fecha excluida y señalada | PASS |
| E02 | Fecha recuperación inválida no cuenta | PASS |
| E03 | Fecha recuperación inválida no cuenta | PASS |
| E04 | Fecha recuperación inválida no cuenta | PASS |
| E05 | Fecha recuperación igual a necesidad se acepta | PASS |
| E06 | Expedite sin fecha no impide evaluar alterno válido | PASS |
| E07 | Costo unitario cero explícito sigue permitido | PASS |
| E08 | Compromisos cero explícitos siguen permitidos | PASS |
| E09 | Costo de expedite faltante no bloquea alterno válido | PASS |
| E10 | Empate se presenta para revisión humana | PASS |
| E11 | Alterno barato sin confirmar no desplaza confirmado | PASS |
| E12 | Primero se filtra presupuesto luego se compara costo | PASS |
| E13 | Presupuesto vacío no da recomendación | PASS |
| E14 | Extra de expedite faltante no es cero | PASS |
| E15 | Fecha necesidad vacía impide factibilidad | PASS |
| E16 | Fecha expedite fraccionaria no acredita plazo | PASS |
| E17 | Precio texto no acredita costo | PASS |
| E18 | Precio negativo no habilita evaluación | PASS |
| E19 | Extra cero explícito sigue válido | PASS |

El archivo de evidencia `regression-results.json` conserva esperados, obtenidos, ubicaciones o pasos y resultado. `regression.mjs` permite repetir las pruebas con Artifact Tool compatible y no sobrescribe el Excel. Los esperados económicos se calculan desde las entradas, de forma independiente de las fórmulas corregidas.

El escaneo final encontró cero marcadores de error de Excel. Se inspeccionaron visualmente las áreas modificadas. La comparación del archivo exportado contra la fuente confirmó mismas hojas, validaciones y formato condicional, y ningún cambio de contenido ajeno al conjunto autorizado.

## Versiones y conservación

- Fuente v0.4.1 SHA-256: `5258d3d6dc4d8cb6e11b02193cfd2d1d00de6486669873384b829e0de39fa5e2`.
- Corrección local v0.4.2 SHA-256: `4008d1681e4d0104922220019c915344a4ee58823241341b147c590d9ac92625`.
- El nombre histórico del archivo se conserva para dar continuidad al libro de trabajo; la revisión correctiva se identifica en la guía y en este reporte.
- Los inputs quedan restaurados al escenario base; no se guardan los valores usados para provocar fallos.
- La hoja Pruebas conserva evidencia histórica identificada como tal. El reporte de la mañana con 27 PASS y 5 FAIL se mantiene como registro previo, no se reescribe como si nunca hubiera habido defectos.

## Límites y pendientes

Las pruebas fueron de recálculo local. No se repitieron en Microsoft Excel 365, ni sobre ERP, cotizaciones o confirmaciones reales. La evidencia anterior de siete casos Excel 365 y 38 casos del simulador continúa separada y no se transfiere a esta revisión.

No se modificó el tratamiento de `Parametros!B23` (material ya comprometido), que no gobierna los cálculos actuales. Su definición y conciliación deben aclararse antes de afirmar eliminación de doble conteo. No se agregaron validaciones de claves entre proyectos, capacidad/MOQ, múltiples entidades, integración con BUD ni mejoras de parking lot. Esos puntos no se presentan como corregidos por este trabajo.

La corrección cubre los cinco fallos autorizados y los criterios confirmados, sin afirmar que todo el modelo esté certificado. No se publicaron cambios en GitHub ni en el sitio web.
