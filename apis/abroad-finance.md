# Abroad Finance
**Qué resuelve:** pagos/FX con enfoque en stablecoins y rails tradicionales.
- **Docs:** https://api.abroad.finance/docs/
- **Áreas:** conversions, partner, partnerUser, payments, quote, transactions.
- **Auth:** API Key (usa variables `.env`).
- **Patrón típico:** quote → confirmar → consultar transacción.
- **Snippet mínimo (pseudocódigo):** POST a /quote, luego POST a /payments con el id de la cotización.
