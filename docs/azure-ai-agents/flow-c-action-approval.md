# Flow C — Agentic AI Action with Approval (Workflow)

## Goal
Human-in-the-loop for risky actions (DB access, credits).

## Sequence
Client → APIM → Agent → Business tool → Workflow (Logic Apps/Teams approval) → OpenAI (summary) → Agent → APIM → Client

<img width="2128" height="704" alt="image" src="https://github.com/user-attachments/assets/f03d9af1-9f2a-4d9d-be83-8ad2ec83a6f3" />

****Scenario — Temporary production DB read access (Internal IT)****

**User ask: “Grant me read-only access to ProdDB for 24 hours to investigate ticket #4321.”**

    Step-by-step
    1–2. Client → APIM → Agent (auth, correlation).
    3. Agent → Business tool: Calls request_db_access(user, db, scope="read", duration="24h", ticket="4321"). Returns {request_id, requested_scope, approver_group}.
    4. Agent → Workflow tool (Logic Apps): Starts an approval flow → posts an Adaptive Card to the on-call DBA Teams channel with buttons Approve/Deny, SLA timers, and context.
    5. Logic Apps → Business tool: On Approve, the tool executes the grant (e.g., adds an AAD role to the DB). Returns {granted:true, expires_at}. On Deny, returns {granted:false, reason}.
    6. Agent → OpenAI (summary): Generates a human-readable confirmation: who approved, scope, expiry, and how to revoke early.
    7–8. Back to client with the outcome; audit and traces captured.

**User sees**

    Access approved by DBA-OnCall for read-only on ProdDB until 2025-08-30 18:00 UTC.
    To revoke early, reply “revoke prod read”.
    Audit ID: REQ-7438.

**Why this flow? Requires human-in-the-loop for risky actions.**

**Watch**

    Long-running approvals: don’t block the HTTP response—return an operationId and send updates via notifications.
    Expiry automation (Logic App scheduled revocation).
    Full audit trail (who asked, who approved, when, scope).

## What to build
- Request tool (propose change, return request_id)
- Logic Apps approval flow (Teams card, Approve/Deny)
- Execute on approval, summarize back to user

## Checklist
- [ ] SLA for approvals/timeouts
- [ ] Full audit trail (who/when/what)
- [ ] Automatic expiry/revocation
