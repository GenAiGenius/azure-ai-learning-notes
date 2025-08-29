# Flow C — Action with Approval (Workflow)

## Goal
Human-in-the-loop for risky actions (DB access, credits).

## Sequence
Client → APIM → Agent → Business tool → Workflow (Logic Apps/Teams approval) → OpenAI (summary) → Agent → APIM → Client

## What to build
- Request tool (propose change, return request_id)
- Logic Apps approval flow (Teams card, Approve/Deny)
- Execute on approval, summarize back to user

## Checklist
- [ ] SLA for approvals/timeouts
- [ ] Full audit trail (who/when/what)
- [ ] Automatic expiry/revocation
