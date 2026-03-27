# Setup Guide — Tooth Care Bangkok Call Center Agent

This repo currently contains **docs + prompts** (no running code yet). Use this guide to deploy the agent in phases.

---

## Phase 1 (Today): Use as a manual agent
### What you do
1) Open `docs/agent-prompt.txt`
2) Copy everything
3) Paste it into your AI tool (ChatGPT / Assistant / your preferred platform) as the **system instructions** (or “agent instructions”).
4) Keep these docs open:
   - `docs/call-flows.md` (step-by-step process)
   - `docs/channel-templates.md` (messages to copy/paste)
5) When a customer asks to book:
   - Collect required fields (name, phone, service, etc.)
   - Manually add the appointment to Google Calendar using the event schema from `docs/google-calendar-integration.md`

### What to say for pricing
Use only: **5,000–10,000 THB** and “final price depends on dentist exam.”

---

## Phase 2 (Next): Decide escalation + staff notifications
Pick one:
- LINE group message to staff
- Email to front desk
- Slack/Teams message

Document your choice here once decided.

---

## Phase 3 (Build): Automation (recommended)
To build a real agent that books automatically, you will implement:
1) A webhook server for one channel (start with LINE or WhatsApp)
2) An LLM agent using the prompt in `docs/agent-prompt.txt`
3) Google Calendar integration:
   - free/busy lookup
   - create/update/delete events
   - 10-minute buffers
4) Logging + audit trail (important for medical scheduling)

### Data required as environment variables (examples)
- `TZ=Asia/Bangkok`
- `CLINIC_MAP_URL=https://maps.app.goo.gl/ySh5ARMpEKNfaUKP9`
- `GOOGLE_CALENDAR_ID=...`
- `GOOGLE_CLIENT_ID=...`
- `GOOGLE_CLIENT_SECRET=...`
- `GOOGLE_REFRESH_TOKEN=...` (or service account credentials)
- Channel credentials (LINE/WhatsApp/FB) depending on what you implement first

---

## Suggested next repo milestone
Create `/src` code to support ONE channel + Google Calendar.
Start with:
- LINE + Google Calendar
or
- WhatsApp + Google Calendar

(We will decide the stack: Node.js or Python.)
