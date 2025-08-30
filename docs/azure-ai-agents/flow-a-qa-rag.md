# Flow A — Agentic AI  Q&A + RAG (Fastest)

## Goal
Grounded answers from your knowledge base with citations.

## Sequence (high level)
Client → APIM → Agent → RAG tool → AI Search → OpenAI → Agent → APIM → Client

<img width="2344" height="836" alt="image" src="https://github.com/user-attachments/assets/f70b2009-0889-40a8-911a-17bb6c473707" />



Scenario — Internal IT/HR policy Q&A

User ask: “What’s our corporate travel allowance for domestic flights?”

Step-by-step
      
      Client → APIM: Web portal sends { userId, message } + Entra token.
      
      APIM → Agent: APIM validates, forwards with x-correlation-id.
      
      Agent → RAG tool: Decides this is policy lookup; calls rag_query(query, roles=["Employee"]).
      
      RAG → AI Search: Vector+semantic search over “Employee Handbook” index; filter acl:Employee.
      
      AI Search → RAG: Returns top-k chunks + metadata {docId, section, snippet, url}.
      
      Agent → OpenAI: Builds grounded prompt with snippets and citation format.
      
      OpenAI → Agent: Produces concise answer with citations (no business actions).
      
      Agent → APIM → Client: Streams final text with links to sections.

**Example response to user**

            Domestic flights: Economy; cap $600 one-way; exceptions require manager approval.
            Sources: Travel Policy v3 (§2.1, §2.3).

**Why this flow?** Fast (<2–3s), no side effects, lowest risk.

**Watch**

    Index freshness when policies update.
    Hallucination control: require citations; if none, return “I didn’t find an authoritative source.”

## What to build
- Vector index in Azure AI Search
- RAG tool function (query → retrieve top-k → return snippets + citations)
- Agent instruction block (require citations)

## Checklist
- [ ] Chunking & embeddings tuned
- [ ] Per-doc ACL filters
- [ ] “No result” fallback


