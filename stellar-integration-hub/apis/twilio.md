# Twilio (Comunicaciones)

**Qué resuelve**: SMS/voz/verificación para notificar o confirmar operaciones.

- **Docs**: https://www.twilio.com/docs
- **OpenAPI**: https://raw.githubusercontent.com/twilio/twilio-oai/main/spec/json/twilio_api_v2010.json

### Snippet (Node) — enviar SMS de prueba
```bash
npm i twilio
```
```js
import twilio from "twilio";
const client = twilio(process.env.TWILIO_SID, process.env.TWILIO_TOKEN);
await client.messages.create({ to: "+573001112233", from: "+15005550006", body: "Hola desde la hackathon 🚀" });
```
