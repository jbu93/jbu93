# Decision Record · Anclaje a evidencia: citar una fuente real o decir "no encontré"

> **🇪🇸 Versión en español abajo** — **🇬🇧 English version below**

---

## 🇪🇸 Español

**Fecha:** 2026-07-05 · **Sistema:** copiloto clínico (Flask + LLM) · **Estado:** vigente

### Problema

Un LLM clínico que inventa un estudio o una norma puede costar una demanda o un paciente. La confianza del profesional es el activo número uno y se pierde una sola vez.

### Decisión

Toda afirmación verificable sale de una **búsqueda en vivo** — APIs de literatura revisada por pares para lo científico, y búsqueda restringida a dominios oficiales de gobierno para lo normativo — con migas de trazabilidad. Si la recuperación no devuelve nada, el sistema lo declara. Los identificadores de fuente (DOI/URL) se adjuntan al stream **por fuera de la prosa del modelo**, para que la narración no los pierda.

### Alternativas descartadas

- **Dejar que el modelo responda de memoria** — alucina referencias con total confianza.
- **Hardcodear una lista curada de enlaces** — se pudren (verificado: páginas oficiales devuelven 403/404 con el tiempo).

### Costo aceptado

A veces responde "sin resultados" donde otro producto inventaría algo convincente. Latencia extra por la búsqueda en vivo y dependencia de servicios externos.

### Señales de revisión

Si un proveedor cambia su API, el registro curado hace de red de seguridad. Vigilar la tasa de "0 resultados": es síntoma de una consulta mal traducida, no de evidencia inexistente.

### Lección (reutilizable)

**Anclar o abstenerse.** Un modelo que no puede citar, no debería afirmar. "No encontré" también es un hallazgo. Y adjunta los identificadores de fuente por fuera del texto del modelo, o la narración los dejará caer silenciosamente.

---

## 🇬🇧 English

# Decision Record · Grounding: cite a real source or say "I didn't find it"

**Date:** 2026-07-05 · **System:** clinical copilot (Flask + LLM) · **Status:** active

### Problem

A clinical LLM that invents a study or a regulation can cost a lawsuit or a patient. Practitioner trust is the number-one asset, and you only lose it once.

### Decision

Every verifiable claim comes from a **live retrieval** — peer-reviewed literature APIs for science, and a search restricted to official government domains for regulation — carrying traceability breadcrumbs. If retrieval returns nothing, the system says so. Source identifiers (DOI/URL) are attached to the stream **outside the model's prose**, so the narration can't drop them.

### Alternatives rejected

- **Let the model answer from memory** — it hallucinates references with total confidence.
- **Hardcode a curated list of links** — they rot (verified: official pages return 403/404 over time).

### Cost accepted

Sometimes it answers "no results" where another product would invent something convincing. Extra latency from live retrieval, and a dependency on external services.

### Review signals

If a provider changes its API, the curated registry is the safety net. Watch the "0 results" rate — it's a symptom of a badly translated query, not of missing evidence.

### Lesson (reusable)

**Ground or abstain.** A model that cannot cite should not assert. "I didn't find it" is also a finding. And attach source identifiers outside the model's text, or the narration will quietly drop them.
