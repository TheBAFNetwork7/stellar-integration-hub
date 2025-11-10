# 00 — Setup en Stellar (10 min)

## 1) Instala Freighter y crea cuenta de Testnet
- Instala la extensión y crea/recupera wallet: https://www.freighter.app
- Abre Friendbot y pega tu clave pública para recibir XLM de prueba: https://laboratory.stellar.org/#friendbot

## 2) Verifica tu cuenta por Horizon
- Usa el API Explorer de Laboratory para ver tu balance: https://laboratory.stellar.org/#explorer?resource=accounts

## 3) Envía una transacción mínima (Node)
```bash
npm init -y && npm i @stellar/stellar-sdk
```
```js
import { Keypair, Server, TransactionBuilder, Networks, Operation, Asset } from "@stellar/stellar-sdk";
const server = new Server("https://horizon-testnet.stellar.org");
const kp = Keypair.fromSecret(process.env.SECRET); // **usa una cuenta de prueba**

const account = await server.loadAccount(kp.publicKey());
const tx = new TransactionBuilder(account, { fee: "100", networkPassphrase: Networks.TESTNET })
  .addOperation(Operation.payment({ destination: kp.publicKey(), asset: Asset.native(), amount: "1" }))
  .setTimeout(30).build();
tx.sign(kp);
const res = await server.submitTransaction(tx);
console.log("hash:", res.hash);
```
