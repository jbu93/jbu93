<div align="center">

# Juan David Burgos · `jbu93`
### Forward Deployed Engineer | Agentic Systems & RAG Architect

`Flask` · `Groq · Llama 3.3 70B` · `RAG / Pinecone` · `Postgres` · `Railway` · `Docker`

[LinkedIn](https://www.linkedin.com/in/juan-burgos-6ab359411) · Cali, Colombia

</div>

---

Construyo y opero **sistemas agénticos en producción**. No estudio la teoría de la IA agéntica — la despliego, la diagnostico cuando falla y la documento en **post-mortems técnicos reales**. Mi portafolio es el código y los incidentes que cerré, no un certificado.

**Cómo trabajo:** guardrails de seguridad en código (no en el prompt) → RAG sobre evidencia → el LLM entra al final → telemetría a un punto central. El mismo patrón, aplicado en dominios distintos.

---

## 📌 Repos estrella

| Repo | Qué es | Por qué mirarlo |
|---|---|---|
| **[EIR-DR](https://github.com/jbu93/EIR-DR)** | Copiloto clínico odontológico | LLM en camino crítico con **9 guardrails fail-closed**, RAG sobre 33 artículos con DOI, **55/55 tests**. README con arquitectura Mermaid. |
| **[ECOSISTEMA_AESIR](https://github.com/jbu93/ECOSISTEMA_AESIR)** | Monorepo de varios agentes (EIR · VEDOR · SKIRNIR) | Cómo se orquestan, observan y contienen **varios** agentes a la vez. |

---

## 🔬 Evidencia de ingeniería (no certificados)

Publico incidentes que diagnostiqué y cerré, con causa raíz y fix arquitectónico:

- **SEV1** — Secreto de sesión con fallback público (account-takeover) → fail-safe aleatorio, nunca un literal del repo.
- **SEV2** — Entregable corrupto por usar un modelo de imagen para un documento de datos → render determinístico.
- **SEV3** — `/mcp` daba 500 por import inexistente → que un archivo exista ≠ que sus imports resuelvan.

> Generados con un motor propio que **nunca infla métricas**. La credibilidad es el activo.

---

## 🛠️ Stack

**Backend:** Python · Flask · Gunicorn · Pydantic
**IA:** Groq (Llama 3.3 70B) · cascada de visión Gemini → Anthropic · RAG
**Datos:** Postgres · Pinecone · object storage R2/S3
**Infra:** Docker · Railway · PowerShell

<div align="center">

![GitHub Stats](https://github-readme-stats.vercel.app/api?username=jbu93&show_icons=true&theme=tokyonight)
![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=jbu93&layout=compact&theme=tokyonight)

<sub>Construido en producción, no en un bootcamp. La evidencia es el código.</sub>

</div>
