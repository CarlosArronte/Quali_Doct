# Correspondencia entre afirmaciones y citas del paso 6

Revisión actualizada el 13 de octubre de 2026. Las citas se asignan a afirmaciones concretas, distinguiendo evidencias de los artículos, síntesis del texto y decisiones metodológicas de la tesis.

## Afirmaciones respaldadas

| Afirmación o pasaje del paso 6 | Referencia asignada | Evidencia comprobada |
| --- | --- | --- |
| La combinación de ecuaciones físicas e información aprendida permite abordar discrepancias del modelo. | `Cheng2025Deep`, `Zhou2025Hybrid` | Cheng integra modelos físicos y una red recurrente mediante UKF: resumen, p. 5582, y formulación de interacción entre modelos. Zhou combina red de tracción, dinámica física y estimación de parámetros: resumen, p. 16735, y sección II. |
| Un residual aditivo corrige una predicción física nominal y permite aprender dinámica que el modelo no representa adecuadamente. | `Kabzan2019LearningBased`, `Chen2026Hybrid` | Kabzan distingue dinámica nominal y término aprendido en la sección III; define el modelo corregido y los datos de regresión. Chen distingue dinámica nominal, residual y ruido en la sección 2, pp. 2–3. |
| En la formulación de Kabzan, los objetivos de entrenamiento se obtienen de transiciones medidas y predicciones nominales, sin identificar cada causa física del error. | `Kabzan2019LearningBased` | Sección III-B, «Learning the Model Error»: construcción del dato de regresión mediante la diferencia entre estado observado y predicción nominal. La separación de causas físicas no forma parte de ese objetivo de entrenamiento. |
| Kabzan utiliza regresión por procesos gaussianos y valida el controlador en un vehículo de competición a escala real. | `Kabzan2019LearningBased` | Resumen, sección III-B y sección V de evaluación experimental. |
| El error medio del modelo corregido se mantiene aproximadamente constante mientras crece el error nominal durante vueltas de mayor exigencia. | `Kabzan2019LearningBased` | Sección V, tabla I y discusión en p. 3369. El aumento de casi 40% se refiere al error medio de predicción nominal; no es una medida de error de seguimiento. El texto conserva el resultado cualitativo. |
| Zhou combina una red de tracción con dinámica física y estimación de masa y coeficiente modificado de fricción de rodadura. | `Zhou2025Hybrid` | Resumen y secciones II–III. El coeficiente modificado representa el término de resistencia en su formulación y no se identifica con la adherencia neumático–carretera. |
| La evaluación de Zhou incluye cargas y condiciones de vía distintas de las utilizadas para entrenamiento. | `Zhou2025Hybrid` | Sección V: caso 1 con condiciones representadas durante entrenamiento; caso 2 con pasajeros adicionales; caso 3 con carga adicional, pendiente y baja adherencia. La afirmación queda limitada a esos casos. |
| Otras arquitecturas fusionan predictores físicos y neuronales o acoplan una red y un observador para estimar deriva. | `Cheng2025Deep`, `Bertipaglia2024An` | Cheng emplea interacción física–RNN mediante UKF. Bertipaglia utiliza CNN para pseudomediciones del ángulo de deriva y parámetros de ruido de proceso de un UKF: resumen, p. 12731, y sección de arquitectura del estimador. Estas citas respaldan fusión y estimación, sin atribuirles un residual dinámico aditivo. |
| Las ecuaciones físicas pueden incorporarse a la función de entrenamiento. | `Wang2027Adaptive` | Sección 3.1: residuos de equilibrio longitudinal/lateral de fuerzas en el objetivo de entrenamiento de un modelo de Koopman. Estos residuos de ecuación tienen una función distinta del residual aditivo de predicción. |
| Chen identifica la limitada adaptación de correcciones entrenadas offline a condiciones nuevas como motivación de las actualizaciones online. | `Chen2026Hybrid` | Resumen e introducción. Se comprobó nuevamente el resumen del editor, ya que el PDF con el nombre original no estaba disponible durante esta revisión. [Publicación del editor](https://www.sciencedirect.com/science/article/pii/S0952197626021251). |

## Decisiones y síntesis de la tesis

La selección de un residual aditivo como objeto de estudio y su evaluación mediante precisión de predicción y efecto en el control son decisiones metodológicas propias. Se identifican como tales y no se atribuyen a un autor externo. El cierre sintetiza la dependencia de lo aprendido respecto a las condiciones representadas por los datos y conduce al paso 7; no presupone que toda variación invalide el residual.

## Consolidación de la bibliografía

- Se conservaron las 27 entradas existentes y sus claves, sin añadir trabajos nuevos: las fuentes disponibles respaldan las afirmaciones del paso 6.
- Se reincorporaron Cheng, Bertipaglia y Wang a las afirmaciones que corresponden a sus arquitecturas. El paso 6 utiliza seis trabajos distintos, contando `Chen2026Hybrid`, registrado bajo el paso 5.
- Bajo `% Paso 6` se agrupan los cinco trabajos de ese bloque citados en el texto. Los otros cuatro se conservan bajo `% Paso 6 -- Referencias adicionales para revisar`: Xiong, Li, Songli y WAKE. Su conservación no implica que respalden las afirmaciones actuales sobre residuales para control.
- Se uniformaron tipos y formato de campos, se normalizaron enlaces DOI y se retiraron campos de exportación y recuentos de citas de Scopus.
- La entrada de Salleh se corrigió como artículo de una serie de conferencias, conservando revista, volumen y número y añadiendo el identificador `012054`, comprobado en el artículo original del repositorio institucional. [Artículo de Salleh](https://eprints.utm.my/89085/1/ShamsuniSalleh2019_PerformanceofRalumacMicro.pdf).

La revisión comprueba correspondencia bibliográfica y de contenido; no reproduce los experimentos de los artículos.
