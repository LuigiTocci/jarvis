# Jarvis — installazione (tutto da iPad)

## 1. App sulla Home
Carica su GitHub (stessa cartella): index.html, sw.js, manifest.json, icon-180.png, icon-192.png, icon-512.png.
Apri la pagina in Safari → Condividi → Aggiungi a Home. Si apre a schermo intero, avvio istantaneo.

## 2. Server (Cloudflare, gratis)
1. dash.cloudflare.com → Workers & Pages → Create → Worker → Deploy → Edit code → incolla worker.js → Deploy.
2. Storage & Databases → KV → Create namespace "jarvis". Nel Worker: Settings → Bindings → Add → KV namespace → nome variabile **KV**.
3. Settings → Variables and Secrets (tipo Secret):
   - JARVIS_TOKEN = una password lunga e casuale (24+ caratteri)
   - ALLOWED_ORIGIN = https://luigitocci.github.io   (senza / finale e senza percorso)
   - OPENAI_KEY = la tua chiave OpenAI
   - G_ID, G_SECRET, G_REFRESH = vedi punto 3
4. In Jarvis → Impostazioni: indirizzo del Worker (https://…workers.dev) e JARVIS_TOKEN → Salva.

## 3. Google (Gmail + Calendar con rinnovo automatico)
1. console.cloud.google.com: abilita Gmail API e Calendar API; crea ID client OAuth "Applicazione web" con URI di reindirizzamento https://developers.google.com/oauthplayground ; aggiungi il tuo account tra gli utenti di test. Sono G_ID e G_SECRET.
2. developers.google.com/oauthplayground → ingranaggio → "Use your own OAuth credentials" → inserisci G_ID/G_SECRET.
3. Scopes: gmail.readonly, gmail.compose, gmail.send, calendar.events → Authorize → Exchange authorization code → copia il **Refresh token** (= G_REFRESH).

## Sicurezza
- Il Worker risponde solo con il token giusto e solo alla tua origine. Email ed eventi partono solo dopo il tuo tocco su Conferma.
- Imposta un limite di spesa sulla chiave OpenAI. Se perdi l'iPad: cambia JARVIS_TOKEN e revoca l'accesso da myaccount.google.com/permissions.
- Per nascondere anche la pagina agli altri: Cloudflare Pages + Access.
