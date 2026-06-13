# Post-Mortem · El contrato frontend↔backend que los tests unitarios no cubren

> **🇪🇸 Versión en español abajo** — **🇬🇧 English version below**

---

## 🇪🇸 Español

**Severidad:** SEV2 · **Fecha:** 2026-06-13 · **Sistema:** copiloto clínico (Flask)

### Resumen

Una funcionalidad de asistente de navegación en el frontend seguía llamando a un endpoint de la API que un refactor anterior había eliminado del backend. Resultado: 404s en producción, y la suite de tests unitarios nunca lo detectó.

### Detección

Una auditoría de rutas: cruzar los endpoints que el backend realmente expone contra las llamadas fetch() que hace el frontend. Varios tests estaban en rojo y habían sido tratados como ruido.

### Causa raíz

Se eliminó una ruta sin auditar **quién la consume** — incluido el frontend. Los tests que la cubrían estaban en rojo y se habían normalizado como "esperado". Los tests unitarios verifican una función en aislamiento; no verifican el contrato entre el navegador y la API.

### Fix

Restauré los endpoints fielmente y realineé la suite de tests a la arquitectura actual. La suite pasó de parcialmente roja a completamente verde.

### Prevención

Regla adoptada: una ruta nunca se elimina sin hacer grep de todos sus consumidores (frontend incluido). Una suite verde es la compuerta para cerrar un cambio — los tests rojos son señales, no ruido.

### Lección (reutilizable)

El contrato frontend↔backend no está cubierto solo por tests unitarios. Antes de eliminar una ruta, audita quién la llama. Un test rojo es información; silenciarlo es cómo los 404s llegan a producción.

---

## 🇬🇧 English

# Post-Mortem · The frontend↔backend contract that unit tests don't cover

**Severity:** SEV2 · **Date:** 2026-06-13 · **System:** clinical copilot (Flask)

### Summary

A navigation-assistant feature in the frontend kept calling an API endpoint that an earlier refactor had removed from the backend. Result: 404s in production, and the unit-test suite never caught it.

### Detection

A route audit: cross-referencing the endpoints the backend actually exposes against the fetch() calls the frontend makes. Several tests were red and had been treated as noise.

### Root cause

A route was deleted without auditing **who consumes it** — including the frontend. The tests that covered it were red and had been normalized as "expected." Unit tests verify a function in isolation; they don't verify the contract between the browser and the API.

### Fix

Restored the endpoints faithfully and realigned the test suite to the current architecture. Suite went from partially red to fully green.

### Prevention

Rule adopted: a route is never removed without grepping every caller (frontend included). A green suite is the gate to close a change — red tests are signals, not noise.

### Lesson (reusable)

The frontend↔backend contract is not covered by unit tests alone. Before deleting a route, audit who calls it. A red test is information; silencing it is how 404s reach prod.
