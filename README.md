# WhatsApp API Bot

Proyecto en Node.js para recibir y responder mensajes de WhatsApp mediante webhooks, con soporte para flujo guiado de citas, consultas asistidas por IA, envío de ubicación y registro de datos en Google Sheets.

## Características

- Webhook de verificación y recepción de mensajes de WhatsApp.
- Menú inicial con opciones interactivas para agendar, consultar y pedir ubicación.
- Flujo de agendamiento paso a paso para capturar datos del cliente y su mascota.
- Respuestas asistidas por OpenAI para consultas libres.
- Envío de mensajes de texto, multimedia, contactos y ubicación.
- Persistencia de citas en Google Sheets.

## Estructura

- `src/app.js`: inicializa Express y monta las rutas del webhook.
- `src/routes/webhookRoutes.js`: define los endpoints `GET /webhook` y `POST /webhook`.
- `src/controllers/webhookController.js`: valida el webhook y procesa mensajes entrantes.
- `src/services/messageHandler.js`: contiene la lógica principal del bot y sus flujos.
- `src/services/whatsappService.js`: integración con la API de WhatsApp.
- `src/services/openAiService.js`: integración con OpenAI.
- `src/services/googleSheetsService.js`: guarda datos de citas en Google Sheets.
- `src/config/env.js`: carga la configuración desde variables de entorno.

## Requisitos

- Node.js 18 o superior.
- Una cuenta y credenciales válidas de WhatsApp Business Cloud API.
- Claves de OpenAI y acceso a Google Sheets si vas a usar los flujos completos.

## Instalación

1. Instala dependencias:

```bash
pnpm install
```

2. Crea tu archivo `.env` copiando la plantilla:

```bash
copy .env-example .env
```

3. Completa las variables de entorno necesarias.

## Variables de entorno

- `WEBHOOK_VERIFY_TOKEN`: token para verificar el webhook de WhatsApp.
- `API_TOKEN`: token de acceso para la API de WhatsApp.
- `PORT`: puerto donde corre el servidor.
- `BUSINESS_PHONE`: número de teléfono asociado al negocio.
- `API_VERSION`: versión de la API de WhatsApp.
- `CHATGPT_API_KEY`: clave de OpenAI.
- `BASE_URL`: URL base del servicio o API externa que uses.

## Ejecución

Modo desarrollo:

```bash
pnpm dev
```

Modo producción:

```bash
pnpm start
```

## Flujo general

1. WhatsApp llama al endpoint `GET /webhook` para verificar la suscripción.
2. Los mensajes entrantes llegan por `POST /webhook`.
3. El bot detecta saludos, opciones del menú o mensajes libres.
4. Según la intención del usuario, responde con texto, botones, ubicación, contacto o una respuesta generada por IA.
5. Cuando se completa una cita, los datos se guardan en Google Sheets.

## Notas

- El proyecto usa un archivo de credenciales local para Google Cloud en desarrollo.
- No subas secretos al repositorio; usa variables de entorno y archivos locales ignorados por Git.
