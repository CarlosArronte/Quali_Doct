# Revisión de la introducción hasta Research problem

Revisión del 13 de octubre de 2026. Comprende el texto de los pasos 1–7, anterior a `Research problem`. Este informe actualiza la ubicación y función de las citas; los informes de los pasos 5, 6 y 7 conservan el detalle de las comprobaciones anteriores.

## Coherencia y redacción

- Se mantiene el ejemplo inicial como situación hipotética, sin atribuirle datos de un accidente documentado.
- La secuencia pasa de los límites de fuerza a la asistencia de control, las variaciones del vehículo, las discrepancias del modelo, los modelos híbridos y la evaluación del residual durante la operación.
- Se reducen las reiteraciones sobre el alcance de la tesis y sobre la necesidad de comprobar la validez del residual. El cierre del paso 7 concentra el planteamiento que conduce al problema de investigación.
- Se distinguen cambios físicos, incertidumbre sobre valores paramétricos y errores de representación. La incertidumbre no se presenta como una modificación física del vehículo.
- Se explica la rigidez lateral en el rango lineal y se diferencia de la capacidad de fuerza limitada por la fricción.
- Se mantiene el alcance sobre fricción, masa/carga y propiedades de los neumáticos.
- Se desarrollan las siglas al introducirlas y se evita usar MPC antes de su definición en el paso 5.

## Correspondencia de las referencias

La revisión combina los PDF completos comprobados en las revisiones anteriores con originales, versiones de autores, resúmenes editoriales y registros institucionales consultados en esta revisión. La comprobación bibliográfica no reproduce los experimentos. Algunos PDF originales ya no estaban disponibles con los nombres proporcionados; no se presenta la revisión como una nueva lectura completa de todos ellos.

| Fuentes | Afirmación respaldada y alcance |
| --- | --- |
| `Bertipaglia2024Model`, `Hu2025Lanechanging` | Límites de fuerza y dificultad de maniobras con baja adherencia. No se atribuye el accidente hipotético a sus experimentos. |
| `Weng2026Leveraging`, `Isasa2025ASkid` | Relación de la fricción con textura y características de la vía. Se elimina la atribución específica sobre pulido de agregados por el tráfico, que requería evidencia más directa. |
| `Salleh2019Performance` | Acumulación de agua en surcos y riesgo de hidroplaneo. El pasaje aparece en la introducción del [original institucional](https://eprints.utm.my/89085/1/ShamsuniSalleh2019_PerformanceofRalumacMicro.pdf), p. 2. Sustituye a Rajendra en esta afirmación. |
| `BoschNDSafe`, `Bosch2025ESP` | Función del ABS y antecedente de ESP. Son fuentes oficiales del fabricante, utilizadas para función e historia; no se les atribuyen resultados científicos de control. |
| `Skrickij2024Review` | Coordinación de actuadores, estimación de estados/parámetros y relación fuerza lateral–ángulo de deriva en el rango lineal. Se comprobó el [texto completo del repositorio de Delft](https://repository.tudelft.nl/file/File_762c1d78-ad36-42b9-9d10-e4aad5197e1f), especialmente la revisión de modelos y estimación de rigidez lateral. |
| `Yun2026RealTime`, `Xu2026Parallel`, `Yeneneh2026Adaptive` | Cargas por eje y predicción de frenado; seguimiento con fricción variable; actualización de parámetros de un modelo lateral. Se evita atribuir a cada estudio ensayos de todos los parámetros considerados por la tesis. Los resultados de seguimiento se identifican como simulaciones. |
| `Su2026ReinforcementLearningBased`, `Pan2026A`, `Li2026TrajectoryTracking`, `Yeneneh2026AutoDyn` | Predicción con restricciones, discrepancias estructurales y paramétricas, e incertidumbre en parámetros del vehículo. Las pruebas de Li se identifican como hardware-in-the-loop. AutoDyn no se presenta como prueba de invalidez de un residual aprendido. |
| `Chen2026Hybrid`, `Chen2026DataMechanism` | Modelo simplificado, corrección residual y actualizaciones; calibración nominal y compensación de dinámica no modelada. Se conserva la distinción entre calibración de parámetros y compensación de discrepancias. Véase también `revision_citas_paso5.md`. |
| `Kabzan2019LearningBased`, `Zhou2025Hybrid` | Residual aditivo aprendido de transiciones medidas y resultados de predicción en un vehículo de competición; red de tracción y estimación de parámetros longitudinales. El resultado de Kabzan se expresa como error de predicción. La arquitectura de Zhou y su coeficiente modificado de fricción de rodadura se distinguen del residual aditivo y de la adherencia disponible. |
| `Cheng2025Deep`, `Bertipaglia2024An`, `Wang2027Adaptive` | Fusión de modelos, estimación de deriva y uso de ecuaciones físicas en el entrenamiento. No se agrupan como si todas fueran correcciones aditivas de dinámica. Véase `revision_citas_paso6.md`. |
| `Kalaria2024Adaptive`, `Brunke2022Safe`, `Chen2026Hybrid` | Actualización de modelos de neumático, dificultades por datos escasos/cambios de distribución y motivación de actualizaciones online. Se distingue el desgaste simulado de ensayos de desgaste físico. El ejemplo de cambio de carga se identifica como conceptual; no se afirma que todo cambio invalide el residual. Véase `revision_citas_paso7.md`. |

## Ajustes bibliográficos

- Se añade [Safe Braking, de Bosch](https://www.bosch.com/stories/beginnings-of-abs/), como respaldo directo de la función del ABS. La página no muestra fecha de publicación: se registra `n.d.` y la fecha de consulta.
- La cita de `Rajendra2013Development` se retira de la afirmación sobre agua en surcos. El contenido accesible identifica un estudio sobre rugosidad y deterioros superficiales; Salleh proporciona el respaldo directo requerido.
- Se completan los identificadores de artículo de Weng (`111794`) e Isasa (`365`).
- En Yeneneh se conserva el año de la edición de revista, 2026, y se añade la fecha de publicación online, 30 de noviembre de 2025, verificada en la [página del editor](https://www.nature.com/articles/s41598-025-30352-3).
- Se conservan los registros importados que no se citan en esta parte. Su presencia en el `.bib` no implica que respalden el argumento actual; la bibliografía del PDF incluye las entradas citadas.

La selección del residual aditivo y la necesidad de relacionar error de modelo con decisiones de control se presentan como planteamientos de la tesis, sin atribuirlos como resultados de un artículo externo. La brecha de investigación y las posibles garantías siguen pendientes de la revisión específica correspondiente.

## Verificación del documento

Se comprobaron 30 registros bibliográficos y 24 claves citadas, sin claves duplicadas ni citas sin entrada. El PDF actualizado compila sin errores ni referencias indefinidas. Permanece un aviso de justificación de una línea en la bibliografía (`Underfull hbox`), sin desbordamientos de texto. Se leyó el texto extraído del PDF para confirmar que contiene la versión corregida de la introducción.
