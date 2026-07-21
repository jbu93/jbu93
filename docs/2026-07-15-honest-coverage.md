# Decision Record · Cobertura honesta: nombra cada regla que NO revisas

> **🇪🇸 Versión en español abajo** — **🇬🇧 English version below**

---

## 🇪🇸 Español

**Fecha:** 2026-07-15 · **Sistema:** módulo de auditoría de cuentas de salud · **Estado:** vigente

### Problema

Un módulo de auditoría salió cubriendo **2 de 97 reglas oficiales** de validación. Fue honesto — el ejecutor se negó a inventar el significado de reglas que no había leído — pero era poco. Y la pantalla le decía al usuario *"revisamos 2 de 97"*.

### Decisión

1. **Cargar las 97 reglas oficiales al repo como dato versionado**, cada una con su código, campos, severidad y **texto oficial literal**. Cuando salga una revisión del estándar, es una actualización de datos, no un rewrite.
2. **Triar las 97 contra una sola pregunta:** *¿esto se puede verificar de verdad con los datos que sí tenemos?* Resultado:
   - **5 verificables** → implementadas.
   - **18 exigen tablas de referencia externas** que no tenemos (que un código *esté presente* ≠ que *exista* en la tabla oficial).
   - **8 exigen cruzar contra la factura** validada por la autoridad tributaria.
   - **66 aplican a tipos de atención** que este entorno nunca reporta.
3. Las 3 reglas nuevas son **comparaciones de fecha puras** sobre campos que ya emitimos, y **se abstienen cuando el dato falta** — nada que comparar, ningún falso positivo.
4. **Cada una de las 92 no verificadas se declara individualmente**, con su código, su texto oficial y su razón. La cobertura **cuadra por construcción: 5 + 92 = 97**, con candado de test.
5. Nuestros chequeos propios adicionales quedan **fuera** del conteo oficial. Sumarlos leería "13 de 97" e **inflaría** el número.

### Alternativas descartadas

- **Implementar más reglas "de memoria" o fingir las tablas.** Si el validador oficial rechaza una cuenta por una regla que dijimos revisar, la culpa es nuestra. **5 ciertas le ganan a 30 dudosas.**

### Costo aceptado

Siguen siendo 5 de 97. Es 2,5× lo anterior y es todo lo verificable sin tablas externas — el grueso espera trabajo de campo.

### Lección (reutilizable)

**La cobertura es una promesa.** Declara el denominador, **nombra lo que no revisas y por qué**, y convierte la aritmética en un test. Un número que no puedes defender no es una feature: es un pasivo.

---

## 🇬🇧 English

# Decision Record · Honest coverage: name every rule you do NOT check

**Date:** 2026-07-15 · **System:** health-claims audit module · **Status:** active

### Problem

An audit module shipped covering **2 of 97 official validation rules**. It was honest — the executor refused to invent the meaning of rules it hadn't read — but thin. And the screen told the user *"we check 2 of 97"*.

### Decision

1. **Load all 97 official rules into the repo as versioned data**, each with its code, fields, severity and **literal official text**. When a revision of the standard ships, it's a data update, not a rewrite.
2. **Triage all 97 against a single question:** *can this actually be verified with the data we truly hold?* Result:
   - **5 verifiable** → implemented.
   - **18 require external reference tables** we don't hold (a code being *present* ≠ it *existing* in the official table).
   - **8 require cross-checking against the invoice** validated by the tax authority.
   - **66 apply to encounter types** this setting never reports.
3. The 3 new rules are **pure date comparisons** over fields we already emit, and they **abstain when the data is missing** — nothing to compare, no false positive.
4. **Each of the 92 unverified rules is declared individually**, with its code, official text and reason. Coverage **adds up by construction: 5 + 92 = 97**, locked by a test.
5. Our own extra checks stay **outside** the official count. Adding them would read "13 of 97" and **inflate** the number.

### Alternatives rejected

- **Implement more rules "from memory" or fake the tables.** If the official validator rejects a claim over a rule we said we check, that's our fault. **5 certain beats 30 doubtful.**

### Cost accepted

It's still 5 of 97. That's 2.5× the previous figure and everything verifiable without external tables — the bulk awaits fieldwork.

### Lesson (reusable)

**Coverage is a promise.** State the denominator, **name what you skip and why**, and make the arithmetic a test. A number you can't defend isn't a feature — it's a liability.
