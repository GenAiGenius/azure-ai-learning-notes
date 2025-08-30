# Flow B — Agentic AI Q&A + Business Action

## Goal
Combine grounded guidance with a real action (e.g., create ticket/RMA).

## Sequence
Client → APIM → Agent → RAG → Search → OpenAI (draft) → Business tool (OBO) → OpenAI (final) → Agent → APIM → Client

<img width="2155" height="768" alt="image" src="https://github.com/user-attachments/assets/c74c1482-1da2-45a3-9146-fdb6c6029d48" />

**Scenario — Returns & RMA creation (Retail/e-com)**


    User ask: “Can I return Order 81427? It arrived damaged.”
    
    Step-by-step
    1–5. Same as A: RAG finds Return Policy and Damage Window sections.
    6. OpenAI (draft): Drafts guidance: eligible if within 30 days, photos required.
    7. Agent → Business tool (OBO): Calls create_rma(order_id, reason, evidence) on a Function/API behind APIM using On-Behalf-Of so the user’s scopes apply.
    
    Request: {"order_id":"81427","reason":"damaged","evidence":["blob://…/photo1.jpg"]}
    
    Response: {"rma_id":"RMA-55913","return_label_url":"…","deadline":"2025-09-20"}
    
    OpenAI (final): Merges policy + tool output into a clear action plan with the RMA ID and label link.
    9–10. Return to client; telemetry written to App Insights; minimal audit to Cosmos/SQL.

**User sees**

    You’re eligible for a return under the Damaged-On-Arrival policy. I created RMA-55913.
    • Download label: …
    • Ship by: Sep 20
    Sources: Returns Policy (§1.2).

Why this flow? Grounded guidance + real action in one turn.

**Watch**

    Idempotency on create_rma (use request_id).
    OBO token exchange & per-tool scopes.
    PII masking in logs (names, addresses).

## What to build
- Business tool API/Function (idempotent, schema-validated)
- APIM policy with OBO (user-scoped token)
- Agent instruction to call the tool and summarize result

## Checklist
- [ ] Input validation & idempotency
- [ ] PII masking in logs
- [ ] Clear user receipts (IDs/links)
