# Changelog · Perfil público `github.com/jbu93/jbu93`

Registro de versiones de lo que se publica en el perfil público de GitHub.
Esta carpeta (`PUBLICO_GITHUB/`) es el **espejo local** de ese repositorio: se edita aquí,
se revisa, y se publica. Nada se borra — cada versión **suma**.

**Regla de saneamiento (obligatoria antes de publicar):** sin rutas de módulos, sin nombres
de variables de entorno, sin IPs, sin umbrales exactos, sin nombres de competidores, sin
datos de pacientes ni clientes. Solo el patrón y la lección.

---

## v2 · 2026-07-21

**Motivo:** cinco semanas sin publicar mientras se acumulaba trabajo real (38 registros de
decisión internos entre 2026-07-03 y 2026-07-19). Actualización, no refactor.

**Añadido — 8 entradas nuevas en `docs/` (bilingües):**

| Archivo | Tipo | Origen interno |
|---|---|---|
| `2026-07-05-grounding-cite-or-abstain.md` | Decision Record | D003 |
| `2026-07-05-llm-returns-data-not-code.md` | Decision Record | D004 |
| `2026-07-09-kill-switches-and-promise-validation.md` | Decision Record | D010 |
| `2026-07-09-decisions-as-source-of-truth.md` | Decision Record | D011 |
| `2026-07-12-orchestration-harness-decides.md` | Decision Record | Gerencia de Modelos |
| `2026-07-15-no-uncalibrated-confidence.md` | Decision Record | D033 |
| `2026-07-15-honest-coverage.md` | Decision Record | D027 |
| `2026-07-19-perimeter-hardening.md` | **Post-Mortem** (SEV3) | D038 |

**Cambiado en `README.md`:**
- Métrica de tests actualizada: **241 → 1.072** (verificada contra la suite real, no estimada).
- Bitácora reorganizada en dos bloques: **Post-mortems** (incidentes) y **Registros de decisión**
  (arquitectura). Antes eran una sola lista de 3.
- Nueva sección en "Lo que construyo": **orquestación multi-modelo** (planificador → ejecutor
  → validador con arnés ejecutable).
- Capacidades nuevas de EIR DR. resumidas: recuperación en vivo de evidencia, revisión asistida
  de imagen sin porcentajes no calibrados, auditoría de cuentas con cobertura declarada.
- "Cómo trabajo" gana 3 principios: *el modelo entrega datos nunca código*, *anclar o abstenerse*,
  *el criterio de aceptación es ejecutable*.
- Sello de frescura: línea "Última actualización".

**Sin cambios:** los 3 post-mortems de v1, el principio de cero métricas infladas, el stack base,
la nota de repos privados. **No se borró nada.**

**Nota de sincronización:** la copia local de `docs/` estaba desactualizada (solo inglés) frente
al repo vivo (bilingüe). Se resincronizó desde el repo antes de añadir lo nuevo, para que este
espejo sea fiel.

---

## v1 · 2026-06-13

**Publicado:** README bilingüe (ES/EN) + 3 post-mortems bilingües.

| Archivo | Tipo |
|---|---|
| `2026-06-13-endpoint-contract.md` | Post-Mortem (SEV2) |
| `2026-06-13-verify-by-running.md` | Post-Mortem (SEV2) |
| `2026-06-13-built-is-not-shipped.md` | Post-Mortem (SEV3) |

Métrica de entonces: 241 tests determinísticos.
