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
