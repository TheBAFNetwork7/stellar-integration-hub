# Stripe (Payments)

**Qué resuelve**: cobros con tarjeta, suscripciones y webhooks (ideal para flujos fiat↔cripto fuera de cadena).

- **Docs**: https://docs.stripe.com/api
- **OpenAPI**: https://raw.githubusercontent.com/stripe/openapi/master/openapi/spec3.json
- **Sandbox**: disponible (claves de prueba).
- **Patrones**: webhook → acción on-chain; onramp fiat → depósito (SEP-24/31).

### Snippet (Node) — crear PaymentIntent de prueba
```bash
npm i stripe
```
```js
import Stripe from "stripe";
const stripe = new Stripe(process.env.STRIPE_KEY, { apiVersion: "2024-06-20" });

const pi = await stripe.paymentIntents.create({
  amount: 5000, currency: "usd",
  automatic_payment_methods: { enabled: true }
});
console.log(pi.client_secret);
```

### Siguiente paso
- Conecta el webhook y reacciona on-chain (ver `quickstarts/04-webhooks-to-stellar.md`).
