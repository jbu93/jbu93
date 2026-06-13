# Post-Mortem · "Se ve correcto" no es "corre": verificar un diseño heredado

> **🇪🇸 Versión en español abajo** — **🇬🇧 English version below**

---

## 🇪🇸 Español

**Severidad:** SEV2 (detectado antes de producción) · **Fecha:** 2026-06-13 · **Sistema:** módulo de CAD dental

### Resumen

Implementé un módulo de CAD dental (diseño de coronas y puentes a partir de un escaneo 3D) en Python puro, partiendo de un diseño conceptual producido en otro lugar. Dos defectos lo habrían hecho fallar en producción. Ambos fueron detectados y corregidos antes de desplegar.

### Detección

Lectura crítica del diseño heredado + tests determinísticos que generan una malla cerrada y corren el pipeline completo de extremo a extremo, en lugar de confiar en que "se veía bien".

### Causa raíz

1. La máquina de estados resolvía el módulo de cada paso por el **nombre del paso** en lugar del **nombre real del archivo** → el import dinámico fallaba siempre. Nunca se había ejecutado.
2. Un nodo indexaba list[-1] cuando su conjunto de entrada estaba vacío → corrompía la geometría silenciosamente (el peor tipo de bug: no se rompe, miente).

Causa raíz en una línea: **un diseño que "se ve correcto" no es código que corre.**

### Fix

1. Mapeo explícito de módulos en la configuración del workflow + una whitelist de nodos permitidos.
2. Un guard que aborta ante un conjunto vacío en lugar de indexarlo.
   Bonus: reemplacé una búsqueda de caminos O(V²) por una basada en heap O(E log V).

### Prevención

17 tests determinísticos que generan geometría y producen un **STL binario válido** de extremo a extremo. Si no produce el archivo, no está hecho. El motor tiene **cero dependencias externas** (Python puro) para determinismo y portabilidad.

### Lección (reutilizable)

La verificación ejecutable es la línea entre "arquitectura en una conversación" y un "producto". Portar un diseño significa ejecutarlo, no copiarlo.

---

## 🇬🇧 English

# Post-Mortem · "Looks correct" is not "runs": verifying an inherited design

**Severity:** SEV2 (caught before production) · **Date:** 2026-06-13 · **System:** dental CAD module

### Summary

I implemented a dental CAD module (designing crowns and bridges from a 3D scan) in pure Python, starting from a conceptual design produced elsewhere. Two defects would have made it fail in production. Both were caught and fixed before deploying.

### Detection

Critical reading of the inherited design + deterministic tests that generate a closed mesh and run the full pipeline end-to-end, instead of trusting that it "looked fine."

### Root cause

1. The state machine resolved each step's module by the **step name** instead of the actual **file name** → the dynamic import failed every time. It had never been run.
2. A node indexed list[-1] when its input set was empty → it silently corrupted geometry (the worst kind of bug: it doesn't crash, it lies).

Root cause in one line: **a design that "looks correct" is not code that runs.**

### Fix

1. Explicit module mapping in the workflow config + a whitelist of allowed nodes.
2. A guard that aborts on an empty set instead of indexing into it.
   Bonus: replaced an O(V²) path search with a heap-based O(E log V) one.

### Prevention

17 deterministic tests that generate geometry and produce a **valid binary STL** end-to-end. If it doesn't produce the file, it isn't done. The engine has **zero external dependencies** (pure Python) for determinism and portability.

### Lesson (reusable)

Executable verification is the line between "architecture in a conversation" and a "product." Porting a design means running it, not copying it.
