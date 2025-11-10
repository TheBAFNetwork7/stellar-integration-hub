# Stellar Wallets Kit (gestor multi-billetera)

- Sitio: https://stellarwalletskit.dev/
- Documentación: https://creit-tech.github.io/Stellar-Wallets-Kit/
- npm: https://www.npmjs.com/package/@creit.tech/stellar-wallets-kit

## Idea
Una misma API para hablar con varias billeteras (Freighter, xBull, etc.). Útil cuando no quieres manejar cada integración por separado.

## Ejemplo mínimo
```bash
npm i @creit.tech/stellar-wallets-kit
```
```js
import { StellarWalletsKit, WalletNetwork } from "@creit.tech/stellar-wallets-kit";

const swk = new StellarWalletsKit({ network: WalletNetwork.TESTNET });
// abrir modal de conexión (según billeteras detectadas)
const { address } = await swk.openModal(); // dirección pública G...
console.log(address);
```
