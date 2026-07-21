# Decision Record · La deuda de conocimiento: las decisiones son la fuente de verdad

> **🇪🇸 Versión en español abajo** — **🇬🇧 English version below**

---

## 🇪🇸 Español

**Fecha:** 2026-07-09 · **Sistema:** disciplina de ingeniería (aplica a todo el monorepo) · **Estado:** vigente

### Problema

**Deuda de conocimiento**: la IA genera código más rápido de lo que el humano construye su modelo mental de ese código. Sin un registro del **porqué**, el autor se pierde en su propio sistema y no puede explicarlo sin tener el computador delante — justo lo que un senior pre-LLM sabía de memoria.

### Decisión

Un sistema de memoria evolutiva cuya **unidad es la DECISIÓN**, append-only, como una historia clínica:

- Los archivos de decisión son **la fuente de verdad**.
- La vista de estudio (visual, con quiz de *active recall*, imprimible) se **compila** desde ellos y **jamás se edita a mano**.
- El humano estudia con un ritual semanal; el agente **registra al cerrar cada misión**.

### Alternativas descartadas

- **Generar un documento por cada cambio** — los formatos divergen entre sí y envejecen: se vuelven la nueva deuda. Quedan como **vistas**, no como almacenamiento.
- **Un knowledge graph o base de datos** — potente pero sobredimensionado hoy; archivos planos + `grep` + `git` dan el 90% con el 1% del costo de mantenimiento.
- **Solo bitácoras por misión** — narran **qué** se hizo, no consolidan el **porqué**, y no son estudiables.

### Razón

El código cambia porque **alguien decidió algo**. Quien domina las decisiones puede reconstruir el sistema en su cabeza. Y la documentación que nadie mantiene es deuda: por eso las vistas se **recompilan** y la fuente es **una sola**.

### Costo aceptado

Disciplina permanente (una entrada por misión relevante) y un ritual humano de estudio. **Sin el ritual, esto es otra carpeta muerta** — y ese costo es innegociable.

### Señales de revisión

Si en dos meses el quiz no se ha usado, **el problema es el ritual, no la herramienta**: hay que reabrir el diseño.

### Lección (reutilizable)

En una base de código asistida por IA, el activo escaso **no es el código: es el porqué**. Haz que las decisiones sean append-only y de fuente única, y **compila** desde ahí cualquier otra vista.

---

## 🇬🇧 English

# Decision Record · Knowledge debt: decisions are the source of truth

**Date:** 2026-07-09 · **System:** engineering discipline (applies across the monorepo) · **Status:** active

### Problem

**Knowledge debt**: AI generates code faster than the human builds a mental model of that code. Without a record of the **why**, the author gets lost inside their own system and can't explain it away from a computer — exactly what a pre-LLM senior knew by heart.

### Decision

An evolving-memory system whose **unit is the DECISION**, append-only, like a medical chart:

- The decision files are **the source of truth**.
- The study view (visual, with an *active recall* quiz, printable) is **compiled** from them and **never hand-edited**.
- The human studies on a weekly ritual; the agent **records on closing each mission**.

### Alternatives rejected

- **Generate a document per change** — formats diverge from each other and age: they become the new debt. They remain **views**, not storage.
- **A knowledge graph or database** — powerful but oversized today; flat files + `grep` + `git` give 90% at 1% of the maintenance cost.
- **Mission logs only** — they narrate **what** was done, don't consolidate the **why**, and aren't studyable.

### Why

Code changes because **someone decided something**. Whoever masters the decisions can rebuild the system in their head. And documentation nobody maintains is debt — so the views **recompile** and the source is **a single one**.

### Cost accepted

Permanent discipline (one entry per relevant mission) and a human study ritual. **Without the ritual this is another dead folder** — and that cost is non-negotiable.

### Review signals

If the quiz hasn't been used in two months, **the problem is the ritual, not the tool**: reopen the design.

### Lesson (reusable)

In an AI-assisted codebase, the scarce asset **isn't the code: it's the why**. Make decisions append-only and single-source, and **compile** every other view from them.
