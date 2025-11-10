# 02 — Conectar una billetera (neutral, 5–10 min)

## Objetivo
Detectar una billetera en el navegador, obtener la **clave pública** y firmar una transacción simple.

### 1) Requisitos
- Navegador con Freighter o xBull instalado.
- App servida por **HTTPS** en desarrollo.
- Node 18+.

### 2) Proyecto base
```bash
npm init -y
npm i @stellar/stellar-sdk @stellar/freighter-api
```

### 3) Obtener cuenta y firmar (Freighter)
```js
import { Keypair, Networks, Operation, Server, TransactionBuilder, Asset, Transaction } from "@stellar/stellar-sdk";
import { isConnected, requestAccess, getPublicKey, signTransaction } from "@stellar/freighter-api";

const server = new Server("https://horizon-testnet.stellar.org");

async function main() {
  if (!(await isConnected())) await requestAccess();
  const pub = await getPublicKey();

  const account = await server.loadAccount(pub);
  const tx = new TransactionBuilder(account, { fee: "100", networkPassphrase: Networks.TESTNET })
    .addOperation(Operation.manageData({ name: "hello", value: "wallet" }))
    .setTimeout(30)
    .build();

  // firma con Freighter
  const signedXDR = await signTransaction(tx.toXDR(), { network: "TESTNET" });
  const signed = Transaction.fromXDR(signedXDR, Networks.TESTNET);
  const res = await server.submitTransaction(signed);
  console.log("hash:", res.hash);
}
main();
```

### 4) Problemas comunes
- **HTTPS**: si no usas HTTPS, la billetera puede bloquear la conexión.
- **Fondos en Testnet**: usa Friendbot para fondear tu cuenta (en otra guía).
