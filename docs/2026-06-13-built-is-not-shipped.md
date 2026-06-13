# Post-Mortem · Construido no es desplegado: la funcionalidad inalcanzable

> **🇪🇸 Versión en español abajo** — **🇬🇧 English version below**

---

## 🇪🇸 Español

**Severidad:** SEV3 · **Fecha:** 2026-06-13 · **Sistema:** copiloto clínico (Flask + Jinja)

### Resumen

Una herramienta de diseño 3D funcional no tenía punto de entrada en la interfaz — solo se podía alcanzar escribiendo la URL a mano. Una auditoría de integridad 360° la encontró y la conectó a la navegación.

### Detección

Un cruce automatizado de "templates ↔ las rutas que los renderizan ↔ enlaces de entrada". La página de la herramienta tenía **cero** enlaces entrantes en la UI.

### Causa raíz

La funcionalidad fue construida y probada a través de su API, pero el paso final — darle una puerta en la UI — nunca se cerró. Causa raíz: **construir no es desplegar.** Una capacidad sin punto de entrada es valor que el usuario nunca ve.

### Fix

Añadí un enlace de entrada en el hub del profesional y en el dashboard, protegido por un feature flag (aparece solo cuando el módulo está habilitado; fail-closed en caso contrario).

### Prevención

El protocolo de auditoría ahora incluye un pilar de Integridad: "cada template debe tener una ruta que lo renderice **y** un enlace de entrada". Se ejecuta al cierre de cada proceso.

### Lección (reutilizable)

Construir no es desplegar. Una funcionalidad sin puerta es trabajo desperdiciado. Una auditoría de huérfanos/integridad debe correr al final de cada proceso, no solo seguridad y lógica.

---

## 🇬🇧 English

# Post-Mortem · Built is not shipped: the unreachable feature

**Severity:** SEV3 · **Date:** 2026-06-13 · **System:** clinical copilot (Flask + Jinja)

### Summary

A working 3D design tool had no entry point in the interface — it could only be reached by typing the URL by hand. A 360° integrity audit found it and wired it into navigation.

### Detection

An automated cross-check of "templates ↔ the routes that render them ↔ entry links." The tool's page had **zero** inbound links in the UI.

### Root cause

The feature was built and tested through its API, but the final step — giving it a door in the UI — was never closed. Root cause: **building is not shipping.** A capability with no entry point is value the user never sees.

### Fix

Added an entry link in the practitioner's hub and dashboard, gated by a feature flag (it appears only when the module is enabled; fail-closed otherwise).

### Prevention

The audit protocol now includes an Integrity pillar: "every template must have a route that renders it **and** an entry link." It runs at the close of every process.

### Lesson (reusable)

Building isn't shipping. A feature with no door is wasted work. An orphan/integrity audit should run at the end of every process, not just security and logic.
