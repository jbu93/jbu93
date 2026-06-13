<div align="center">

# Juan David Burgos · Forward Deployed Engineer / AI Systems

</div>

> **🇪🇸 Español** — Llevo sistemas de IA a **producción**, no al demo. Pongo un LLM en el camino crítico de un producto real y hago que **no se rompa**: guardrails en código (fail-closed), recuperación sobre evidencia (RAG), observabilidad y despliegue.
>
> **🇬🇧 English** — I take AI systems to **production**, not to the demo. I put an LLM on the critical path of a real product and make it **not break**: guardrails in code (fail-closed), retrieval over evidence (RAG), observability, and deployment.

📍 Cali, Colombia · 🛠️ Python · Flask · Groq · RAG · Railway
🔗 [LinkedIn](https://www.linkedin.com/in/juan-burgos-6ab359411)

---

## 🇪🇸 Español

### 🧠 Lo que construyo (mis propios sistemas de ingeniería, en producción/staging)

- **🦷 EIR DR.** — Un copiloto clínico odontológico. Un LLM (Groq · Llama 3.3 70B) en el camino crítico, en streaming, **detrás de guardrails clínicos escritos en código** que bloquean combinaciones peligrosas *antes* de que el modelo sea siquiera invocado. Historias clínicas legales, RAG anclado en evidencia citable, y un **módulo de CAD dental escrito en Python puro** (diseña coronas y puentes fijos de 3 unidades a partir de un escaneo STL, visor 3D para marcar el margen, exportación STL binaria lista para fresado). → 241 tests determinísticos, en verde.
- **🛰️ Ecosistema agéntico** — El mismo patrón (*guardrails → RAG → LLM → telemetría*) generalizado a varios agentes: una tienda agéntica con pagos, y un dashboard de telemetría que triangula eventos de cada servicio.
- **🔬 Motor de Post-Mortem técnico** — Una herramienta que convierte mis incidentes reales en evidencia de ingeniería estructurada (causa raíz → fix arquitectónico → lección reutilizable).

### 🛠️ Stack

Python · Flask / Gunicorn · Groq (Llama 3.3 70B) · RAG / Pinecone · PostgreSQL · Docker · Railway · reportlab · Three.js

### 🔒 Cómo trabajo

- **Guardrails en código, no en el prompt** — las reglas de seguridad son sentencias if, fail-closed.
- **Higiene de secretos** — los secretos viven solo en variables de entorno, nunca en el código.
- **Verificación ejecutable** — si no produce el artefacto, no cuenta.
- **Auditoría forense al final de cada proceso** — pasadas de seguridad, lógica e integridad.

### 📒 Bitácora de ingeniería (post-mortems reales · saneados para público)

- [El contrato frontend↔backend que los tests unitarios no cubren](docs/2026-06-13-endpoint-contract.md)
- ["Se ve correcto" no es "corre": verificar un diseño heredado](docs/2026-06-13-verify-by-running.md)
- [Construido no es desplegado: la funcionalidad inalcanzable](docs/2026-06-13-built-is-not-shipped.md)

> El código de producción vive en repositorios privados (seguridad). Con gusto doy un recorrido técnico a pedido.

### ⚖️ Principio

**Cero métricas infladas.** Mi historial de incidentes empieza en 0 y solo crece con eventos reales. Mi evidencia no son certificados — es código de producción y post-mortems que cualquiera puede leer. Diagnostico, arreglo, documento.

---

## 🇬🇧 English

### 🧠 What I build (my own engineering systems, in production/staging)

- **🦷 EIR DR.** — A dental clinical copilot. An LLM (Groq · Llama 3.3 70B) on the critical path, streaming, **behind clinical guardrails written in code** that block dangerous combinations *before* the model is ever called. Legal clinical records, RAG grounded on citable evidence, and a **dental CAD module written in pure Python** (designs crowns and 3-unit fixed bridges from an STL scan, 3D viewer to mark the margin, binary STL export ready for milling). → 241 deterministic tests, green.
- **🛰️ Agentic ecosystem** — The same pattern (*guardrails → RAG → LLM → telemetry*) generalized across several agents: an agentic store with payments, and a telemetry dashboard that triangulates events from every service.
- **🔬 Technical Post-Mortem engine** — A tool that turns my real incidents into structured engineering evidence (root cause → architectural fix → reusable lesson).

### 🛠️ Stack

Python · Flask / Gunicorn · Groq (Llama 3.3 70B) · RAG / Pinecone · PostgreSQL · Docker · Railway · reportlab · Three.js

### 🔒 How I work

- **Guardrails in code, not in the prompt** — safety rules are if statements, fail-closed.
- **Secret hygiene** — secrets live only in environment variables, never in code.
- **Executable verification** — if it doesn't produce the artifact, it doesn't count.
- **Forensic audit at the end of each process** — security, logic, and integrity passes.

### 📒 Engineering Log (real post-mortems · sanitized for public)

- [The frontend↔backend contract that unit tests don't cover](docs/2026-06-13-endpoint-contract.md)
- ["Looks correct" is not "runs": verifying an inherited design](docs/2026-06-13-verify-by-running.md)
- [Built is not shipped: the unreachable feature](docs/2026-06-13-built-is-not-shipped.md)

> Production code lives in private repositories (security). Happy to give a technical walkthrough on request.

### ⚖️ Principle

**Zero inflated metrics.** My incident history starts at 0 and only grows with real events. My evidence isn't certificates — it's production code and post-mortems anyone can read. I diagnose, I fix, I document.

<sub>Forward Deployed Engineer = orquestando, conteniendo y escalando agentes en producción con un blast radius controlado. / orchestrating, containing and scaling agents in production with a controlled blast radius.</sub>
