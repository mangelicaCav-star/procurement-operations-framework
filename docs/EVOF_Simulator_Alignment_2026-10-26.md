# EVOF — Alcance acotado para alinear el simulador

**Fecha:** 26 de octubre de 2026. **Estado:** preparado para iniciar comparación e implementación puntual. El simulador no fue modificado por esta publicación. La referencia es el workbook correctivo v0.4.2, con 51/51 comprobaciones locales y evidencia de Excel registrada por separado.

| Regla aceptada | Comportamiento objetivo | Comprobación trasladable |
|---|---|---|
| Recuperación sin fecha válida | Excluir del suministro reconocido y señalar; conservar el faltante completo | 45 confirmadas sin fecha → recuperación 0, faltante 105 |
| Fecha de alternativa ausente/incorrecta | No declarar factibilidad confirmada | Expedite sin fecha no puede ser candidato |
| Precio, cargos o compromisos ausentes | Conservar dato desconocido; no transformarlo en cero | Precio o línea base vacía no habilitan recomendación |
| Cero explícito | Distinguirlo de vacío y permitir cálculo bajo el supuesto declarado | Costo cero o compromisos cero no se borran |
| Selección | Confirmación, plazo, cobertura, calificación y presupuesto antes de comparar costo | 8460 vs 7020, ambas elegibles → alterno |
| Empate | Mostrar ambas opciones equivalentes en costo para decisión humana | 7020 vs 7020 → empate |
| Base | Conservar cantidades y costos del escenario de referencia | Demanda 135, remanente 30, faltante 105, expedite 6310 |

## Secuencia de trabajo

1. Inspeccionar las reglas actuales del simulador privado; no asumir que reproduce los defectos del workbook.
2. Ejecutar estos escenarios y registrar diferencias contra el workbook y la regla operativa.
3. Modificar únicamente diferencias confirmadas dentro de este conjunto.
4. Repetir los 38 casos históricos del simulador y añadir los escenarios nuevos con esperados independientes. Mantener separado el conteo del Excel.
5. Verificar la interacción y los avisos; conservar el acceso privado. Documentar revisión y evidencia antes de declarar paridad.

La prueba desktop de menor costo requiere reconfirmación de ambas opciones elegibles. No impide inspeccionar e iniciar la alineación, pero debe cerrarse antes de declarar aceptación cruzada final.

## Frontera de costos

El simulador documenta un crédito por material ya comprometido; el campo B23 del workbook no gobierna cálculos. No se asume equivalencia. Mantener esa extensión identificada y excluirla del reclamo de paridad mientras no se defina su contrato y se acepte con casos específicos. No implementar una deducción improvisada, ni eliminar un control existente sin revisar su alcance.

No agregar compras multi-entidad, nuevas alternativas, BUD, funciones de producción, capacidad/MOQ nuevos ni mejoras de parking lot. No convertir la preparación de alineación en una reconstrucción del modelo. Los criterios ya confirmados son suficientes para empezar; no hay una actualización del simulador publicada por este documento.
