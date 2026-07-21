# Decision Record · Ningún porcentaje de confianza que el modelo no pueda calibrar

> **🇪🇸 Versión en español abajo** — **🇬🇧 English version below**

---

## 🇪🇸 Español

**Fecha:** 2026-07-15 · **Sistema:** copiloto clínico — revisión asistida de imagen · **Estado:** vigente (beta deliberada)

### Problema

En esta categoría de producto es común pintar hallazgos con "96% de confianza". Pero un LLM multimodal general **no produce probabilidades calibradas**. Pintar un porcentaje es **precisión falsa** — y presentarlo como diagnóstico roza el territorio regulado de dispositivo médico.

### Decisión

Una capa honesta sobre el motor de visión existente:

1. **Nunca es diagnóstico** — la respuesta se marca explícitamente como no diagnóstica, con el descargo pegado al resultado.
2. **Sin porcentajes** — el prompt los prohíbe **y** existe un **candado de salida** que, si el modelo desobedece y emite un `%`, lo retira y lo reemplaza por "(revisar)". Preferimos "revisar pieza 14" sin número a un "96%" inventado.
3. **Jamás escribe la historia clínica** — devuelve piezas a revisar; el profesional confirma una por una.
4. **Motor caído se declara, no se inventa.**
5. Sale detrás de un **kill-switch**, en beta deliberada y sin UI destacada hasta validarla con profesionales reales.

### Alternativas descartadas

- **Mostrar un % "como la competencia"** — precisión falsa. Un modelo especializado y calibrado (o un tercero certificado) es la única vía honesta hacia números.
- **Imagen → llenar la historia clínica automáticamente** — la imagen no manda; el criterio del clínico manda.

### Costo aceptado

La función **se ve menos impresionante en un demo** que una que imprime números.

### Lección (reutilizable)

No renderices un número que tu modelo no puede calibrar. Y hazlo cumplir con un **candado de salida**: una instrucción en el prompt es una petición, no una restricción.

---

## 🇬🇧 English

# Decision Record · No confidence percentage the model cannot calibrate

**Date:** 2026-07-15 · **System:** clinical copilot — assisted image review · **Status:** active (deliberate beta)

### Problem

In this product category it's common to paint findings with "96% confidence". But a general multimodal LLM **does not produce calibrated probabilities**. Printing a percentage is **false precision** — and presenting it as a diagnosis edges into regulated medical-device territory.

### Decision

An honest layer over the existing vision engine:

1. **Never a diagnosis** — the response is explicitly flagged as non-diagnostic, with the disclaimer attached to the result itself.
2. **No percentages** — the prompt forbids them **and** an **output guard** strips any `%` the model emits anyway, replacing it with "(review)". "Review tooth 14" without a number beats an invented "96%".
3. **Never writes the clinical chart** — it returns items to review; the practitioner confirms them one by one.
4. **Engine down is declared, not invented.**
5. Ships behind a **kill-switch**, in deliberate beta with no prominent UI until validated with real practitioners.

### Alternatives rejected

- **Show a % "like the competition"** — false precision. A calibrated specialist model (or a certified third party) is the only honest route to numbers.
- **Image → auto-fill the clinical chart** — the image doesn't decide; the clinician does.

### Cost accepted

The feature **looks less impressive in a demo** than one that prints numbers.

### Lesson (reusable)

Don't render a number your model cannot calibrate. And enforce it with an **output guard**: a prompt instruction is a request, not a constraint.
