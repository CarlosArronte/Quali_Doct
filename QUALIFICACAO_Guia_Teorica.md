# Guía teórica para la Qualificação

## 1. Objetivo de este documento

Servir como guía para redactar el documento de qualificação y organizar la evidencia bibliográfica necesaria para justificar el problema doctoral.

Este documento **no debe contener detalles de código, datasets concretos ni decisiones de implementación** salvo cuando sean necesarios para explicar la metodología propuesta.

---

## 2. Problema científico provisional

Los modelos aprendidos utilizados dentro de arquitecturas de control vehicular pueden degradar su validez cuando las condiciones de operación difieren del dominio usado para su entrenamiento.

El problema doctoral no es simplemente detectar muestras OOD, sino estudiar:

\[
\boxed{
	ext{cómo caracterizar runtime validity}
+
	ext{cómo usarla dentro del control}
}
\]

La cadena causal que debe justificar la tesis es:

\[
	ext{operating-condition change}
ightarrow
	ext{learned-information validity change}
ightarrow
	ext{possible control degradation}
ightarrow
	ext{runtime validity estimation}
ightarrow
	ext{confidence-aware control reaction}.
\]

---

## 3. Pregunta de investigación provisional

> **¿Cómo evaluar en tiempo de ejecución la validez/confianza de información generada por modelos de IA de dinámica vehicular y utilizarla para modular su influencia en una arquitectura de control ante cambios de condiciones operativas?**

Preguntas secundarias candidatas:

1. ¿Qué tipos de cambios de dinámica vehicular producen pérdida significativa de validez del modelo aprendido?
2. ¿Qué información aportan uncertainty y OOD sobre esa pérdida de validez?
3. ¿Son uncertainty y OOD complementarios o redundantes?
4. ¿Qué señal representa mejor el error relevante para control?
5. ¿Cómo debe traducirse esa señal en una modificación del controlador?
6. ¿Qué mejora closed-loop produce la arquitectura frente a usar el learned model sin validity awareness?

---

## 4. Hipótesis provisional

> La combinación de uncertainty y OOD puede caracterizar de forma útil la validez runtime de información aprendida en dinámica vehicular, y utilizar esa caracterización dentro del controlador puede reducir la degradación closed-loop bajo cambios de régimen.

La qualificação debe dejar claro:
- qué parte es evidencia del estado del arte;
- qué parte es hipótesis;
- qué parte será validada durante el doctorado.

---

## 5. Estructura sugerida del documento de qualificação

### 5.1 Introducción
Explicar:
- por qué los learned models/information son atractivos en control vehicular;
- por qué la dinámica vehicular cambia con operating conditions;
- por qué esa variación puede afectar la validez de información aprendida;
- por qué el problema importa closed-loop.

Terminar con la pregunta de investigación.

### 5.2 Fundamentos de dinámica y control vehicular
Solo lo necesario para sustentar el problema:
- estados dinámicos relevantes;
- tire-road interaction;
- model mismatch;
- operating envelope;
- modelos control-oriented;
- MPC/CBF/control architecture seleccionada.

Evitar convertir este capítulo en un tratado general de vehículos autónomos.

### 5.3 AI-generated information in vehicle control
Organizar por **rol funcional**, no por algoritmo:
1. full learned dynamics model;
2. hybrid physics + learning;
3. residual/model-mismatch learning;
4. learned tire/force/parameter estimation;
5. uncertainty/confidence information.

Pregunta guía:
> ¿Qué información produce el modelo y cómo modifica el controlador?

### 5.4 Runtime validity
Separar conceptualmente:

#### Uncertainty
- epistemic;
- aleatoric;
- predictive;
- calibration.

#### OOD / distribution shift
- input-space shift;
- feature-space shift;
- dynamics shift;
- residual-based detection;
- temporal change.

#### Confidence / validity
Explicar que:

\[
	ext{uncertainty} \neq 	ext{OOD} \neq 	ext{validity}
\]

aunque puedan estar relacionados.

### 5.5 Estado del arte de validity-aware control
La revisión debe buscar explícitamente:
- learned dynamics + uncertainty + MPC;
- OOD detection for dynamics models;
- confidence-aware control;
- adaptive/robust MPC under learned model error;
- runtime monitoring of learned components;
- safety filters / fallback mechanisms;
- automotive/robotics/CPS equivalents cuando el mecanismo sea transferible.

El objetivo NO es demostrar “nadie lo hizo”, sino responder:

\[
\boxed{
	ext{qué existe}
ightarrow
	ext{qué resuelve}
ightarrow
	ext{qué limitaciones deja}
}
\]

---

## 6. Política de evidencia bibliográfica

### Evidencia fuerte
- reviews recientes;
- artículos primarios peer-reviewed;
- trabajos con closed-loop evaluation;
- estudios con hardware/vehicle/HIL cuando existan.

### Evidencia auxiliar
- conference papers;
- preprints;
- papers cross-domain;
- surveys más antiguos.

### Regla de redacción
No escribir:
> “No existe X”

salvo que una revisión suficientemente amplia lo sustente.

Preferir:
> “Existing approaches address X through A/B/C, but the evidence reviewed indicates limitations under Y/Z.”

---

## 7. Cómo tratar trabajos previos cercanos

Los trabajos que ya usan OOD + uncertainty no invalidan automáticamente la tesis.

Para cada paper cercano registrar:
- problema;
- dominio;
- learned information;
- uncertainty method;
- OOD method;
- control architecture;
- cómo la señal afecta control;
- operating shifts;
- closed-loop metrics;
- garantías;
- limitaciones;
- qué se reutiliza;
- qué queda diferente en la tesis.

El objetivo es delimitar contribución, no demostrar prioridad absoluta.

---

## 8. Tabla maestra recomendada

```text
ID
Referencia
Año
Dominio
Información aprendida
Modelo AI
Controlador
Uncertainty
OOD
Definición de validity/confidence
Shift estudiado
Cómo validity modifica control
Closed-loop property
Guarantee
Validation
Real-time
Limitación explícita
Qué aporta al problema doctoral
Threatens contribution?
DOI
```

---

## 9. Formulación del gap: regla de seguridad

No usar todavía:
> “There is no method that combines OOD and uncertainty for autonomous vehicle control.”

Formulación provisional más segura:

> Learned models are increasingly used to provide control-relevant information in vehicle dynamics applications. Their validity may degrade when operating conditions differ from those represented during training. Existing work provides uncertainty estimation, OOD detection, robust control, adaptation and runtime monitoring mechanisms, but the doctoral problem focuses on how to characterize the runtime validity of learned vehicle-dynamics information and translate that validity explicitly into control decisions under changing operating conditions.

La última parte deberá ajustarse después de completar la revisión.

---

## 10. Contribuciones candidatas

No congelar todavía. Candidatas:

### C1 — Characterization
Caracterizar relación entre:
\[
	ext{shift}
ightarrow
OOD
ightarrow
U
ightarrow
	ext{prediction/control-relevant error}.
\]

### C2 — Confidence / validity representation
Proponer una señal:
\[
C = g(OOD,U)
\]
o demostrar cuándo conviene mantener ambas separadas.

### C3 — Control integration
Definir mecanismo para:
\[
C
ightarrow
	ext{control authority / robustness / constraints / fallback}.
\]

### C4 — Closed-loop evaluation
Demostrar experimentalmente cómo validity awareness afecta:
- tracking;
- stability;
- constraint satisfaction;
- recovery;
- robustness;
- computation.

La tesis debería seleccionar 2–3 contribuciones principales, no prometer todas.

---

## 11. Fenómenos que deben probarse

La qualificação debe justificar por qué los experimentos futuros incluirán distintos tipos de cambio.

### Parametric shift
- masa;
- inertia;
- tire coefficients.

### Environment shift
- friction;
- road condition.

### Operating-envelope shift
- speed;
- lateral acceleration;
- high curvature;
- handling limits.

### Structural/data shift
- new maneuver;
- region poorly represented during training.

Cada shift debe tener una razón física y no solo estadística.

---

## 12. Qué debería demostrar la qualificação

Al terminar, el lector debería poder responder:
1. ¿Cuál es el problema físico/controlístico?
2. ¿Por qué learned information puede dejar de ser válida?
3. ¿Por qué OOD y uncertainty son relevantes?
4. ¿Qué soluciones previas existen?
5. ¿Qué limitación concreta se estudiará?
6. ¿Qué se propone investigar?
7. ¿Qué contribución se espera?
8. ¿Cómo se evaluará?
9. ¿Por qué es una contribución doctoral y no solo una aplicación?

---

## 13. Decisiones científicas por cerrar antes de congelar la tesis

- [ ] learned information principal;
- [ ] controller principal;
- [ ] definición operacional de OOD;
- [ ] tipo de uncertainty;
- [ ] definición de confidence/validity;
- [ ] reacción de control;
- [ ] shifts principales;
- [ ] contribuciones;
- [ ] baselines;
- [ ] garantías;
- [ ] validación real-time/experimental.

---

## 14. Próximos pasos teóricos

1. Recuperar los trabajos previos más cercanos a OOD + uncertainty + control.
2. Crear la tabla “qué existe / qué falta / qué tomar prestado”.
3. Delimitar el fenómeno vehicular concreto.
4. Fijar 2–3 contribuciones potenciales.
5. Redactar la pregunta doctoral definitiva.
6. Solo entonces construir la query bibliográfica final de qualificação.
7. Preparar la narrativa completa del documento.

---

## 15. Frase guía del proyecto

\[
\boxed{
	ext{No buscamos demostrar que OOD + uncertainty sea nuevo.}
}
\]

Buscamos demostrar que existe un problema de **runtime validity de información aprendida dentro del control vehicular**, que merece una solución y una evaluación propias.
