# EVOF — Cierre de sprint del 26 de octubre de 2026

**Disposición:** cierre de ejecución del sprint acotado, con reservas explícitas de aceptación. El modelo de portafolio MRP/project-cost queda en revisión correctiva v0.4.2. No se declara terminado todo EVOF ni una liberación productiva.

## Objetivo y resultado

El objetivo fue verificar en Excel 365 el escenario base, cinco correcciones y el empate, homologar fechas y documentar el estado. La agenda propuesta fue de 60 minutos. No existe cronometraje fiable para afirmar cumplimiento o desviación de duración.

| Plan | Trabajo realizado | Estado |
|---|---|---|
| Escenario base | 105 piezas, expedite USD 6,310, proyección USD 26,310 confirmados por la usuaria | PASS reportado |
| Cinco correcciones | Cuatro casos de datos faltantes confirmados; selección por menor costo reportada PASS con reserva de preparación | Aceptación acotada |
| Empate | Tras corregir la fecha de expedite, la usuaria confirmó el resultado de empate | PASS reportado |
| Homologar fechas | Nueve celdas usan yyyy-mm-dd, incluidos Parametros B25 y Alternativas C2:C4 | Comprobado localmente |
| Aclarar B23 | No se obtuvo definición suficiente del material ya comprometido | Pendiente explícito |
| Documentación | Registro de Excel, cierre, reglas para alinear simulador y evidencia local separados | Entregados |

La evidencia de Excel suma siete casos con respuesta positiva de la usuaria: seis se conservan como confirmaciones del caso solicitado y uno, menor costo, requiere reconfirmar sus condiciones de elegibilidad. No se presenta como siete casos independientemente observados. Véase el registro detallado de Excel 365.

## Reserva de la prueba de menor costo

Se reportó EVALUAR ALTERNO con expedite USD 8,460 y alterno USD 7,020. En la prueba posterior de empate, una captura mostró que expedite carecía de fecha válida y por ello no era elegible. No se cuenta con una captura anterior que demuestre que ambas alternativas sí lo eran durante la comparación de menor costo. La reserva afecta la trazabilidad del caso; no demuestra un fallo de la fórmula. Las 51 comprobaciones locales incluyen la comparación con ambas alternativas elegibles y pasan.

Para aceptación estricta en Excel: repetir el caso con B19:B21=1, B12=3000, fechas válidas 29/oct/2026 y 28/oct/2026, presupuesto 40000 y compromisos 20000. Confirmar ambas filas como FACTIBLE CONFIRMADA y CANDIDATA A APROBACION, y después EVALUAR ALTERNO. Este punto es una reconfirmación del mismo alcance, no una funcionalidad nueva.

## Correcciones y evidencia

R01 excluye y señala recuperación sin fecha válida. R02 impide usar una fecha ausente como plazo cumplido. R03 y R04 mantienen desconocidos los precios y compromisos vacíos; preservan ceros explícitos. R05 compara el costo entre opciones elegibles y muestra empate para revisión humana.

La revisión de formato del 26/oct cambió únicamente la presentación de fechas. Se verificaron valores y fórmulas iguales a la revisión corregida del 25/oct. Antes de publicar se volvió a ejecutar la batería de 51 comprobaciones sobre el archivo final: **51 PASS / 0 FAIL**. No se suman esta repetición ni los 38 casos históricos del simulador a ese total.

La usuaria informó restaurar el escenario base. La última captura de parámetros contenía B25 con año 2025 y fecha alterna 29/oct; la copia maestra entregada conserva 29/oct/2026 en B25 y 28/oct/2026 en B18. No se afirma haber verificado el archivo local de la usuaria después de esa observación. El binario publicado es la copia maestra restaurada y comprobada localmente.

## Pendientes y límites

- B23, material ya comprometido: el campo no participa en el cálculo del workbook. No se puede afirmar eliminación de doble conteo por modificarlo. Definir su relación con la línea base antes de cambiar esa regla.
- Reconfirmar el caso de menor costo en Excel con ambas opciones elegibles.
- La evidencia nativa es reportada por la usuaria, con capturas parciales. No es una regresión exhaustiva de Excel.
- ERP, cotizaciones, capacidad, recepciones, costos y autorizaciones reales no se validaron.
- BUD, compras multi-entidad, MOQ/capacidad nuevos y mejoras de parking lot no se incorporan a este cierre.

## Preparación del simulador

**Listo para iniciar una actualización acotada de alineación**, no para afirmar paridad ya completada. Las reglas de datos obligatorios, recuperación, elegibilidad, menor costo y empate están definidas y tienen casos locales reproducibles. Se debe inspeccionar su implementación actual, modificar solo diferencias y repetir las pruebas del simulador más los casos trasladados.

La regla de crédito por material comprometido ya existe como extensión en el simulador; no debe presentarse como equivalente a B23 ni alterarse sin aclaración. Las extensiones de reasignación, MOQ y capacidad conservan su estado separado. El simulador y el sitio no se modificaron en este sprint.

## Valor aportado

Se obtuvo evidencia de uso en Excel, se verificaron protecciones que evitan recomendaciones con datos incompletos y se hizo explícito el empate. La revisión detectó valores de prueba no restaurados y separó problemas de preparación del escenario de posibles fallos del motor. El cierre permite continuar con una base más precisa, sin ampliar el alcance ni esconder pendientes para obtener un cierre nominal.
