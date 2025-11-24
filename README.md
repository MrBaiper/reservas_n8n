🎯 Objetivo de la Automatización

Este workflow actúa como un agente de reservas de restaurantes.
Su propósito es:
  1. Mostrar la lista de restaurantes obtenidos desde una API.
  2. Interpretar las solicitudes del usuario (restaurante, fecha, hora, personas y nombre).
  3. Validar y estructurar la información en un JSON con un formato exacto.
  4. Registrar automáticamente la reserva en Google Sheets.
  5. Responder de forma conversacional cuando falte información.

El agente utiliza un modelo LLM para comprender al usuario y generar el JSON requerido.

-------------------------------------------------------------------------------------------

🔐 Configuración de Credenciales

1. OpenAI / LLM Provider
   
En n8n:
  1. Ve a Credentials → OpenAI API.
  2. Crea credenciales con tu API Key, yo use Groq.
     API Key Usada (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)
  4. Asígnale un nombre (ej: OpenAi account 2).
  5. Base URL: https://api.groq.com/openai/v1
  6. Asegúrate que el nodo OpenAI Chat Model use dichas credenciales.
  7. Modelo usado: llama-3.3-70b-versatile


2. Google Sheets

El nodo POST Datos usa credenciales:
  - Tipo: Google Sheets OAuth2
  - Nombre en el workflow: Google Sheets account

Para configurarlo:
  1. Ir a Credentials en n8n.
  2. Seleccionar Google Sheets OAuth2.
  3. Autorizar con tu cuenta de Google.
  4. Dar acceso al documento de Google Sheets usado. 
    (https://docs.google.com/spreadsheets/d/1Ls9XMNW1yh-53kKD1dzErM10XR3AeP73GAlIamkhG3g/edit?usp=sharing)

---------------------------------------------------------------------------------------------


▶️ Cómo importar y ejecutar el Workflow

📥 1. Importar Workflow
  1. Abre n8n → Workflows
  2. Clic en Import
  3. Selecciona workflow.json

🛠️ 2. Asignar credenciales necesarias
Reemplaza en los nodos:
  - OpenAI Chat Model → tus credenciales de OpenAI
  - POST Datos → tus credenciales de Google Sheets

📝 3. Configurar Google Sheets
  En el workflow viene preset un documento con ID: 1Ls9XMNW1yh-53kKD1dzErM10XR3AeP73GAlIamkhG3g

▶️ 4. Probar el flujo
  - Ejecuta el Chat Trigger en modo test si estás en n8n Cloud.
  - Pregunta por restaurantes.
  - Envía los datos de una reserva completa.
  - Verifica la escritura en Google Sheets.


--------------------------------------

🧪 Cómo Probar Ejemplos

  🟢 Solicitar lista de restaurantes
    Muéstrame los restaurantes disponibles

  🟢 Crear reserva válida
    Quiero reservar en Pizzería Roma para el 25 de enero a las 7 pm para 2 personas a nombre de Ana López.

El agente debe responder solo un JSON, por ejemplo:
  {
    "valid": true,
    "restaurantName": "Pizzería Roma",
    "date": "25/01/2025",
    "time": "07:00 PM",
    "numberOfPeople": 2,
    "customerName": "Ana López",
    "message": "Reserva confirmada."
  }
El dato se registrará en Google Sheets.


