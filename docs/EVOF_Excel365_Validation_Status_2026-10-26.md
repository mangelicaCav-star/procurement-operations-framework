# EVOF v0.4.2 — Registro Excel 365, 26 de octubre de 2026

**Procedencia:** pruebas ejecutadas por la usuaria en su Excel y confirmadas en conversación. Capturas parciales revisadas para la investigación del empate. No existe ejecución de Excel 365 controlada de forma independiente por el asistente, ni se recibió el archivo local de prueba para verificar su estado final.

| ID | Caso | Esperado principal | Evidencia y estado |
|---|---|---|---|
| EV26-01 | Escenario base | Faltante 105; costo 6310; forecast 26310 | PASS reportado por usuaria |
| EV26-02 | Recuperación confirmada sin fecha | Recuperación reconocida 0; faltante 105; aviso de exclusión | PASS reportado |
| EV26-03 | Expedite sin fecha | FECHA REQUERIDA; DATOS REQUERIDOS; no recomendar esa opción | PASS reportado |
| EV26-04 | Precio unitario vacío | COSTO REQUERIDO en costo/forecast; DATOS REQUERIDOS / REVISAR | PASS reportado |
| EV26-05 | Compromisos vacíos | LINEA BASE REQUERIDA; no recomendar compra | PASS reportado; usuaria indicó valor restaurado |
| EV26-06 | Alterno confirmado más barato | Expedite 8460; alterno 7020; EVALUAR ALTERNO con ambas candidatas elegibles | PASS reportado con condición de preparación por reconfirmar |
| EV26-07 | Empate de costo | Costos 7020 y 7020; EMPATE DE COSTO / REVISAR con ambas elegibles | PASS reportado después de restaurar fecha válida de expedite |

**Conteo:** siete resultados positivos reportados, de los cuales seis corresponden a confirmaciones aceptadas para los casos solicitados y uno conserva reserva sobre sus precondiciones. No reportar 7/7 como validación estricta sin esa reserva. Las siete pruebas del 21/oct pertenecen a una revisión anterior y se mantienen separadas.

## Diagnóstico observado durante el empate

Una captura inicial mostró Control_Decision B3=EVALUAR ALTERNO y variación −30980. Se corrigió Proyectos C2 a 20000 y la variación pasó a −12980. Una captura de Alternativas mostró ambos costos en 7020, pero expedite con FECHA REQUERIDA y COMPLETAR FECHA, mientras alterno era candidata. La selección de alterno era correcta bajo esas condiciones. Después de indicar una fecha válida en Parametros B17, la usuaria confirmó los resultados esperados de elegibilidad y empate.

Esta secuencia demuestra el valor de comprobar precondiciones y evita registrar un falso fallo del empate. También deja la prueba EV26-06 con reserva: no se observó que ambas alternativas fueran elegibles antes de su respuesta inicial.

## Reconfirmación mínima de EV26-06

Partir de una copia de prueba del workbook v0.4.2, conservar stock 90, demanda previa 60, FG 25→45, BOM 3, recuperación previa 0. Parametros B10=52, B12=3000, B13=64, B14=300, B15=30/oct/2026, B17=29/oct/2026, B18=28/oct/2026, B19:B21=1. Proyectos B2=40000 y C2=20000. Exigir M3:M4=FACTIBLE CONFIRMADA y N3:N4=CANDIDATA A APROBACION, antes de confirmar G3=8460, G4=7020 y Control_Decision B3=EVALUAR ALTERNO. Registrar las filas y restaurar la base después.

## Formato y restauración

Se homologaron nueve celdas de fecha a yyyy-mm-dd: Parametros B2, B15:B18, B25 y Alternativas C2:C4. El formato no corrige una fecha del año equivocado. La última captura del usuario tenía B25=29/10/2025; el archivo maestro entregado y publicado tiene 29/10/2026. Se preservaron en él las demás entradas base y fórmulas. La restauración final del archivo local de la usuaria después de esta observación no fue inspeccionada.

**Aceptación:** los resultados respaldan el prototipo de portafolio en el alcance definido. EV26-06 queda por reconfirmar en condiciones completas. No constituyen validación productiva, autenticación de confirmaciones o prueba de integración ERP.
