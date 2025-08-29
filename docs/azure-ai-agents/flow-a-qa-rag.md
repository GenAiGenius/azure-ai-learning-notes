# Flow A — Q&A + RAG (Fastest)

## Goal
Grounded answers from your knowledge base with citations.

## Sequence (high level)
Client → APIM → Agent → RAG tool → AI Search → OpenAI → Agent → APIM → Client

## What to build
- Vector index in Azure AI Search
- RAG tool function (query → retrieve top-k → return snippets + citations)
- Agent instruction block (require citations)

## Checklist
- [ ] Chunking & embeddings tuned
- [ ] Per-doc ACL filters
- [ ] “No result” fallback
