# 03 — Consumir API externa y anclar dato on-chain (10 min)

## Objetivo
Llamar una API externa (ej: cotización) y guardar el resultado en la red (memo o manageData).

### 1) Prepara proyecto
```bash
npm init -y && npm i node-fetch @stellar/stellar-sdk
```
```js
import fetch from "node-fetch";
const price = (await (await fetch("https://api.coindesk.com/v1/bpi/currentprice/USD.json")).json()).bpi.USD.rate_float;
console.log("price", price);
```

### 2) Escribe el dato en una transacción (memo + manageData)
```js
import { Keypair, Server, TransactionBuilder, Networks, Operation, Memo } from "@stellar/stellar-sdk";
const server = new Server("https://horizon-testnet.stellar.org");
const kp = Keypair.fromSecret(process.env.SECRET);
const acc = await server.loadAccount(kp.publicKey());
const tx = new TransactionBuilder(acc, { fee: "100", networkPassphrase: Networks.TESTNET })
  .addMemo(Memo.text(`USD:${Math.round(price)}`))
  .addOperation(Operation.manageData({ name: "oracle", value: Buffer.from(String(Math.round(price))) }))
  .setTimeout(30).build();
tx.sign(kp);
await server.submitTransaction(tx);
console.log("OK");
```

> Para casos formales, usa contratos Soroban + oráculos.
