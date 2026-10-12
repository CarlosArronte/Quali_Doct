# Revisión de las citas del paso 5

Se contrastaron las atribuciones del borrador con los PDF proporcionados. La revisión comprueba la correspondencia entre las afirmaciones de la tesis y el contenido de los artículos; no constituye una reproducción de sus resultados experimentales.

## Referencias conservadas en el paso 5

| Clave | Contenido comprobado en el PDF | Uso en la versión corregida |
| --- | --- | --- |
| `Su2026ReinforcementLearningBased` | La introducción, página 18857, describe predicción sobre un horizonte finito, restricciones y optimización en MPC. El trabajo emplea aprendizaje por refuerzo como solucionador del controlador nominal, junto con un controlador auxiliar. | Descripción del funcionamiento de MPC/NMPC. Se retiró la atribución de que el artículo establece como conclusión la distinción entre parámetros físicos, nominales y estimados. |
| `Chen2026Hybrid` | La sección 2, páginas 2–3, presenta un modelo bicicleta simplificado con estados de posición, orientación, velocidad y velocidad de guiñada. Distingue modelo nominal, dinámica residual y ruido. | Compromiso entre precisión del modelo y costo computacional. Se eliminó su identificación como modelo lineal de dos grados de libertad. |
| `Pan2026A` | Resumen e introducción, páginas 1–2: incertidumbre por estructura del modelo y errores paramétricos; compromiso entre precisión y complejidad; control robusto con restricciones ajustadas. | Fuentes de discrepancia entre modelo orientado al control y vehículo. Se retiraron consecuencias universales y afirmaciones de recuperación exacta de límites físicos. |
| `Yeneneh2026AutoDyn` | El artículo define un vector paramétrico de masa, rigideces laterales delantera y trasera, y fricción. Su formulación incorpora incertidumbre paramétrica y evalúa el control mediante simulación. | Ejemplo de tratamiento de incertidumbre en esos parámetros. Se eliminó la atribución conjunta de un modelo lineal de dos grados de libertad. |
| `Li2026TrajectoryTracking` | Resumen, introducción y formulación: acoplamiento longitudinal/lateral, incertidumbre de rigidez lateral y momento de inercia de guiñada, ley de adaptación y pruebas hardware-in-the-loop. | Ejemplo de incertidumbre paramétrica más allá de la fricción. Se retiró la afirmación de que los valores nominales se obtienen necesariamente mediante identificación offline en condiciones estándar. |
| `Chen2026DataMechanism` | Resumen y secciones II–III: calibración del modelo físico nominal mediante optimización bayesiana y compensación de dinámica no modelada; actualización de coeficientes de fusión mediante DEKF. | Evidencia de que calibrar parámetros y compensar dinámica no modelada son operaciones distintas. Se eliminó la atribución de que el método ajusta límites de optimización para coincidir con los límites reales de fuerza de los neumáticos. |

## Otras referencias citadas en el borrador

| Clave | Resultado de la revisión | Decisión |
| --- | --- | --- |
| `Ma2026ObserverBased` | El resumen describe aprendizaje por imitación de la política NMPC, agregación de datos y un observador de velocidad lateral/fricción. La red residual mencionada forma parte de la política; no justifica presentarla como estimador de residuales de dinámica. | Se retiró la cita del paso 5. |
| `Zhou2026Integrated` | El resumen presenta Tube-RMPC para vehículos pesados articulados, control de guiñada y simulaciones con incertidumbre y perturbaciones. Ese contenido no basta para sostener todas las afirmaciones sobre carga, desplazamiento del centro de gravedad y divergencia atribuidas en el borrador. | Se retiró la cita del paso 5. |
| `Jalalnezhad2026A` | El artículo desarrolla una política PPO para seguimiento de un robot móvil con suavizado de acciones. Los pasajes revisados no aportan una justificación específica de degradación de rigidez lateral por temperatura, desgaste o saturación. | Se retiró la cita del paso 5. |
| `Sun2026Model` | Es una revisión de MPC en transporte de carretera, ferroviario, aéreo y marítimo. Discute incertidumbre y costo computacional, pero no se utilizó como evidencia específica de que cambios paramétricos automotivos producen necesariamente divergencia o violaciones de restricciones. | Se sustituyeron sus citas por fuentes primarias con correspondencia más directa. |

## Correcciones del argumento

- El uso de un modelo interno se refiere a los controladores predictivos; no se impone a todo controlador automotivo.
- La masa total y el reparto de carga no se representan indistintamente mediante una sola variable de masa.
- La saturación de fuerza del neumático no se presenta como sinónimo de reducción de rigidez lateral.
- Los cambios físicos pueden ocurrir entre recorridos o durante uno; no se presupone que todos varíen continuamente.
- La compensación o adaptación no garantiza que una estimación coincida con el parámetro real.
- Los detalles de las soluciones aprendidas se reservan para el paso 6.

## Limpieza de `referencias.bib`

Se examinaron las citas activas de todos los archivos `.tex` del proyecto. Tras corregir el paso 5, se eliminaron 11 entradas sin uso:

`Perez2019Skid`, `Yang2026Stability`, `Yu2027KnowledgeData`, `Jiang2026GeometryDynamics`, `Li2026An`, `Zhou2026Integrated`, `Ma2026ObserverBased`, `Tsakiris2026TimeComfort`, `Jalalnezhad2026A`, `Sun2026Model` y `Jin2026Active`.

Quedan 18 entradas. Todas las claves citadas tienen una entrada correspondiente. Los PDF originales permanecen en su ubicación.
