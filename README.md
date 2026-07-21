<div align="center">

# Juan David Burgos · Forward Deployed Engineer / AI Systems

</div>

> **🇪🇸 Español** — Llevo sistemas de IA a **producción**, no al demo. Pongo un LLM en el camino crítico de un producto real y hago que **no se rompa**: guardrails en código (fail-closed), recuperación sobre evidencia (RAG), observabilidad y despliegue.
>
> **🇬🇧 English** — I take AI systems to **production**, not to the demo. I put an LLM on the critical path of a real product and make it **not break**: guardrails in code (fail-closed), retrieval over evidence (RAG), observability, and deployment.

📍 Cali, Colombia · 🛠️ Python · Flask · Groq · RAG · Railway
🔗 [LinkedIn](https://www.linkedin.com/in/juan-burgos-6ab359411)

<sub>Última actualización / Last updated: **2026-07-21**</sub>

---

## 🇪🇸 Español

### 🧠 Lo que construyo (mis propios sistemas de ingeniería, en producción/staging)

- **🦷 EIR DR.** — Un copiloto clínico odontológico. Un LLM en el camino crítico, en streaming, **detrás de guardrails clínicos escritos en código** que bloquean combinaciones peligrosas *antes* de que el modelo sea siquiera invocado. Historias clínicas legales, **RAG anclado en evidencia citable con recuperación en vivo**, revisión asistida de imagen **sin porcentajes que el modelo no pueda calibrar**, auditoría de cuentas de salud con **cobertura declarada regla por regla**, y un **módulo de CAD dental en Python puro** (coronas y puentes fijos de 3 unidades desde un escaneo STL, visor 3D, exportación STL lista para fresado). → **1.072 tests determinísticos, en verde.**
- **🛰️ Ecosistema agéntico** — El mismo patrón (*guardrails → RAG → LLM → telemetría*) generalizado a varios agentes: una tienda agéntica con pagos y un dashboard de telemetría que triangula eventos de cada servicio.
- **🎛️ Orquestación multi-modelo** — Un ciclo **planificador → ejecutor → validador** donde el criterio de aceptación es un **arnés ejecutable** (PASS/FAIL por criterio, salida 0/1): el juicio vive en código, no en el auto-reporte del modelo.
- **🔬 Motor de Post-Mortem técnico** — Una herramienta que convierte mis incidentes reales en evidencia de ingeniería estructurada (causa raíz → fix arquitectónico → lección reutilizable).

### 🛠️ Stack

Python · Flask / Gunicorn · LLMs en cadena resiliente multi-proveedor · RAG / Pinecone · PostgreSQL · Docker · Railway · reportlab · Three.js

### 🔒 Cómo trabajo

- **Guardrails en código, no en el prompt** — las reglas de seguridad son sentencias if, fail-closed.
- **El modelo entrega datos, nunca código** — su salida es dato no confiable; el render lo hace mi código, en sandbox.
- **Anclar o abstenerse** — si no puede citar una fuente real, el sistema dice "no encontré". "No encontré" también es un hallazgo.
- **El criterio de aceptación es ejecutable** — un modelo diciendo "hecho" no es evidencia; un arnés saliendo con código 0 sí.
- **Higiene de secretos** — los secretos viven solo en variables de entorno, nunca en el código.
- **Verificación ejecutable** — si no produce el artefacto, no cuenta.
- **Auditoría forense al final de cada proceso** — pasadas de seguridad, lógica e integridad.

### 📒 Bitácora de ingeniería (casos reales · saneados para público)

**Post-mortems (incidentes reales)**

- [Tráfico de escáner automatizado: endurecer el perímetro sin WAF](docs/2026-07-19-perimeter-hardening.md) · SEV3
- [El contrato frontend↔backend que los tests unitarios no cubren](docs/2026-06-13-endpoint-contract.md) · SEV2
- ["Se ve correcto" no es "corre": verificar un diseño heredado](docs/2026-06-13-verify-by-running.md) · SEV2
- [Construido no es desplegado: la funcionalidad inalcanzable](docs/2026-06-13-built-is-not-shipped.md) · SEV3

**Registros de decisión (arquitectura y trade-offs)**

- [Anclaje a evidencia: citar una fuente real o decir "no encontré"](docs/2026-07-05-grounding-cite-or-abstain.md)
- [El LLM entrega DATOS; el render lo hace nuestro código](docs/2026-07-05-llm-returns-data-not-code.md)
- [Ningún porcentaje de confianza que el modelo no pueda calibrar](docs/2026-07-15-no-uncalibrated-confidence.md)
- [Cobertura honesta: nombra cada regla que NO revisas](docs/2026-07-15-honest-coverage.md)
- [Kill-switch en toda función de riesgo + loop promesa-contra-producción](docs/2026-07-09-kill-switches-and-promise-validation.md)
- [Orquestación de modelos: decide el arnés, no el auto-reporte del modelo](docs/2026-07-12-orchestration-harness-decides.md)
- [La deuda de conocimiento: las decisiones son la fuente de verdad](docs/2026-07-09-decisions-as-source-of-truth.md)

> El código de producción vive en repositorios privados (seguridad). Con gusto doy un recorrido técnico a pedido.

### ⚖️ Principio

**Cero métricas infladas.** Mi historial de incidentes empieza en 0 y solo crece con eventos reales. Mi evidencia no son certificados — es código de producción y post-mortems que cualquiera puede leer. Diagnostico, arreglo, documento.

---

## 🇬🇧 English

### 🧠 What I build (my own engineering systems, in production/staging)

- **🦷 EIR DR.** — A dental clinical copilot. An LLM on the critical path, streaming, **behind clinical guardrails written in code** that block dangerous combinations *before* the model is ever called. Legal clinical records, **RAG grounded on citable evidence with live retrieval**, assisted image review **with no percentages the model cannot calibrate**, a health-claims audit module with **coverage declared rule by rule**, and a **dental CAD module in pure Python** (crowns and 3-unit fixed bridges from an STL scan, 3D viewer, binary STL export ready for milling). → **1,072 deterministic tests, green.**
- **🛰️ Agentic ecosystem** — The same pattern (*guardrails → RAG → LLM → telemetry*) generalized across several agents: an agentic store with payments and a telemetry dashboard that triangulates events from every service.
- **🎛️ Multi-model orchestration** — A **planner → executor → validator** cycle where the acceptance criterion is an **executable harness** (PASS/FAIL per criterion, exit 0/1): judgment lives in code, not in the model's self-report.
- **🔬 Technical Post-Mortem engine** — A tool that turns my real incidents into structured engineering evidence (root cause → architectural fix → reusable lesson).

### 🛠️ Stack

Python · Flask / Gunicorn · LLMs in a resilient multi-provider chain · RAG / Pinecone · PostgreSQL · Docker · Railway · reportlab · Three.js

### 🔒 How I work

- **Guardrails in code, not in the prompt** — safety rules are if statements, fail-closed.
- **The model returns data, never code** — its output is untrusted data; my code does the rendering, sandboxed.
- **Ground or abstain** — if it can't cite a real source, the system says "I didn't find it". That's also a finding.
- **The acceptance criterion is executable** — a model saying "done" is not evidence; a harness exiting 0 is.
- **Secret hygiene** — secrets live only in environment variables, never in the code.
- **Executable verification** — if it doesn't produce the artifact, it doesn't count.
- **Forensic audit at the end of each process** — security, logic, and integrity passes.

### 📒 Engineering Log (real cases · sanitized for public)

**Post-mortems (real incidents)**

- [Automated scanner traffic: hardening the perimeter without a WAF](docs/2026-07-19-perimeter-hardening.md) · SEV3
- [The frontend↔backend contract that unit tests don't cover](docs/2026-06-13-endpoint-contract.md) · SEV2
- ["Looks correct" is not "runs": verifying an inherited design](docs/2026-06-13-verify-by-running.md) · SEV2
- [Built is not shipped: the unreachable feature](docs/2026-06-13-built-is-not-shipped.md) · SEV3

**Decision records (architecture and trade-offs)**

- [Grounding: cite a real source or say "I didn't find it"](docs/2026-07-05-grounding-cite-or-abstain.md)
- [The LLM returns DATA; our code does the rendering](docs/2026-07-05-llm-returns-data-not-code.md)
- [No confidence percentage the model cannot calibrate](docs/2026-07-15-no-uncalibrated-confidence.md)
- [Honest coverage: name every rule you do NOT check](docs/2026-07-15-honest-coverage.md)
- [Kill-switch on every risky feature + a promise-vs-production loop](docs/2026-07-09-kill-switches-and-promise-validation.md)
- [Model orchestration: the harness decides, not the model's self-report](docs/2026-07-12-orchestration-harness-decides.md)
- [Knowledge debt: decisions are the source of truth](docs/2026-07-09-decisions-as-source-of-truth.md)

> Production code lives in private repositories (security). Happy to give a technical walkthrough on request.

### ⚖️ Principle

**Zero inflated metrics.** My incident history starts at 0 and only grows with real events. My evidence isn't certificates — it's production code and post-mortems anyone can read. I diagnose, I fix, I document.

<sub>Forward Deployed Engineer = orquestando, conteniendo y escalando agentes en producción con un blast radius controlado. / orchestrating, containing and scaling agents in production with a controlled blast radius.</sub>
