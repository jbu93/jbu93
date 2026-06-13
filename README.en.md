<div align="center">

# Juan David Burgos · `jbu93`
### Forward Deployed Engineer | Agentic Systems & RAG Architect

`Flask` · `Groq · Llama 3.3 70B` · `RAG / Pinecone` · `Postgres` · `Railway` · `Docker`

[LinkedIn](https://www.linkedin.com/in/juan-burgos-6ab359411) · Cali, Colombia

[Read in Spanish / Leer en español](./README.md)

</div>

---

I build and operate **agentic systems in production**. I don't study the theory of agentic AI — I deploy it, diagnose it when it fails, and document it in **real technical post-mortems**. My portfolio is the code and the incidents I closed, not a certificate.

**How I work:** security guardrails in code (not in the prompt) -> RAG over evidence -> the LLM runs last -> telemetry to a central point. The same pattern, applied across different domains.

---

## Featured repos

| Repo | What it is | Why look at it |
|---|---|---|
| **[EIR-DR](https://github.com/jbu93/EIR-DR)** | Dental clinical copilot | LLM on the critical path behind **fail-closed clinical guardrails**, RAG over evidence (DOI), and a **pure-Python dental CAD module** (crown/bridge design from an STL scan, 3D viewer, export to milling). 241 deterministic tests green. |
| **[ECOSISTEMA_AESIR](https://github.com/jbu93)** | Agent monorepo | The pattern *guardrails -> RAG -> LLM -> telemetry* generalized across several agents: an agentic store with payments and a centralized telemetry dashboard. |

---

## Stack
Python · Flask / Gunicorn · Groq (Llama 3.3 70B) · RAG / Pinecone · PostgreSQL · Docker · Railway · reportlab · Three.js

---

## How I work (this week, for example)
I build in public and with traceability. This week: I closed 6 administrative phases of EIR DR., built a sovereign dental CAD module (pure-Python geometry engine, no external dependencies), and ran a 360 degree forensic audit protocol that detected and fixed orphaned endpoints, a feature with no entry point, and hardening gaps — every finding documented as a technical post-mortem.

---

## Principle
Zero inflated metrics. My track record starts at 0 and grows only with real incidents. My evidence isn't certificates: it's code in production and post-mortems anyone can read. I diagnose, I fix, I document.

<sub>Forward Deployed Engineer = orchestrate, contain, and scale agents in production with a controlled blast radius.</sub>
