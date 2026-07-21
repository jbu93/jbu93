# Decision Record · El LLM entrega DATOS; el render lo hace nuestro código

> **🇪🇸 Versión en español abajo** — **🇬🇧 English version below**

---

## 🇪🇸 Español

**Fecha:** 2026-07-05 · **Sistema:** copiloto clínico (Flask + frontend en sandbox) · **Estado:** vigente

### Problema

Un generador de módulos de estudio interactivos deja que el modelo produzca contenido. Si el LLM escribiera el HTML/JS directamente, una inyección de prompt podría **ejecutar código en el navegador del profesional**: robo de sesión o XSS sobre datos clínicos protegidos.

### Decisión

El modelo produce **solo JSON de datos validado**. Las plantillas interactivas son nuestras. El resultado se monta en un **iframe sandbox** (origen opaco, sin cookies).

### Alternativas descartadas

- **El modelo genera HTML y lo sanitizamos** — sanitizar marcado generado es un juego del gato y el ratón que siempre pierde el gato.
- **Sin sandbox** — inaceptable con sesiones clínicas activas.

### Razón

Lo peor que puede hacer un modelo manipulado debe ser **escribir texto raro, nunca ejecutar código**. Seguridad por diseño, no por filtro.

### Costo aceptado

Cada tipo de módulo interactivo exige construir su propia plantilla a mano. Menos "magia" del modelo, más trabajo nuestro.

### Señales de revisión

Si aparece una plantilla nueva que interpole datos sin escapar, eso es una brecha: auditar toda interpolación nueva.

### Lección (reutilizable)

Trata la salida del modelo como **dato no confiable, jamás como código**. Si tu defensa es un sanitizador, ya elegiste el bando que pierde.

---

## 🇬🇧 English

# Decision Record · The LLM returns DATA; our code does the rendering

**Date:** 2026-07-05 · **System:** clinical copilot (Flask + sandboxed frontend) · **Status:** active

### Problem

An interactive study-module generator lets the model produce content. If the LLM wrote HTML/JS directly, a prompt injection could **execute code in the practitioner's browser**: session theft or XSS over protected clinical data.

### Decision

The model emits **only validated JSON data**. The interactive templates are ours. The result is mounted in a **sandboxed iframe** (opaque origin, no cookies).

### Alternatives rejected

- **Model generates HTML and we sanitize it** — sanitizing generated markup is a cat-and-mouse game the cat always loses.
- **No sandbox** — unacceptable with live clinical sessions.

### Why

The worst thing a manipulated model can do must be to **write strange text, never to execute code**. Security by design, not by filter.

### Cost accepted

Every new interactive module type needs its own hand-built template. Less model "magic", more of our work.

### Review signals

If a new template interpolates data without escaping, that's a breach: audit every new interpolation.

### Lesson (reusable)

Treat model output as **untrusted data, never as code**. If your defense is a sanitizer, you have already picked the losing side.
