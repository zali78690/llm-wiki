# Semantic Router

**Type**: concept
**Related**: [[graph-rag-retrieval-pipeline]], [[semantic-cache]], [[knowledge-bundle]]
**ADRs**: ADR-100, ADR-302, ADR-409
**Last updated**: 2026-04-06

## Summary
Semantic Router (aurelio-labs) is a Python library that routes LLM requests to tools, agents, or pipelines using semantic similarity over pre-defined example utterances — bypassing slow LLM calls for intent classification. Routes are defined as sets of example phrases; incoming queries are embedded and matched via cosine similarity to the nearest route.

## Key Insights
- Intent routing without LLM inference: sub-millisecond decisions vs. 200–500ms LLM round-trips
- Routes carry example utterances; the router embeds them once and matches at query time — same principle as our semantic cache (0.95 cosine threshold)
- Supports multi-modal routing and dynamic routes with parameter extraction (a route can also run a lightweight LLM call for slot filling)
- Pluggable encoder backends (Cohere, OpenAI, HuggingFace, FastEmbed) and vector stores (Pinecone, Qdrant, local)
- Fully local operation possible — no external API dependency if using FastEmbed
- 3.4k stars, production-ready: 91 releases, 2,342 commits

## Relevance to This Project
Our child-model selection pipeline (ADR-100, ADR-409) routes queries to semantic child models using embedding similarity. Semantic Router formalises this pattern with: named routes, threshold control, multi-backend support, and dynamic parameter extraction that we currently do ad-hoc.

## Cross-References
- [[graph-rag-retrieval-pipeline]] — router is step 1 of the 4-stage pipeline; semantic-router formalises how that step works
- [[semantic-cache]] — both rely on cosine similarity thresholds; semantic-router adds multi-route branching beyond cache hit/miss
- [[knowledge-bundle]] — child model selection is effectively semantic routing over domain bundles
- [[dlthub-minimum-viable-context]] — intent-first thesis aligns with semantic-routing over example utterances
- [[agentic-mesh-blueprint]] — heavier governance alternative (OWL/SHACL) for multi-agent routing
