# Flow B — Q&A + Business Action

## Goal
Combine grounded guidance with a real action (e.g., create ticket/RMA).

## Sequence
Client → APIM → Agent → RAG → Search → OpenAI (draft) → Business tool (OBO) → OpenAI (final) → Agent → APIM → Client

## What to build
- Business tool API/Function (idempotent, schema-validated)
- APIM policy with OBO (user-scoped token)
- Agent instruction to call the tool and summarize result

## Checklist
- [ ] Input validation & idempotency
- [ ] PII masking in logs
- [ ] Clear user receipts (IDs/links)
