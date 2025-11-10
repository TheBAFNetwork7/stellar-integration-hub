# Stellar Integration Hub

> Repositorio general para construir e integrar servicios sobre **Stellar**. Incluye guías cortas, catálogo de integraciones (APIs), estándares SEP y ejemplos. Útil para hackathons **y** para desarrollo continuo de equipos y startups.

- **Audiencia:** equipos de hackathon, builders individuales, startups y partners que deseen integrar sus servicios.
- **Objetivo:** onboarding claro, ejemplos reproducibles y un punto único para descubrir y agregar integraciones.

---

## ✨ Objetivos del Hub

1. Centralizar documentación y ejemplos mínimos reproducibles.
2. Facilitar integraciones con servicios externos (pagos, notificaciones, identidad, datos, etc.).
3. Aplicar SEPs clave con explicaciones prácticas y enlaces a fuentes oficiales.
4. Reunir inspiración en un Hall of Fame y fomentar contribuciones por Pull Request.

---
# Stellar Integration Hub (con soporte de billeteras)

Este repositorio centraliza QuickStarts, integraciones (APIs), SEPs, herramientas **y ahora una sección de billeteras** para apps sobre Stellar.

## Estructura
```

```
## 🧭 Estructura del repositorio

```
/quickstarts/      # Guías cortas y neutrales (5–10 min)
/apis/             # Fichas por servicio + registry.yml (catálogo de APIs)
/wallets/          # Cómo integrar billeteras (Freighter, xBull, kits multi-wallet)
/seps/             # Resúmenes prácticos de SEPs relevantes
/tools/            # Tooling opcional (wallets, Horizon/RPC, devcontainers, scaffold, etc.)
/examples/         # Demos mínimas + Hall of Fame (inspiración)
/partners/         # Cómo un partner agrega su API por PR
/.github/          # Templates de PR/Issues + CI mínimo
```

- **Archivo clave:** `apis/registry.yml` → lista legible por máquina de APIs (útil para generar índices automáticos).
- **Ruta sugerida para nuevos equipos:** `README` → `quickstarts` → `apis` → `examples`.

---

## 🧩 Catálogo de Integraciones (APIs)

Cada API debe incluir:
- **Ficha** en `/apis/<nombre>.md` con: qué resuelve, autenticación, sandbox, límites de rate, snippet mínimo y enlaces.
- **Entrada** en `apis/registry.yml` para mantener un índice consistente.
- **QuickStart** (≤10 min) o ejemplo mínimo en `/examples` que se ejecute con claves de prueba.

**Formato sugerido para `apis/registry.yml`:**
```yaml
apis:
  - name: "Stripe"
    category: "Payments"
    docs: "<URL de documentación>"
    openapi: "<URL a OpenAPI si existe>"
    auth: ["api_key", "oauth2"]
    sandbox: true
    tags: ["webhook","checkout","fiat-onramp"]
  - name: "Twilio"
    category: "Comms"
    docs: "<URL de documentación>"
    openapi: "<URL a OpenAPI si existe>"
    auth: ["api_key"]
    sandbox: true
    tags: ["sms","voice","webhook"]
```
**Categorías comunes:** `Payments`, `Comms`, `Identity/KYC`, `Data/Oracles`, `Analytics`, `Ops`.

---

## 📚 SEPs esenciales (visión práctica)

- **SEP-10 (WebAuth):** autenticación entre cliente (wallet/app) y servidor mediante desafíos firmados.
- **SEP-24 (Depósitos/Retiros):** flujo interactivo para on/off-ramps.
- **SEP-31 (Send/Payouts):** pagos entre anchors; habitual en remesas.
- **SEP-38 (Rates/RFQ):** cotizaciones firmes/indicativas entre fiat y activos on-chain.

> En `/seps/` agrega “cuándo usarlo”, diagramas simples y enlaces oficiales.

---

## 🛠️ Herramientas (opcionales y generales)

- **Wallets y Horizon/RPC:** cómo consultar balances, enviar transacciones y explorar la red.
- **Plantillas/Scaffolds:** por ejemplo, herramientas para generar dApps o contratos con frontends.
- **Devcontainers/Codespaces:** entorno reproducible (Node, Rust, etc.) en `/.devcontainer/`.
- **CI básico:** validaciones mínimas en `/.github/workflows/ci.yml` (por ejemplo, que exista `apis/registry.yml`).

---

## 🧪 QuickStarts (neutrales)

Incluye guías cortas y genéricas (no atadas a una herramienta específica) con estos criterios:
- **Duración objetivo:** 5–10 min.
- **Formato:** pasos numerados, comandos copiables y variables `.env` claras.
- **Resultados verificables:** qué se espera ver al final (salida de consola, transacción, evento simulado, etc.).

Ejemplos de temas:
- **A. Integración de API externa (neutral):** consumir un endpoint público y almacenar el resultado on-chain o en un log verificable.
- **B. Webhooks (neutral):** recibir un POST firmado y disparar una acción (encolar un trabajo, registrar un evento, etc.).
- **C. Flujo con SEPs (simulado):** bosquejo de interacción cliente-servidor siguiendo SEP-10/24/31/38, sin acoplarse a un proveedor concreto.

---

## 🏆 Hall of Fame (inspiración)

En `examples/README.md`, agrega proyectos o demos destacadas con:
- 1–2 frases de impacto (qué problema resuelve).
- Stack principal (lenguajes, frameworks, SDKs).
- Enlaces a repo y demo.
- Etiquetas: Remesas, On/Off-ramp, DeFi, Identidad/KYC, Datos, Gaming, AI+Stellar, etc.

---

## 🤝 Cómo contribuir

1. Crea una rama y agrega:
   - Ficha de tu API en `/apis/<tu-api>.md`.
   - Entrada en `apis/registry.yml`.
   - Un QuickStart o ejemplo mínimo reproducible.
2. Abre un Pull Request usando `/.github/PULL_REQUEST_TEMPLATE.md`.
3. Responde el feedback: sandbox, manejo de errores, validación de firmas/headers en webhooks, descripción clara del flujo.

**Requisitos mínimos para integraciones:**
- **Sandbox** o plan de prueba.
- **Documentación pública** (ideal: OpenAPI 3.0).
- **Ejemplo reproducible** con claves de prueba y tratamiento básico de errores/timeouts.

---

## ✅ Barra de calidad (para evaluar y aceptar PRs/proyectos)

- **Valor de la integración:** caso de uso claro y medible.
- **Robustez:** reintentos, idempotencia, validación de firmas en webhooks, timeouts y backoff.
- **Seguridad:** secretos fuera del repo, autenticación adecuada, cumplimiento de SEPs cuando aplique.
- **DX:** README claro, configuración < 10 min, variables `.env` documentadas.
- **Observabilidad:** logs suficientes para reproducir errores o auditoría mínima.

---

## 🗓️ Uso en eventos (opcional)

Si se usa en una hackathon o programa específico, añade en esta sección:
- Enlaces de registro, fechas y reglas.
- Canales de soporte (Slack/Discord/Email) y horarios.
- Pinned Issues: **Add your API** / **Add your QuickStart**.
- Criterios de evaluación (pueden basarse en la **Barra de calidad**).

> Fuera de eventos, el Hub sirve como repositorio vivo para desarrollo continuo.

---

## 📄 Licencia

MIT — Verifica que tienes derecho a compartir cualquier código o contenido que aportes.

---

## 📬 Contacto

- Mantenedores: `<@equipo o usuario>`
- Colaboraciones/soporte: `<email o enlace>`
