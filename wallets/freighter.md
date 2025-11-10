# Freighter (extensión de navegador)

- Sitio: https://www.freighter.app
- Repositorio: https://github.com/stellar/freighter
- Guías dev: https://developers.stellar.org/docs/build/guides/freighter
- Guía “prompt to sign tx”: https://developers.stellar.org/docs/build/guides/freighter/prompt-to-sign-tx
- Guía de uso en web app (API): https://docs.freighter.app/docs/guide/usingfreighterwebapp/
- Nota: requiere **HTTPS** en local para interactuar con tu dApp (ver guía de frontend en docs de Stellar).

## Uso básico (JS)
Instala la lib cliente:
```bash
npm i @stellar/freighter-api
```

Ejemplo mínimo (obtener cuenta y firmar una transacción preparada como XDR):
```js
import { isConnected, requestAccess, getPublicKey, signTransaction } from "@stellar/freighter-api";

if (!(await isConnected())) {
  await requestAccess(); // abre el popup para conectar
}

const pubKey = await getPublicKey(); // GABC...

/**
 * txXDR: cadena XDR de la transacción (preparada con @stellar/stellar-sdk)
 * network: "TESTNET" o "PUBLIC"
 */
const signed = await signTransaction(txXDR, { network: "TESTNET" });
// envía 'signed' a Horizon con @stellar/stellar-sdk
```
