# Plan de trabajo experimental del doctorado

## 1. Objetivo del plan

Este documento organiza las actividades prácticas necesarias para desarrollar y validar la propuesta doctoral:

> **Estimación de validez en tiempo de ejecución para la integración de modelos híbridos aprendidos en control de dinámica vehicular.**

La estrategia experimental se basa inicialmente en **MATLAB/Simulink + CarSim**, con posibilidad de migrar o ampliar posteriormente a otra plataforma experimental si resulta necesario.

La secuencia general de trabajo sigue la lógica:

**modelo físico → residual aprendido → uncertainty/OOD → shifts → validity → integración con MPC/NMPC → comparación → extensiones**

---

## 2. Priorización del alcance

Las actividades se dividen en tres niveles.

| Nivel | Actividades | Prioridad |
|---|---|---|
| **Core** | Modelo físico + residual aprendido + uncertainty/OOD + validity + MPC/NMPC | Obligatorio |
| **Validación** | Shifts + baselines + ablation study + análisis estadístico | Obligatorio |
| **Extensiones** | CBF, DAgger/retraining, sensor failure, input OOD | Opcional |

### Regla de alcance

Las extensiones no deben comprometer la ejecución del núcleo de la tesis.

La prioridad será obtener evidencia sólida sobre la cadena:

**shift → pérdida de validez → estimación de validity → adaptación del control → desempeño closed-loop**

---

# 3. Paquetes de trabajo

## WP0 — Infraestructura experimental

### Objetivo

Establecer un banco de simulación reproducible basado en **MATLAB/Simulink + CarSim**.

### Actividades

- Configurar la comunicación CarSim–MATLAB/Simulink.
- Seleccionar el vehículo de referencia.
- Definir las maniobras iniciales.
- Definir las señales a registrar.
- Definir frecuencia de muestreo.
- Establecer condiciones nominales de operación.
- Diseñar una estructura reproducible para:
  - configuraciones;
  - simulaciones;
  - seeds;
  - logs;
  - resultados;
  - figuras.
- Automatizar, en lo posible, la ejecución y almacenamiento de experimentos.

### Entregable

Banco experimental reproducible.

### Hito H0

> ¿MATLAB/CarSim proporciona la flexibilidad necesaria para ejecutar los experimentos previstos?

### Criterio de DONE

- Una maniobra puede ejecutarse de forma automática.
- Los parámetros relevantes pueden modificarse de forma controlada.
- Una misma configuración produce resultados reproducibles.
- Todos los datos necesarios pueden exportarse.

### Duración estimada

**1 semana**

---

## WP1 — Modelo físico y MPC/NMPC baseline

### Objetivo

Implementar el modelo físico **control-oriented** y establecer el controlador de referencia **B0 — Physics-only**.

### Arquitectura inicial

```text
Reference
    ↓
MPC/NMPC
    ↓
CarSim
    ↓
States / outputs
```

### Actividades

- Seleccionar/formular el modelo físico control-oriented.
- Identificar parámetros nominales.
- Implementar el modelo en MATLAB/Simulink.
- Implementar el MPC o NMPC.
- Definir restricciones.
- Definir función de coste.
- Definir horizonte inicial.
- Ejecutar maniobras nominales.
- Registrar desempeño closed-loop.

### Entregable

Baseline físico funcional y reproducible.

### Hito H1

> ¿El controlador physics-only funciona correctamente bajo condiciones nominales?

### Criterio de DONE

- Seguimiento aceptable de referencia.
- Restricciones satisfechas en condiciones nominales.
- Simulaciones repetibles.
- Métricas baseline disponibles.

### Duración estimada

**2–3 semanas**

---

## WP2 — Modelo híbrido: physics + learned residual

### Objetivo

Desarrollar un modelo híbrido:

\[
x_{k+1}=f_{physics}(x_k,u_k)+r_\theta(x_k,u_k)
\]

### Actividades

- Generar dataset nominal desde CarSim.
- Definir dominio ID de entrenamiento.
- Separar:
  - train;
  - validation;
  - test ID.
- Entrenar un residual aprendido.
- Utilizar inicialmente una arquitectura sencilla, por ejemplo:
  - MLP.
- Comparar:
  - modelo físico;
  - modelo híbrido.
- Evaluar error multi-step si resulta relevante para MPC.

### Preguntas clave

1. ¿El residual mejora la predicción respecto al modelo físico?
2. ¿La mejora es suficientemente significativa como para justificar su uso en control?
3. ¿Existen condiciones fuera del dominio de entrenamiento donde el residual pierde validez?

### Entregable

Modelo híbrido validado en ID.

### Hito H2

> ¿El residual aprendido aporta mejora real respecto al modelo físico?

### Criterio de DONE

- Mejora cuantificada en ID.
- Errores caracterizados.
- Modelo exportable/usable dentro del controlador.

### Duración estimada

**2 semanas**

---

## WP3 — Uncertainty, calibration y OOD

### Objetivo

Dotar al residual aprendido de señales que permitan caracterizar su validez en runtime.

### Componentes iniciales

- **Uncertainty aleatoric**
  - modelo heteroscedástico.
- **Uncertainty epistemic**
  - ensemble pequeño.
- **Calibration**
  - evaluación y ajuste de la incertidumbre.
- **OOD score**
  - método de bajo coste computacional.

### Actividades

- Implementar estimación aleatoric.
- Implementar ensemble para epistemic uncertainty.
- Evaluar calibración.
- Implementar score OOD.
- Caracterizar las señales bajo condiciones ID.
- Medir coste computacional.

### Entregable

Sistema de estimación de uncertainty/OOD funcionando.

### Hito H3

> ¿Las señales de uncertainty y OOD presentan un comportamiento interpretable y útil?

### Criterio de DONE

- \(U_{ale}\) disponible.
- \(U_{epi}\) disponible.
- Calibration cuantificada.
- OOD score disponible.
- Coste computacional registrado.

### Duración estimada

**2–3 semanas**

---

# 4. Campaña experimental principal

## WP4 — Diseño y caracterización de shifts

### Objetivo

Evaluar cómo diferentes condiciones no representadas afectan:

- error predictivo;
- uncertainty;
- calibration;
- OOD;
- error relevante para control.

### Shifts prioritarios

#### S1 — Cambio desconocido de fricción

Variación de \(\mu\) respecto al dominio de entrenamiento.

**Prioridad: alta**

#### S2 — Extensión del rango de velocidad

Evaluar:

\[
V_x > V_{x,max,train}
\]

**Prioridad: alta**

#### S3 — Degradación/fallo sensorial

Ejemplos:

- ruido adicional;
- bias;
- dropout;
- pérdida parcial de señal.

**Prioridad: opcional**

#### S4 — Input OOD

Excitaciones/inputs fuera de la distribución observada durante entrenamiento.

**Prioridad: opcional**

### Cadena experimental

```text
Shift severity
      ↓
Prediction error
      ↓
U_epi
U_ale
Calibration
OOD score
      ↓
Control-relevant error
```

### Entregable

Mapa experimental:

**shift → uncertainty/OOD → error → relevancia para control**

### Hito H4

> ¿Los shifts seleccionados generan una degradación medible y físicamente interpretable?

### Criterio de DONE

- Al menos dos shifts principales caracterizados.
- Severidad parametrizada.
- Curvas de degradación disponibles.
- Correlaciones con uncertainty/OOD cuantificadas.

### Duración estimada

**3–4 semanas**

---

## WP5 — Construcción de la señal de validity

### Objetivo

Construir y justificar experimentalmente:

\[
C_k=g(U_{epi},U_{ale},Cal,S_{OOD})
\]

### Principio

La función \(g(\cdot)\) **no debe fijarse a priori**.

Debe construirse después de observar:

- redundancia;
- complementariedad;
- sensibilidad;
- capacidad predictiva;
- relación con error relevante para control.

### Ablation study inicial

Evaluar:

```text
U_epi
U_ale
OOD
U_epi + U_ale
U_epi + OOD
U_ale + OOD
U_epi + U_ale + OOD
```

Incluir calibration cuando corresponda.

### Objetivo de la señal

No basta correlacionarla con RMSE.

La señal debe reflejar un **error útil para la toma de decisiones del controlador**.

### Entregable

Definición experimentalmente justificada de \(C_k\).

### Hito H5

> ¿Existe suficiente información complementaria entre uncertainty, calibration y OOD para justificar una señal de validity combinada?

### Posibles resultados

#### Resultado A

Los componentes son complementarios.

→ Mantener \(C_k\) combinada.

#### Resultado B

Algunos componentes son redundantes.

→ Simplificar \(C_k\).

#### Resultado C

OOD o uncertainty individual domina.

→ Revisar la arquitectura y reformular la contribución.

### Criterio de DONE

- Relación con error cuantificada.
- Ablations completas.
- Función \(g(\cdot)\) definida.
- Umbrales o rango de validity establecido.

### Duración estimada

**2–3 semanas**

---

# 5. Integración con control

## WP6 — Validity-aware MPC/NMPC

### Objetivo

Utilizar \(C_k\) para adaptar el controlador.

### Mecanismo inicial

Adaptación del horizonte:

\[
C_k \rightarrow N_k
\]

Ejemplo inicial:

```text
High validity
    ↓
N = N_max

Medium validity
    ↓
N = N_medium

Low validity
    ↓
N = N_min
```

Posteriormente podrá evaluarse una función continua si los resultados lo justifican.

### Actividades

- Diseñar mapping \(C_k ightarrow N_k\).
- Evaluar sensibilidad del desempeño al horizonte.
- Comparar:
  - horizonte fijo;
  - horizonte adaptable.
- Evaluar comportamiento bajo shifts.

### Entregable

Controlador MPC/NMPC validity-aware.

### Hito H6

> ¿La adaptación mediante validity reduce la degradación closed-loop?

### Regla GO / NO-GO

Si la adaptación del horizonte no mejora el control después de una evaluación razonable:

**NO invertir meses tratando de forzar el resultado.**

Se revisará el mecanismo mediante el cual \(C_k\) afecta al MPC/NMPC.

### Alternativas posibles

- modificar pesos de coste;
- modificar constraints;
- modificar confianza en el modelo aprendido;
- blending physics/learned;
- modificar horizonte;
- combinación de estrategias.

### Criterio de DONE

- Adaptación implementada.
- Comparación contra horizonte fijo.
- Resultados closed-loop disponibles.
- Decisión GO/NO-GO documentada.

### Duración estimada

**3–4 semanas**

---

# 6. Validación definitiva

## WP7 — Baselines, ablations y experimento principal

### Objetivo

Demostrar qué aporta cada componente de la arquitectura.

### Baselines

| Caso | Physics | Residual | Uncertainty | OOD | Validity adaptation |
|---|---:|---:|---:|---:|---:|
| **B0 — Physics-only** | ✓ | | | | |
| **B1 — Learned/no-awareness** | ✓ | ✓ | | | |
| **B2 — Validity/uncertainty-only** | ✓ | ✓ | ✓ | | ✓ |
| **B3 — OOD-only** | ✓ | ✓ | | ✓ | ✓ |
| **P — Proposed** | ✓ | ✓ | ✓ | ✓ | ✓ |

### Condiciones experimentales mínimas

- ID.
- Friction shift:
  - leve;
  - medio;
  - severo.
- Velocity shift:
  - leve;
  - medio;
  - severo.
- Combinaciones seleccionadas si son relevantes.

### Métricas

#### Modelo

- MAE.
- RMSE.
- error multi-step.
- error relevante para control.

#### Uncertainty / calibration / OOD

- calibration error.
- coverage.
- correlation uncertainty-error.
- AUROC/AUPR si aplica.
- detección anticipada de degradación.

#### Closed-loop

- tracking error.
- constraint violations.
- coste \(J\).
- estabilidad empírica.
- robustez empírica.
- coste computacional.

### Criterio principal

Evaluar:

\[
\Delta J_{prop} < \Delta J_{baseline}
\]

bajo condiciones de shift relevantes.

### Entregable

Evidencia experimental central de la tesis.

### Hito H7

> ¿La arquitectura propuesta reduce de forma consistente la degradación closed-loop frente a los baselines?

### Criterio de DONE

- Baselines completos.
- Ablation study completo.
- Repeticiones estadísticas.
- Resultados reproducibles.
- Figuras y tablas finales.
- Conclusión clara respecto a la hipótesis.

### Duración estimada

**3–4 semanas**

---

# 7. Extensiones

## WP8 — Extensiones opcionales

Solo se ejecutarán después de completar satisfactoriamente WP7.

### Opción A — CBF

Utilizar \(C_k\) para modificar/agudizar la acción de una Control Barrier Function.

### Opción B — DAgger / retraining

Usar alta incertidumbre epistemic / OOD como criterio de adquisición de nuevas muestras.

### Opción C — Sensor degradation

Extender la taxonomía experimental de shifts.

### Opción D — Input OOD

Incluir excitaciones no observadas durante entrenamiento.

### Regla

No intentar desarrollar todas las extensiones.

Seleccionar aquella que:

1. fortalezca más la contribución principal;
2. responda a resultados obtenidos durante WP4–WP7;
3. sea viable dentro del cronograma restante.

---

# 8. Cronograma estimado

| Semanas | Paquete | Actividad principal |
|---:|---|---|
| 1 | WP0 | Infraestructura MATLAB/CarSim |
| 2–4 | WP1 | Physics model + MPC/NMPC |
| 5–6 | WP2 | Learned residual |
| 7–9 | WP3 | Uncertainty + calibration + OOD |
| 10–13 | WP4 | Shift campaign |
| 14–16 | WP5 | Validity estimation |
| 17–20 | WP6 | Validity-aware MPC/NMPC |
| 21–24 | WP7 | Baselines + ablations + validación |
| 25+ | WP8 | Extensión seleccionada |

### Horizonte esperado

Aproximadamente **6 meses** para disponer de la evidencia experimental central, sin contar extensiones.

---

# 9. Hitos de decisión

| Hito | Pregunta de decisión |
|---|---|
| **H0** | ¿MATLAB/CarSim es suficiente para el experimento? |
| **H1** | ¿El baseline physics-only funciona adecuadamente? |
| **H2** | ¿El residual aprendido aporta una mejora real? |
| **H3** | ¿Uncertainty/OOD se comportan de forma útil? |
| **H4** | ¿Los shifts generan degradación medible? |
| **H5** | ¿Existe información suficiente para justificar \(C_k\)? |
| **H6** | ¿Usar \(C_k\) mejora el MPC/NMPC? |
| **H7** | ¿La propuesta supera los baselines? |

---

# 10. Filosofía experimental

## 10.1. Resultado negativo ≠ fracaso

Cada WP debe terminar en una decisión científica.

Ejemplos:

- uncertainty y OOD resultan redundantes;
- el residual no mejora suficientemente el modelo físico;
- reducir el horizonte no mejora closed-loop;
- cierto shift no genera una degradación significativa.

Estos resultados deben utilizarse para reformular la arquitectura, no ocultarse.

---

## 10.2. Una variable nueva debe justificar su existencia

Cada componente adicional debe demostrar que aporta información o desempeño útil.

Evitar arquitecturas innecesariamente complejas.

---

## 10.3. Priorizar relevancia para control

El principal objetivo no es maximizar accuracy predictiva.

La cuestión central es:

> ¿La información generada permite al controlador tomar mejores decisiones cuando el modelo aprendido pierde validez?

---

## 10.4. Reproducibilidad desde el inicio

Cada experimento debe registrar:

- configuración;
- seed;
- dataset;
- modelo;
- hiperparámetros;
- versión de código;
- parámetros de CarSim;
- resultados;
- métricas;
- fecha.

---

# 11. Entregables mínimos de cada WP

Cada paquete de trabajo debe generar al menos:

1. **Código/configuración reproducible.**
2. **Dataset o logs experimentales.**
3. **Tabla de métricas.**
4. **Al menos una figura interpretable.**
5. **Conclusión del WP.**
6. **Decisión del hito correspondiente.**

---

# 12. Figuras finales esperadas de la tesis

## F1 — Arquitectura general

```text
Physics model
      +
Learned residual
      ↓
Prediction
      ↓
Uncertainty / Calibration / OOD
      ↓
Validity C_k
      ↓
Validity-aware MPC/NMPC
      ↓
Vehicle
```

## F2 — Shift vs prediction error

Mostrar degradación del modelo bajo cambios de régimen.

## F3 — Shift vs uncertainty/OOD

Mostrar sensibilidad de cada señal.

## F4 — Validity vs control-relevant error

Validar \(C_k\).

## F5 — Closed-loop performance vs shift severity

Comparar B0, B1, B2, B3 y Proposed.

## F6 — Ablation study

Mostrar qué componentes de \(C_k\) aportan valor.

---

# 13. Riesgos técnicos principales

## R1 — Redundancia uncertainty/OOD

### Mitigación

Ablation study y análisis de complementariedad.

---

## R2 — Uncertainty mal calibrada

### Mitigación

Calibration explícita y evaluación de coverage.

---

## R3 — Validity no correlaciona con error relevante para control

### Mitigación

Redefinir \(C_k\) utilizando métricas control-oriented.

---

## R4 — Adaptar el horizonte no mejora closed-loop

### Mitigación

Revisar el mecanismo de integración con MPC/NMPC.

---

## R5 — Complejidad computacional elevada

### Mitigación

- ensemble pequeño;
- OOD score cheap;
- simplificación de \(C_k\);
- profiling desde WP3.

---

## R6 — Scope creep

### Mitigación

Mantener CBF, DAgger, sensor degradation e input OOD como extensiones.

---

# 14. Definición de éxito del experimento central

El experimento principal será considerado exitoso si se demuestra que:

1. El residual aprendido mejora el modelo físico en ID.
2. Existen shifts físicamente relevantes que degradan su validez.
3. Esa degradación puede ser caracterizada mediante uncertainty/calibration/OOD.
4. Puede construirse una señal runtime \(C_k\) relacionada con error relevante para control.
5. El controlador puede utilizar \(C_k\) para modificar su comportamiento.
6. La arquitectura propuesta reduce la degradación closed-loop respecto a baselines relevantes.

---

# 15. Próxima actividad

La siguiente actividad práctica será:

## **WP0 — Definir formalmente el banco experimental MATLAB/CarSim**

Antes de implementar, debe fijarse:

- modelo de vehículo;
- maniobra inicial;
- estados;
- inputs;
- outputs;
- sampling time;
- parámetros nominales;
- rango ID;
- variables que se modificarán para generar shifts;
- estructura de datos;
- métricas mínimas.

---

## Fuente de referencia

Plan elaborado a partir del documento de qualificação, especialmente de:

- Objetivos específicos OE1–OE8.
- Estrategia experimental E1–E8.
- Escenarios de shift.
- Baselines B0–B3 y Proposed.
- Métricas.
- Riesgos y limitaciones.
