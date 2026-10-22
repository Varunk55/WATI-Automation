# ClinicReply bot

WhatsApp -> WATI webhook -> this server -> the AI (Gemini) -> reply via WATI.

## Run locally (test)
pip install -r requirements.txt
export $(cat .env | xargs)      # copy .env.example to .env and fill it
uvicorn main:app --port 8000
Expose it with a tunnel (e.g. `cloudflared tunnel --url http://localhost:8000`) to get a public URL.

## Deploy (free tier ok for demos)
Render.com -> New Web Service -> connect a GitHub repo with these files.
Build: pip install -r requirements.txt
Start: uvicorn main:app --host 0.0.0.0 --port $PORT
Add the env vars from .env.example in the dashboard.

## Connect WATI
WATI dashboard -> Webhooks -> Add Webhook
URL: https://YOUR-APP.onrender.com/webhook/<WEBHOOK_SECRET>
Event: Message Received (only). Do NOT enable "Session Message Sent" or the bot will see its own messages.
Get the API token from WATI -> API Docs / Settings. Disable WATI's own chatbot/AI agent on this number.

## Per clinic
Copy clinic.json, fill it in, deploy with CLINIC_FILE pointing to it (one deployment per clinic number).
