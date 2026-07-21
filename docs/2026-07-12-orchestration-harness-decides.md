# Decision Record · Orquestación de modelos: decide el arnés, no el auto-reporte del modelo

> **🇪🇸 Versión en español abajo** — **🇬🇧 English version below**

---

## 🇪🇸 Español

**Fecha:** 2026-07-12 · **Sistema:** capa de gobernanza del monorepo (multi-proyecto) · **Estado:** vigente

### Problema

Trabajar con varios modelos de distinta capacidad plantea tres riesgos: **quemar el modelo más caro en trabajo mecánico**, **perder trabajo por alucinación** (el modelo reporta "listo" sobre algo que no corrió), y **atar el sistema a la memoria de una sesión** que se pierde al cambiar de modelo o de herramienta.

### Decisión

Un ciclo de tres capas, con el juicio **compilado en archivos del repo**, no en el chat:

| Capa | Qué hace |
|---|---|
| **Planificador** (el modelo más capaz disponible) | No ejecuta: **piensa** la misión y deja un contrato completo — pasos atómicos, cada uno con su edición exacta, su salida esperada y su **compuerta** |
| **Ejecutor** (modelos de menor costo, elegidos por perfil de tarea) | Recorre el plan, pasa compuertas y deja **migas verificables en tiempo real** |
| **Validador** (el planificador en modo lectura) | Corre el arnés, lee migas, hace spot-checks y sella el veredicto |

Dos piezas hacen que funcione:

- **El arnés ejecutable.** Cada misión trae un verificador que imprime PASS/FAIL por criterio y sale con código 0/1. **El juicio vive en código, no en el modelo** — el auto-reporte del ejecutor no es la prueba.
- **Diseñar para el ejecutor más débil.** Si la misión la puede correr el modelo más pequeño, es a prueba de balas para cualquiera. **La inteligencia no está en el ejecutor: está en el contrato.**

### Alternativas descartadas

- **Delegar todo al modelo más capaz** — funciona, pero desperdicia presupuesto en trabajo mecánico perfectamente especificable.
- **Confiar en el reporte del ejecutor** — es exactamente el punto donde entra la alucinación.

### Costo aceptado

El ciclo son **tres pasadas**. Por eso hay una regla anti-desperdicio explícita: una misión de menos de ~30 minutos **no entra al sistema**, la hace el planificador directo. El sistema paga en trabajo grande-mecánico o de riesgo alto que amerita validación independiente.

### Honestidad obligatoria

Hay tareas que **no son delegables** por más perfecta que sea la especificación — arquitectura, seguridad, deuda desconocida, rescates. El planificador **las retiene y lo declara**.

### Lección (reutilizable)

Si vas a orquestar modelos, **el criterio de aceptación tiene que ser ejecutable**. Un modelo diciendo "hecho" no es evidencia; un arnés saliendo con código 0 sí. Y escribe el contrato para el ejecutor más débil: te obliga a eliminar la ambigüedad que causa la mayoría de los fallos.

---

## 🇬🇧 English

# Decision Record · Model orchestration: the harness decides, not the model's self-report

**Date:** 2026-07-12 · **System:** monorepo governance layer (multi-project) · **Status:** active

### Problem

Working with several models of differing capability raises three risks: **burning the most expensive model on mechanical work**, **losing work to hallucination** (the model reports "done" for something that never ran), and **tying the system to a session's memory**, which disappears when you switch model or tool.

### Decision

A three-layer cycle, with judgment **compiled into repo files**, not into the chat:

| Layer | What it does |
|---|---|
| **Planner** (most capable model available) | Doesn't execute: it **thinks** the mission and leaves a complete contract — atomic steps, each with its exact edit, expected output and **gate** |
| **Executor** (lower-cost models, chosen by task profile) | Walks the plan, passes gates and leaves **verifiable breadcrumbs in real time** |
| **Validator** (the planner in read-only mode) | Runs the harness, reads breadcrumbs, spot-checks and seals the verdict |

Two pieces make it work:

- **The executable harness.** Every mission ships a verifier that prints PASS/FAIL per criterion and exits 0/1. **Judgment lives in code, not in the model** — the executor's self-report is not the proof.
- **Design for the weakest executor.** If the smallest model can run the mission, it's bulletproof for anyone. **The intelligence isn't in the executor: it's in the contract.**

### Alternatives rejected

- **Delegate everything to the most capable model** — it works, but wastes budget on mechanical work that can be fully specified.
- **Trust the executor's report** — that's precisely where hallucination enters.

### Cost accepted

The cycle is **three passes**. Hence an explicit anti-waste rule: a mission under ~30 minutes **doesn't enter the system** — the planner just does it. The system pays off on large-mechanical or high-risk work that warrants independent validation.

### Mandatory honesty

Some tasks are **not delegable** no matter how perfect the spec — architecture, security, unknown debt, rescues. The planner **retains them and says so**.

### Lesson (reusable)

If you're going to orchestrate models, **the acceptance criterion has to be executable**. A model saying "done" is not evidence; a harness exiting 0 is. And write the contract for the weakest executor — it forces you to remove the ambiguity that causes most failures.
