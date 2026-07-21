<div align="center">

# Juan David Burgos · `jbu93`
### Forward Deployed Engineer | Agentic Systems & RAG Architect

`Flask` · `Multi-provider LLM chain` · `RAG / Pinecone` · `Postgres` · `Railway` · `Docker`

[LinkedIn](https://www.linkedin.com/in/juan-burgos-6ab359411) · Cali, Colombia

[Read in Spanish / Leer en español](./README.md)

</div>

---

I build and operate **agentic systems in production**. I don't study the theory of agentic AI — I deploy it, diagnose it when it fails, and document it in **real technical post-mortems and decision records**. My portfolio is the code and the incidents I closed, not a certificate.

**How I work:** security guardrails in code (not in the prompt) -> RAG over evidence -> the LLM runs last -> telemetry to a central point. The same pattern, applied across different domains.

---

## Featured repos

| Repo | What it is | Why look at it |
|---|---|---|
| **[EIR-DR](https://github.com/jbu93/EIR-DR)** | Dental clinical copilot | LLM on the critical path behind **fail-closed clinical guardrails**, RAG over evidence with **live retrieval**, assisted image review with **no uncalibrated confidence scores**, a health-claims audit with **coverage declared rule by rule**, and a **pure-Python dental CAD module** (crown/bridge design from an STL scan, 3D viewer, export to milling). **1,072 deterministic tests green.** |
| **[ECOSISTEMA_AESIR](https://github.com/jbu93)** | Agent monorepo | The pattern *guardrails -> RAG -> LLM -> telemetry* generalized across several agents: an agentic store with payments and a centralized telemetry dashboard. |

---

## Stack
Python · Flask / Gunicorn · LLMs in a resilient multi-provider chain · RAG / Pinecone · PostgreSQL · Docker · Railway · reportlab · Three.js

---

## Engineering principles I actually enforce

- **Guardrails in code, not in the prompt** — safety rules are `if` statements, fail-closed.
- **The model returns data, never code** — its output is untrusted data; my code renders it, sandboxed.
- **Ground or abstain** — if it can't cite a real source, the system says "I didn't find it".
- **No number the model can't calibrate** — enforced by an output guard, not by a prompt request.
- **The acceptance criterion is executable** — a model saying "done" is not evidence; a harness exiting 0 is.
- **Coverage is a promise** — state the denominator and name what you don't check.

📒 **[Read the full engineering log →](./README.md#-bitácora-de-ingeniería-casos-reales--saneados-para-público)** — post-mortems of real incidents and decision records with their trade-offs and accepted costs.

---

## Principle
Zero inflated metrics. My track record starts at 0 and grows only with real incidents. My evidence isn't certificates: it's code in production and post-mortems anyone can read. I diagnose, I fix, I document.

<sub>Forward Deployed Engineer = orchestrate, contain, and scale agents in production with a controlled blast radius.</sub>
