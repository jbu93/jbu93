# Post-Mortem · Tráfico de escáner automatizado: endurecer el perímetro sin WAF

> **🇪🇸 Versión en español abajo** — **🇬🇧 English version below**

---

## 🇪🇸 Español

**Severidad:** SEV3 · **Fecha:** 2026-07-19 · **Sistema:** copiloto clínico (producción sobre PaaS)

### Resumen

Los logs HTTP de la plataforma mostraron un escáner automatizado disparando **cientos de sondas** de path traversal y robo de credenciales en pocos minutos. **No hubo brecha** — pero el ruido era real y cada sonda se estaba procesando y logueando.

### Detección

Lectura de los logs HTTP crudos de la plataforma, y luego **verificación del diagnóstico EN EL CÓDIGO** en vez de confiar en un resumen de terceros.

### Hallazgos (causa raíz)

- **Cero brecha:** los secretos viven en variables de entorno de la plataforma, no en disco servible; los únicos endpoints que sirven archivos ya eran anti-traversal (basename + whitelist, regex estricta).
- El interceptor existente **ya devolvía 403** a la mayoría de sondas.
- **Pero:** (a) cada sonda se procesaba y se logueaba → ruido; (b) una familia de sondas se colaba del blocklist y llegaba al enrutador — 404 inofensivos, pero sin cazar.

### Fix

Una capa de **defensa en profundidad** sobre el interceptor existente (no lo reemplaza):

1. **Detección de traversal ampliada**, para rechazar esas sondas **en el borde** en vez de 404 tarde.
2. **Auto-baneo por reincidencia (tarpit):** tras N sondas en una ventana corta, el origen queda baneado por un TTL. El interceptor consulta el baneo **antes que todo** → rechazo en microsegundos, sin procesar ni loguear cada sonda. **Se loguea una sola vez, al banear.**
3. **Memoria acotada:** estado por worker, con purga por TTL y tope duro de orígenes rastreados, para que direcciones rotativas no lo hagan crecer sin límite. Detrás de un kill-switch. **Reloj inyectable → tests deterministas sin `sleep`.**

**Verificado en vivo:** una ráfaga de sondas produjo el baneo esperado; el origen baneado perdió incluso el endpoint de salud; un origen no relacionado siguió en 200.

### Alternativas descartadas

- **WAF de red.** Es **la capa correcta** para que la sonda ni toque la aplicación — pero vive **antes** del contenedor: es una acción de consola, no código. Este tarpit **reduce** ruido y costo; **no los elimina**. Queda declarado.
- **Baneo compartido entre workers** vía almacén externo — se prefirió memoria por worker (simple, sin dependencia dura). Un escáner baneado en un worker puede tocar otro hasta cruzar el umbral ahí. Aceptado: las sondas siempre fallan.
- **Middleware de terceros** — una dependencia extra para algo que cabe en ~120 líneas propias, auditadas y testeadas.

### Costo aceptado

Dejamos de loguear **cada** sonda. Ahora se loguea el baneo una vez; las sondas previas no dejan línea. Es exactamente la reducción de ruido buscada, **a cambio de detalle forense de bajo valor** (siempre fueron 403/404). El baneo es por worker hasta que haya un WAF de red.

### Prevención

Rotar la lista de patrones cuando aparezcan familias nuevas en los logs. Si el volumen de escaneo llega a mover CPU o costo, **escalar a WAF de red**.

### Lección (reutilizable)

**"Nos están escaneando" no es "nos vulneraron"** — verifica en el código antes de reaccionar. Después optimiza para el costo real, que aquí era **ruido de logs y ciclos desperdiciados**, no exposición. Y **nombra la capa que NO implementaste**, para que nadie confunda un tarpit con un WAF.

---

## 🇬🇧 English

# Post-Mortem · Automated scanner traffic: hardening the perimeter without a WAF

**Severity:** SEV3 · **Date:** 2026-07-19 · **System:** clinical copilot (production on a PaaS)

### Summary

Platform HTTP logs showed an automated scanner firing **hundreds of probes** for path traversal and credential theft within a few minutes. **No breach** — but the noise was real, and every probe was being processed and logged.

### Detection

Reading the platform's raw HTTP logs, then **verifying the diagnosis IN THE CODE** rather than trusting a third-party summary.

### Findings (root cause)

- **Zero breach:** secrets live in the platform's environment variables, not on servable disk; the only endpoints that serve files were already traversal-safe (basename + whitelist, strict regex).
- The existing interceptor **already returned 403** to most probes.
- **But:** (a) every probe was processed and logged → noise; (b) a family of probes slipped past the blocklist and reached the router — harmless 404s, but uncaught.

### Fix

A **defense-in-depth** layer over the existing interceptor (not replacing it):

1. **Broader traversal detection**, so those probes are refused **at the edge** instead of 404-ing late.
2. **Auto-ban on repetition (tarpit):** after N probes within a short window, the source is banned for a TTL. The interceptor checks the ban **before anything else** → rejection in microseconds, without processing or logging each probe. **It logs once, at ban time.**
3. **Bounded memory:** per-worker state, with TTL purge and a hard cap on tracked sources, so rotating addresses can't grow it without limit. Behind a kill-switch. **Injectable clock → deterministic tests without `sleep`.**

**Verified live:** a burst of probes produced the expected ban; the banned source lost even the health endpoint; an unrelated source stayed at 200.

### Alternatives rejected

- **A network WAF.** It's **the correct layer** for the probe to never touch the app — but it lives **before** the container: a console action, not code. This tarpit **reduces** noise and cost; it **doesn't eliminate** them. Declared as such.
- **Cross-worker bans** via an external store — preferred per-worker memory (simple, no hard dependency). A scanner banned on one worker can hit another until it crosses the threshold there. Accepted: the probes always fail anyway.
- **Third-party middleware** — an extra dependency for something that fits in ~120 audited, tested lines of our own.

### Cost accepted

We stopped logging **every** probe. Now the ban is logged once; the probes before it leave no line. That's exactly the noise reduction we wanted, **in exchange for low-value forensic detail** (they were always 403/404). The ban is per-worker until a network WAF is in place.

### Prevention

Rotate the pattern list when new probe families appear in the logs. If scan volume ever moves CPU or cost, **escalate to a network WAF**.

### Lesson (reusable)

**"We're being scanned" is not "we're breached"** — verify in the code before reacting. Then optimize for the real cost, which here was **log noise and wasted cycles**, not exposure. And **name the layer you did NOT implement**, so nobody mistakes a tarpit for a WAF.
