# Google Calendar Integration Spec (Docs-only)

## Purpose
Automatically book, reschedule, and cancel appointments in Google Calendar for Tooth Care Bangkok.

## Timezone + hours
- Time zone: Asia/Bangkok
- Business hours: Mon–Sat 09:00–17:00
- Closed: Sunday
- Buffer: 10 minutes after each appointment block

## Appointment types + consult durations
- Implant: 60 min
- Aligner: 45 min
- Cosmetic: 30 min
- General/Unknown: 45 min
Block duration = consult duration + 10 minutes buffer.

## Immediate booking rule
If user wants “now/today”:
- Find earliest available slot that starts >= 30 minutes from current time AND ends by 17:00.
- If none today, propose next 3 available slots.

## Event schema
- Title: Tooth Care – {Service} – {Name}
- Location: https://maps.app.goo.gl/ySh5ARMpEKNfaUKP9
- Description fields:
  - Name
  - Phone
  - Channel
  - Language
  - Service
  - Concern
  - Pain score
  - Swelling/Fever/Trauma (yes/no + notes)
  - Notes

## Conflict handling
If the requested time overlaps any existing event:
- Propose the next 3 available times that fit the block duration and business hours.

## Cancel / reschedule
- Cancel: verify (name + phone) then delete the event.
- Reschedule: verify then move the event to new slot.

## Notes (implementation)
When you implement this in code later:
- Use Google Calendar Free/Busy or Events list queries within business hours.
- Enforce timezone handling explicitly.
- Ensure buffer is applied consistently (either by increasing event duration or by adding a separate buffer event).
