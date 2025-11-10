# <Nombre de la API>

**Qué resuelve:** <1–2 líneas>

## Enlaces
- Docs: <URL>
- OpenAPI (si existe): <URL>

## Autenticación & API keys
- Cómo obtener la key: <ruta en dashboard y modo test>
- Variables .env necesarias:
  - `NOMBRE_API_KEY=`
  - `NOMBRE_WEBHOOK_SECRET=` (si aplica)

## Snippet mínimo (Node)
```bash
npm i node-fetch dotenv
js
Copy code
import 'dotenv/config';
import fetch from 'node-fetch';
const r = await fetch('<endpoint>', { headers: { Authorization: `Bearer ${process.env.NOMBRE_API_KEY}` } }).then(r=>r.json());
console.log(r);
Contacto del integrador
Email/Discord: <contacto>

yaml
Copy code

---

# `/apis/stripe.md`
```md
# Stripe

**Qué resuelve:** cobros con tarjeta, suscripciones, on-ramp y webhooks.

## Enlaces
- Docs: https://docs.stripe.com/api
- Webhooks: https://docs.stripe.com/webhooks

## Autenticación & API keys
- Clave **test** `sk_test_…` desde el Dashboard → Developers → API keys.
- Webhook **Signing secret** `whsec_…` (crea tu endpoint y copia el secret).
- **Variables .env**:
  - `STRIPE_SECRET=`
  - `STRIPE_WEBHOOK_SECRET=`

## Snippet mínimo (Node)
```bash
npm i stripe dotenv
js
Copy code
import 'dotenv/config';
import Stripe from 'stripe';
const stripe = new Stripe(process.env.STRIPE_SECRET);
Contacto del integrador
Email/Discord: <contacto>

yaml
Copy code

---

# `/apis/twilio.md`
```md
# Twilio

**Qué resuelve:** SMS/voz/WhatsApp, webhooks entrantes (mensajes/calls), OTP (Verify).

## Enlaces
- Docs: https://www.twilio.com/docs
- Verify: https://www.twilio.com/docs/verify
- Webhooks: https://www.twilio.com/docs/usage/webhooks

## Autenticación & API keys
- `TWILIO_API_KEY`, `TWILIO_API_SECRET`, `TWILIO_SID` desde la consola.
- **Variables .env**:
  - `TWILIO_SID=`
  - `TWILIO_API_KEY=`
  - `TWILIO_API_SECRET=`

## Snippet mínimo (Node)
```bash
npm i twilio dotenv
js
Copy code
import 'dotenv/config';
import twilio from 'twilio';
const client = twilio(process.env.TWILIO_API_KEY, process.env.TWILIO_API_SECRET, { accountSid: process.env.TWILIO_SID });
Contacto del integrador
Email/Discord: <contacto>

yaml
Copy code

---

# `/apis/abroad-finance.md`
```md
# Abroad Finance

**Qué resuelve:** pagos/FX con enfoque en stablecoins y rails tradicionales.

## Enlaces
- Docs/API Portal: https://api.abroad.finance/docs/
- (Si está) OpenAPI JSON: puede exponerse detrás de la UI.

## Autenticación & API keys
- Genera una **API Key** en su portal.
- **Variables .env**:
  - `ABROAD_KEY=`

## Snippet mínimo (Node; esquema)
```bash
npm i node-fetch dotenv
js
Copy code
import 'dotenv/config';
import fetch from 'node-fetch';

const r = await fetch('https://api.abroad.finance/<endpoint>', {
  method: 'POST',
  headers: { Authorization: `Bearer ${process.env.ABROAD_KEY}`, 'Content-Type': 'application/json' },
  body: JSON.stringify({ /* payload */ })
}).then(r => r.json());

console.log(r);
Contacto del integrador
Email/Discord: <contacto>

yaml
Copy code

---

# `/wallets/README.md`
```md
# Billeteras (Wallets)

Cómo conectar tu app a billeteras del ecosistema Stellar.

## Opciones
- **Freighter** (extensión; firma transacciones y Soroban).
- **xBull** (extensión; open source).
- **Kits multi-billetera** (una API para varias wallets).

> Requisito común: sirve tu app por **HTTPS** en desarrollo.