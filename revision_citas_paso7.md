# Revisión del paso 7

El paso 7 conecta la dependencia de los datos, presentada al cierre del paso 6, con la necesidad de evaluar la utilidad del residual durante la operación. Mantiene el alcance sobre carga y propiedades de los neumáticos, sin reducirlo a la fricción.

| Pasaje | Comprobación y ajuste |
| --- | --- |
| Dependencia de la corrección respecto al error de modelo durante la operación | Se añadieron `Kabzan2019LearningBased` y `Chen2026Hybrid`, cuyas formulaciones aprenden la discrepancia con el modelo nominal y evalúan o actualizan la corrección. |
| Ejemplo de cambio de carga | Se presenta como ejemplo conceptual de la tesis. Se explicita que el modelo nominal y el residual permanecen sin actualizar; el cambio de carga no se trata como prueba automática de invalidez. |
| Respuesta distinta ante entradas familiares cuando cambian los parámetros del neumático | Se añadió `Yeneneh2026AutoDyn`, que representa incertidumbre en los parámetros de rigidez lateral dentro de la dinámica vehicular. No se presenta como evidencia de un ensayo con un residual aprendido. |
| `Kalaria2024Adaptive` | Se verificaron título, autores, año y páginas en la [ficha de Carnegie Mellon](https://publications.ri.cmu.edu/adaptive-planning-and-control-with-time-varying-tire-models-for-autonomous-racing-using-extreme-learning-machine). La [versión de los autores](https://arxiv.org/html/2303.08235), sección V, evalúa cambios del modelo de neumáticos en un simulador numérico y en CARLA. El desgaste se representa mediante cambios simulados; no se atribuyen pruebas de desgaste en un vehículo físico. |
| `Brunke2022Safe` | Se verificaron los metadatos en la [página del editor](https://www.annualreviews.org/content/journals/10.1146/annurev-control-042920-020211). La [versión de los autores](https://roboralab.com/papers/dsl-annurev22.pdf), sección 5, página 25, menciona datos escasos y cambios de distribución como dificultades prácticas. Se utiliza esa formulación, sin presentar la revisión como demostración experimental sobre un residual automotivo. |
| Utilidad fuera de las condiciones evaluadas | Se añadió una cita explícita a `Chen2026Hybrid`, que identifica limitaciones de adaptación del aprendizaje offline ante nuevas condiciones. No se presupone que cualquier cambio físico invalide lo aprendido. |
| Cierre | Se conecta la evaluación runtime con el efecto del error sobre las decisiones del controlador, preparando los pasos 8 y 9. La identificación de la causa física no se introduce como requisito del método. |

Se añadieron los enlaces DOI a las dos entradas existentes y se normalizó el comentario `% Paso 7`. No se añadieron trabajos nuevos.
