# Azure AI Learning Notes — Build, Ship & Scale

Welcome! This site is a practical, hands-on guide to designing and delivering **Azure AI solutions**—from quick wins with prebuilt services to full production systems using **Agents, RAG, secure tool calling, and workflows**.

> **Audience:** AI engineers, cloud developers, solution architects, and anyone preparing for Azure AI roles (AI-102/DP-100).

---

## What you’ll learn here

- **Azure AI building blocks**  
  Azure AI Agents Service, Azure OpenAI, Azure AI Search (vector + hybrid), Document Intelligence, Vision, Language, Translator, Prompt Flow/Logic Apps, Functions/APIM, Key Vault, App Insights.

- **End-to-end patterns**  
  RAG grounding, function/tool calling, workflow/approvals, observability, content safety, cost/latency tuning, zero-downtime index updates, RBAC + OBO (on-behalf-of) authorization.

- **Production hardening**  
  Prompt & schema design, idempotent tools, retries, fallbacks, drift/quality checks, audit logging, and compliance-aware data flows.

---

## Trending AI topics covered (kept practical)

- **Agentic architectures**: planning, multi-tool orchestration, memory/state, human-in-the-loop.
- **RAG done right**: chunking, embeddings, vector + semantic hybrid search, grounding/citation policies.
- **Tool/Function calling**: JSON schemas, validation, idempotency, OBO flows via APIM, failure handling.
- **Multimodal**: using vision, speech, and text together in real scenarios.
- **Evaluation & safety**: groundedness checks, safe-completion, red-teaming basics, content filtering.
- **Latency & cost**: token budgets, streaming, caching, batch vs real-time, model tiering (e.g., 4o-mini → 4o).
- **Fine-tuning vs RAG**: when to fine-tune, when to engineer prompts + retrieval, and how to combine them.
- **Ops & governance**: monitoring, KPIs, access control, secrets, private networking, data residency.

> This site focuses on **how to apply** these trends in Azure—clear steps, code, and checklists instead of hype.

---

## Learning paths (pick one to start)

- **AI Engineer (most popular):** Agents + RAG + Tools → Workflows → Observability/Safety → Ship.  
- **Data/ML path:** Data prep → training in Azure ML → deploy endpoints → integrate with Agents/RAG.  
- **Architect path:** Landing zone, identity, network isolation, cost & SLA planning, multi-environment CI/CD.

---

## Hands-on projects you’ll build

1. **Pure Q&A with Grounding** (fastest)  
   Agent + RAG over Azure AI Search; citations, safe answers, P95 < 3s.

2. **Q&A + Business Action**  
   Grounded guidance plus a real action (e.g., create RMA/ticket) via a secured Function/APIM (OBO).

3. **Action with Approval (Workflow)**  
   Risky change (DB access/credit memo) routed to Logic Apps/Teams for approval, then executed and summarized.

Each project includes **prompts, schemas, code snippets, and an ops checklist**.

---

## How to use this site

- Browse from the left nav (Overview → Sequences → .NET quickstarts → Workflows).  
- Copy the code samples and adapt the names to your subscription (resource names, endpoints).  
- Use the **checklists** before you go live: identity, Key Vault, logging, rate limits, and fallbacks.

---

## Prerequisites

- Azure subscription + basic familiarity with resource groups, Entra ID, Key Vault, APIM.  
- Dev stack: **.NET** or Python (examples use both, choose what you like).  
- Basic understanding of HTTP/REST and JSON.

---

## Keep current

- I’ll add short “What’s new” summaries and refresh checklists as Azure AI evolves.  
- Each page aims to be **vendor-accurate** and **practical**—if something no longer works, open an issue/PR.

---

## Contribute / Request topics

Spotted a gap, typo, or want a new guide (e.g., “multilingual RAG” or “Doc Intelligence + RAG”)?  
Open an **Issue** or **Pull Request**—suggestions and examples are welcome!

---

_Last updated: {{ update-date }}_
