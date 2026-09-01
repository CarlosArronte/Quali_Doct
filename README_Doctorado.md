# Doctorado — Guía científica y documental

**Estado:** línea de trabajo provisional, agosto de 2026  
**Propósito:** mantener alineadas las decisiones científicas, la revisión bibliográfica, el documento de qualificação y la futura implementación experimental.

---

## 1. Estructura recomendada de documentación

Para no mezclar argumentación científica con decisiones de implementación, el proyecto debe mantener **dos documentos principales**:

1. **`QUALIFICACAO_Guia_Teorica.md`**  
   Problema científico, estado del arte, hipótesis, preguntas, contribuciones, evidencia bibliográfica y estructura del documento de qualificação.

2. **`IMPLEMENTACAO_Guia_Practica.md`**  
   Arquitectura experimental, datasets, modelos, OOD, uncertainty, integración con MPC/CBF, métricas, experimentos y reproducibilidad.

Este `README` funciona como **mapa maestro** y registro de decisiones.  
La guía práctica debe desarrollarse en el chat de **Implementación del proyecto**.

---

## 2. Dominio científico

El trabajo se mantiene dentro de:

$$
\text{dinámica vehicular}
\rightarrow
\text{información generada mediante IA}
\rightarrow
\text{arquitectura de control}
\rightarrow
\text{comportamiento closed-loop}
$$

Quedan fuera del núcleo, salvo conexión directa con el controlador dinámico:

- percepción;
- detección de objetos;
- planificación de ruta;
- predicción de comportamiento de otros agentes;
- assurance del stack completo de autonomía.

---

## 3. Fenómeno científico actualmente elegido

El fenómeno de interés es la **pérdida de validez en runtime de información generada por modelos de IA cuando cambian las condiciones dinámicas del vehículo**.

Ejemplo conceptual:

$$
f_\theta \text{ entrenado en } \mathcal D_{\text{train}}
$$

opera después bajo:

$$
\mathcal D_{\text{runtime}} \neq \mathcal D_{\text{train}}
$$

por cambios de:

- fricción neumático-carretera;
- propiedades del neumático;
- masa/carga;
- velocidad;
- maniobra;
- rango dinámico;
- condiciones cercanas al handling limit;
- otros cambios de régimen.

El problema de control aparece cuando:

$$
\text{el controlador sigue usando información aprendida}
$$

aunque:

$$
\text{su validez haya cambiado}.
$$

---

## 4. Herramientas candidatas

Las herramientas principales que se desean estudiar son:

$$
\boxed{\text{OOD detection} + \text{uncertainty estimation}}
$$

No se consideran el gap por sí mismas.

Su papel es potencialmente producir una señal de:

$$
\boxed{\text{validez / confianza runtime}}
$$

que pueda modificar la influencia de la información aprendida sobre el controlador.

Arquitectura conceptual:

$$
x_k
\rightarrow
f_\theta
\rightarrow
\{\hat y_k,\;U_k,\;OOD_k\}
\rightarrow
C_k
\rightarrow
\text{controlador}
\rightarrow
u_k
\rightarrow
\text{vehículo}
$$

donde:

- \(\hat y_k\): información aprendida usada por control;
- \(U_k\): uncertainty;
- \(OOD_k\): indicador de cambio respecto al dominio de entrenamiento;
- \(C_k\): confidence/validity signal;
- \(u_k\): acción de control.

---

## 5. Pregunta de investigación provisional

> **¿Cómo evaluar en tiempo de ejecución la validez/confianza de información generada por modelos de IA de dinámica vehicular y utilizarla para modular su influencia en una arquitectura de control ante cambios de condiciones operativas?**

Esta formulación es **provisional**. Antes de congelarla deben cerrarse las decisiones D1–D10.

---

## 6. Hipótesis de trabajo provisional

> La combinación de señales de uncertainty y OOD puede proporcionar información complementaria sobre la validez runtime de un modelo aprendido de dinámica vehicular, y el uso explícito de esta información dentro del lazo de control puede reducir la degradación closed-loop cuando las condiciones operativas se alejan del dominio de entrenamiento.

Esto **todavía no debe escribirse como resultado demostrado**.

---

## 7. Qué NO debe afirmarse

Evitar afirmaciones como:

- “nadie ha combinado OOD y uncertainty”;
- “no existe ningún método de runtime validity”;
- “no existen soluciones confidence-aware”;
- “OOD garantiza que el modelo es incorrecto”;
- “uncertainty equivale a model validity”;
- “un modelo con menor RMSE necesariamente produce mejor control”;
- “el trabajo previo cercano invalida automáticamente la tesis”.

La contribución doctoral no necesita ser una “invención virgen”; debe ser una **aportación original, justificada y suficientemente profunda**.

---

## 8. Decisiones científicas pendientes

### D1 — ¿Qué información aprendida será supervisada?

Elegir una arquitectura principal:

- learned full dynamics model;
- physics + learned residual;
- learned tire/force model;
- learned state/parameter estimator;
- otra información dinámica directamente relevante al control.

**Criterio:** la información debe afectar explícitamente el comportamiento closed-loop.

### D2 — ¿Qué controlador será el receptor?

Candidatos:

- MPC / NMPC;
- robust/stochastic MPC;
- CBF/safety filter;
- arquitectura híbrida.

Debe elegirse una arquitectura donde pueda definirse claramente qué cambia cuando disminuye la confianza.

### D3 — ¿Qué significa OOD en dinámica vehicular?

Debe definirse operacionalmente.

Posibles niveles:

- input OOD;
- feature/latent OOD;
- dynamics OOD;
- residual-based OOD;
- distribution shift;
- régimen físico no representado.

La tesis no debe tratar OOD como una etiqueta genérica.

### D4 — ¿Qué uncertainty se utilizará?

Distinguir:

- **aleatoric uncertainty**;
- **epistemic uncertainty**;
- total predictive uncertainty;
- uncertainty calibrada/no calibrada.

Preguntas:
- ¿cuál correlaciona con error del modelo?
- ¿cuál aporta información diferente de OOD?
- ¿cuál es utilizable en tiempo real?

### D5 — ¿Cómo se construye la señal de confianza?

Opciones conceptuales:

$$
C = g(U,\;OOD)
$$

o mecanismos separados.

Debe estudiarse si OOD y uncertainty aportan información complementaria o si existe alta redundancia.

La señal debe relacionarse con **error relevante para control**, no solo con métricas de clasificación OOD.

### D6 — ¿Cómo reacciona el controlador?

Opciones a estudiar:

- disminuir autoridad del learned model;
- aumentar robustificación;
- modificar constraints;
- cambiar pesos;
- switching;
- fallback a modelo físico;
- activar safety layer;
- adaptar horizonte;
- combinación gradual.

La reacción debe ser explícita y medible.

### D7 — ¿Qué condiciones no nominales se estudiarán?

Construir una taxonomía física de shifts.

Ejemplos:

- \(\mu\) desconocida / cambio de fricción;
- neumático diferente;
- masa/carga;
- cambio de velocidad/rango de operación;
- maniobras no vistas;
- operación próxima a saturación;
- ruido/fallo de sensores, solo si se justifica como cambio relevante para la información aprendida.

No mezclar todos los shifts en un único “OOD”.

### D8 — ¿Dónde estará la contribución original?

Posibles niveles:

1. caracterización de OOD/uncertainty en learned vehicle dynamics;
2. nueva representación de confidence/validity;
3. método de fusión OOD + uncertainty;
4. mecanismo confidence-aware de integración con control;
5. análisis closed-loop;
6. validación sistemática de múltiples shifts;
7. implementación real-time.

La tesis no necesita inventar todos estos componentes. Debe identificar **2–3 contribuciones fuertes y coherentes**.

### D9 — ¿Contra qué se compara?

Baselines mínimos conceptuales:

- controlador con modelo aprendido sin validity monitoring;
- uncertainty-only;
- OOD-only;
- OOD + uncertainty;
- fallback/modelo físico si aplica;
- controlador nominal de referencia.

La comparación debe medir tanto calidad del detector/modelo como impacto closed-loop.

### D10 — ¿Qué nivel de garantía se pretende?

Decidir si la tesis buscará:

- evidencia empírica;
- bounds probabilísticos;
- robustez;
- recursive feasibility;
- constraint satisfaction;
- estabilidad formal;
- safety via CBF;
- ninguna garantía formal, pero evaluación experimental rigurosa.

No prometer estabilidad/seguridad formal hasta que la arquitectura elegida realmente lo permita.

---

## 9. Métricas que deberán convivir

### Modelo / predictor
- RMSE / MAE;
- NLL;
- calibration;
- multi-step error;
- residual error.

### OOD / uncertainty
- AUROC;
- AUPR;
- FPR@TPR;
- calibration error;
- correlation con prediction error;
- detection delay si hay cambio temporal.

### Closed-loop
- tracking error;
- yaw/sideslip error;
- constraint violations;
- control effort;
- stability indicators;
- feasibility;
- recovery after shift;
- computation time / sampling deadline.

La métrica central no debe ser únicamente AUROC.

---

## 10. Regla científica principal

La tesis debe cerrar el círculo:

$$
\boxed{
\text{runtime validity}
\rightarrow
\text{control decision}
\rightarrow
\text{vehicle closed-loop behavior}
}
$$

Si el trabajo termina en NN → uncertainty → OOD AUROC, sin impacto explícito en control, la contribución queda demasiado cerca de ML aplicado.

---

## 11. Papel de trabajos previos cercanos

Trabajos previos que combinen OOD, uncertainty o runtime monitoring deben tratarse como:

- **estado del arte**;
- fuentes de mecanismos reutilizables;
- baselines;
- referencias para delimitar la contribución.

No deben interpretarse automáticamente como “gap killers”.

La pregunta correcta es:

> ¿Qué resuelven, bajo qué supuestos y qué parte específica del problema vehicular/closed-loop queda para nuestra contribución?

---

## 12. Criterio de avance

Antes de comenzar una implementación doctoral grande deben estar cerrados:

- [ ] D1 — información aprendida;
- [ ] D2 — controlador;
- [ ] D3 — definición de OOD;
- [ ] D4 — uncertainty;
- [ ] D5 — confidence;
- [ ] D6 — reacción de control;
- [ ] D7 — shifts;
- [ ] D8 — contribución;
- [ ] D9 — baselines;
- [ ] D10 — garantías.

---

## 13. Documentos asociados

- **Guía teórica / qualificação:** `QUALIFICACAO_Guia_Teorica.md`
- **Guía práctica / implementación:** `IMPLEMENTACAO_Guia_Practica.md` — desarrollar en el chat de implementación.

---

## 14. Estado actual de la línea

**Decisión actual:** dejar de buscar un “gap virgen” y trabajar sobre el problema de **runtime validity/confidence de información aprendida aplicada a control de dinámica vehicular**, utilizando OOD y uncertainty como mecanismos candidatos.

**Estado:** dirección científica escogida de forma provisional; faltan delimitar contribución, arquitectura de control y protocolo experimental antes de congelar la pregunta doctoral definitiva.
