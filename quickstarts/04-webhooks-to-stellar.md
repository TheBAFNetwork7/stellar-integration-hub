# 04 — Webhook → Acción on-chain (10 min)

## Caso
Cuando un pago externo (Stripe) o un evento (Twilio) llega vía webhook, ejecuta una operación en Stellar.

### 1) Prepara un endpoint local
```bash
npm i express body-parser @stellar/stellar-sdk
```
```js
import express from "express";
import bodyParser from "body-parser";
import { Server, Keypair, TransactionBuilder, Networks, Operation, Asset } from "@stellar/stellar-sdk";

const server = new Server("https://horizon-testnet.stellar.org");
const app = express(); app.use(bodyParser.json());

app.post("/webhook", async (req, res) => {
  // TODO: verifica firma del proveedor (Stripe/Twilio)
  const kp = Keypair.fromSecret(process.env.SECRET);
  const acc = await server.loadAccount(kp.publicKey());
  const tx = new TransactionBuilder(acc, { fee: "100", networkPassphrase: Networks.TESTNET })
    .addOperation(Operation.payment({ destination: kp.publicKey(), asset: Asset.native(), amount: "1" }))
    .setTimeout(30).build();
  tx.sign(kp);
  await server.submitTransaction(tx);
  res.send({ ok: true });
});
app.listen(3000, () => console.log("listening 3000"));
```

### 2) Conecta proveedor
- Stripe: https://docs.stripe.com/webhooks
- Twilio: https://www.twilio.com/docs/usage/webhooks
