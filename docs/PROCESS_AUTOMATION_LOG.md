# EVOF — Bitácora de procesos y preparación para orquestación

**Inicio:** 2026-10-20 · **Estado:** registro complementario de diseño, no implementación de agentes · **Alcance:** preparación documental para integración manual y eventual LLM/tool chaining.

## Propósito y límites

Documentar cada proceso a medida que se implemente o revise, preservando entradas, reglas, actores, resultados, validaciones y excepciones. **No cambia el alcance de los sprints, no valida funcionalidad pendiente y no implica que exista integración ERP, agente o automatización en producción.** Las descripciones siguientes son un **inventario inicial de trabajo** y deben contrastarse con los artefactos funcionales actuales al cerrar cada proceso.

## Plantilla obligatoria por proceso

- **ID, versión, fecha, owner y estado:** diseñado / implementado / validado localmente / validado en Excel 365 / bloqueado / futuro.
- **Evento disparador y alcance:** inicio, fin, condiciones previas y exclusiones.
- **Entradas y contratos de datos:** fuente, ID, granularidad, campos obligatorios, moneda/unidades, frescura y linaje.
- **Transformaciones y reglas:** secuencia, cálculos deterministas, tablas de decisión y supuestos explícitos.
- **Responsabilidades:** dueño del dato, ejecutor, responsable de validación, autoridad de aprobación y segregación de funciones.
- **Salidas y destinos:** registros producidos, esquema, consumidores y evidencias.
- **Excepciones y recuperación:** faltantes, inconsistencias, duplicados, errores y ruta de escalamiento.
- **Control y evidencia:** pruebas, caso reproducible, artefacto/versión y resultado (sin confundir pruebas locales con Excel 365).
- **Potencial de orquestación FUTURA:** pasos fijos, herramientas deterministas, tareas interpretativas candidatas a LLM, aprobaciones humanas, permisos, registros y límites.
- **Dependencias BUD ↔ EVOF:** contrato de interfaz propuesto, sin presumir integración existente.

## Inventario inicial de procesos (hipótesis documentales; validar uno por uno)

| ID | Proceso | Entradas | Reglas o trabajo | Salida | Estado / limitación |
|---|---|---|---|---|---|
| EVOF-P01 | Recepción y normalización de requerimientos | Necesidades de materiales, proyecto, fechas, IDs | Validar completitud, unidades, maestro de materiales y relación proyecto | Requerimientos listos para análisis | Contratos ERP v2.0 conceptuales; sin integración viva |
| EVOF-P02 | Evaluación de proveedores y RFQ | Cotizaciones, condiciones, costo total, lead times | Aplicar criterios documentados y registrar supuestos | Comparativo y recomendación | Validar pesos, elegibilidad y calidad de información |
| EVOF-P03 | Cobertura y planeación MRP | Demanda fechada, inventario, órdenes abiertas y fechas | Calcular cobertura temporal sin sumar disponibilidad posterior a la fecha de necesidad | Brecha de materiales y fechas objetivo | Validar escenarios de límites; no equiparar cálculo local con ERP |
| EVOF-P04 | Alternativas de abastecimiento y costo de proyecto | Escenarios esperar/expeditar/alternar, costos incrementales | Comparar factibilidad temporal, impacto presupuestal y riesgo | Alternativas justificadas | Piloto v0.4 parcialmente validado; pruebas pendientes |
| EVOF-P05 | Aprobación y trazabilidad de PO | Reglas de autorización, responsable, referencias, cambios | Evaluar elegibilidad y registrar cambios; no autenticar aprobadores sin sistema fuente | Estado de aprobación consultivo y log | Controles consultivos del prototipo; sin bloqueo transaccional |
| EVOF-P06 | Monitoreo de proveedores, riesgos y KPI | PO abiertas, riesgos, eventos de recepción, métricas | Calcular indicadores solo con eventos verificables | Alertas, KPIs y excepciones | Recepciones reales incompletas; OTD no verificable todavía |

## Registro incremental de ejecución

| Fecha | Proceso | Cambio / decisión | Referencia al archivo o prueba | Estado real | Dependencia / siguiente acción |
|---|---|---|---|---|---|
| 2026-10-20 | General | Se crea plantilla transversal para documentar procesos orientados a futura automatización, sin construir agentes | README + esta bitácora | Documentación creada | Completar fichas con la implementación real conforme cierren los sprints |

## Puertas de avance

1. **Baseline individual:** funcionalidad cerrada, reglas y contratos registrados, evidencia de pruebas con limitaciones.
2. **Integración manual BUD–EVOF:** identificadores y conversiones definidos; escenarios end-to-end reproducibles; conciliaciones y excepciones documentadas.
3. **Diseño de orquestación:** separar motores deterministas de LLM, definir permisos, trazas, evaluación y aprobación humana.
4. **Piloto:** ejecución en entorno aislado contra casos de referencia manual, sin escrituras reales al ERP ni aprobaciones automáticas.

## Principios de diseño

- No sustituir cálculo MRP, FX o finanzas por texto generado por LLM.
- No asumir autenticación de aprobaciones ni integridad de datos no disponibles.
- Registrar versión, procedencia y evidencia; preservar la decisión manual cuando corresponda.
- Cualquier decisión sobre agentes se considera **futura** hasta terminar y validar la integración manual.


## Actualización de simulación privada — 2026-10-22

**Artefacto:** simulador EVOF 1.0. **Owner de revisión funcional:** Angelica Martinez. **Estado:** implementado y validado en motor JavaScript con datos ficticios; no validación productiva ni integración entre proyectos. [Guía](./EVOF_Simulator_Guide.md) y [matriz de 38 casos](./EVOF_Simulator_Validation_2026-10-22.md).

| Registro | Disparador / entradas | Reglas / transformación | Responsables y autoridad | Salidas / evidencia | Excepción y recuperación |
|---|---|---|---|---|---|
| EVOF-SIM-P01 | Cambio MPS FG-B; BOM; stock compartido; consumo fechado; evidencia de recuperación | Recalcular demanda, conservar déficit previo y descontar solo cobertura verificable y oportuna | Planeación valida demanda; Almacén, posición; Compras, suministro; owner revisa lógica | Demanda y faltante residual; casos de cobertura del motor | Faltante o recuperación sin evidencia conserva exposición; corregir supuesto y recalcular |
| EVOF-SIM-P02 | Faltante + alternativas + fechas, confirmaciones, costo y presupuesto | Ventanas por alternativa; cobertura; factibilidad; presupuesto; comparación entre candidatas | Compras confirma cantidad/ETA; Ingeniería valida; Finanzas valida costos; autoridad humana aprueba | Comparativo, costo incremental, forecast y siguiente frontera de decisión | Parcial/tardía no resuelve todo; sobrepresupuesto escala; sin opción preventiva pasar a gestión de impacto |
| EVOF-SIM-P03 | Posición donante, autorización, reposición, fecha origen y asignación propuesta | Proteger proyecto origen y receptor; contar material una vez; conservar obligación de reposición | Proyectos origen/receptor y Finanzas revisan conjuntamente | Cantidad transferida, residual, buffer y ambos presupuestos | Sin evidencia de reposición o mitigación aprobada no declarar factibilidad confirmada |

**Contrato y procedencia:** escenarios sintéticos, unidades y moneda visibles, versión fuente y corte separados del escenario. Los supuestos editados no constituyen hechos ERP ni autorizaciones autenticadas. 38/38 resultados JavaScript PASS y verificación de interacción en navegador; las pruebas de Excel 365 se registran por separado con su procedencia de usuario.

**Dependencia BUD–EVOF:** no hay interfaz ejecutada. El intercambio manual necesita IDs, moneda, reglas aceptadas y pruebas cruzadas antes de cualquier orquestación. **LLM/agentes:** futuro; ningún motor determinista se sustituye por texto generado. Exportar JSON permite revisar el caso, no crea una bitácora inmutable.

**Siguiente puerta:** comparar escenarios Excel–simulador–criterio operativo, registrar diferencias y aceptar o rechazar las extensiones. No se declara cerrado el backlog pendiente por tener un simulador funcional.
