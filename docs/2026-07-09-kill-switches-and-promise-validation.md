# Decision Record · Kill-switch en toda función de riesgo + loop promesa-contra-producción

> **🇪🇸 Versión en español abajo** — **🇬🇧 English version below**

---

## 🇪🇸 Español

**Fecha:** 2026-07-09 · **Sistema:** copiloto clínico (producción sobre PaaS) · **Estado:** vigente

### Problema

Dos dolores gemelos:

- **(a)** Una función con costo o riesgo **no debería necesitar un redespliegue para apagarse.**
- **(b)** Lo que el producto **promete** (páginas de ayuda, landing, documentación) puede **divergir silenciosamente** de lo que de verdad **funciona** en producción.

### Decisión

- **(a)** Toda función de riesgo o costo lleva un **kill-switch por variable de entorno**, con default seguro.
- **(b)** Un **validador automatizado** corre decenas de chequeos **contra el despliegue real** y clasifica cada promesa como **CUMPLE / PROTEGIDA** (auth rechazando correctamente) **/ APAGADA** (kill-switch deliberado) **/ ROTA**. Solo el catálogo canónico entra al loop.

### Alternativas descartadas

- **Servicio externo de feature flags** — costo y dependencia innecesarios a esta escala.
- **Confiar en los tests locales como prueba de producción** — los tests no ven la plataforma, ni una variable faltante, ni un deploy fallido.

### Razón

Apagar debe ser una decisión **reversible en segundos, no un deploy**. Y la promesa de valor se audita **contra la realidad, no contra la intención**.

### Costo aceptado

Cada switch es una rama más que testear.

### Señales de revisión

Un switch olvidado en OFF **parece un bug** — por eso el validador lo reporta como APAGADA con su variable, y no como ROTA.

### Lección (reutilizable)

**Una suite local en verde no es evidencia sobre producción.** Valida la promesa contra el despliegue en vivo, y haz que **"apagado a propósito" sea un estado distinto de "roto"**.

---

## 🇬🇧 English

# Decision Record · Kill-switch on every risky feature + a promise-vs-production loop

**Date:** 2026-07-09 · **System:** clinical copilot (production on a PaaS) · **Status:** active

### Problem

Two twin pains:

- **(a)** A feature with cost or risk **shouldn't require a redeploy to turn off.**
- **(b)** What the product **promises** (help pages, landing, docs) can **silently drift** from what actually **works** in production.

### Decision

- **(a)** Every risky or costly feature carries an **environment-variable kill-switch**, with a safe default.
- **(b)** An **automated validator** runs dozens of checks **against the real deployment** and classifies each promise as **MEETS / PROTECTED** (auth correctly refusing) **/ OFF** (deliberate kill-switch) **/ BROKEN**. Only the canonical catalogue enters the loop.

### Alternatives rejected

- **External feature-flag service** — cost and dependency we don't need at this size.
- **Trusting local tests as proof of production** — tests don't see the platform, a missing variable, or a failed deploy.

### Why

Turning something off must be a decision that's **reversible in seconds, not a deploy**. And the value promise is audited **against reality, not against intention**.

### Cost accepted

Each switch is one more branch to test.

### Review signals

A switch left OFF **looks like a bug** — which is why the validator reports it as OFF with its variable, rather than as BROKEN.

### Lesson (reusable)

**A green local suite is not evidence about production.** Validate the promise against the live deployment, and make **"deliberately off" a distinct state from "broken"**.
