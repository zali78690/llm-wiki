# Graph-RAG Retrieval Pipeline

**Type**: pattern
**Related**: [[knowledge-bundle]], [[entity-extraction-resolution]], [[semantic-cache]], [[hipporag-neurips-2024]], [[hybridrag-2024]]
**ADRs**: ADR-101, ADR-102, ADR-202, ADR-203
**Last updated**: 2026-04-06

## Summary
A 4-stage deterministic retrieval pipeline that combines knowledge graph traversal with dense+sparse vector search to answer business questions. All LLM calls are offline (ingestion time); query-time retrieval is fully deterministic. Used in this project as the `precog_retrieve_context` MCP tool — runs ~35ms total.

## Stages

| Stage | Method | Latency | Purpose |
|-------|--------|---------|---------|
| 1. Router | Rule-based → MLP (Phase 2) | ~1ms | Classify: direct lookup / graph traverse / hybrid |
| 2. Entity Retrieval | cosine(query_emb, node_embs) + BM25 → Fusion MLP | ~5ms | Identify seed entities most relevant to the question |
| 3. PageRank Traversal | Personalized PageRank seeded by Stage 2 | ~10ms | Expand entity cluster via graph relationships |
| 4. Constrained Chunk Search | BM25 + dense, scoped to entity-linked passages only | ~15ms | Retrieve grounding passages within the entity cluster |

## Key Insights
- **Determinism by design**: the only probabilistic steps are at ingestion (Haiku/Sonnet extraction). All 4 retrieval stages are deterministic functions of fixed data.
- **Router saves latency**: simple definitional queries ("what is a crew?") skip Stage 3 (PageRank) entirely. Saves ~10ms and avoids graph noise for direct lookups.
- **Constrained search is the key move**: rather than searching all passages, Stage 4 scopes BM25+dense search to passages linked to the entity cluster found in Stage 3. Prevents irrelevant chunk retrieval.
- **Phase 1 compromise**: Router MLP uses rule-based heuristics until ~200 labelled examples are available. Fusion MLP uses fixed 0.7/0.3 weights. Both slots are reserved in the data structure.
- Backed by HippoRAG (NeurIPS 2024): PageRank traversal is 10× cheaper than GraphRAG community summaries with 20% better multi-hop recall.

## Cross-References
- [[knowledge-bundle]] — the data structure this pipeline queries
- [[entity-extraction-resolution]] — builds the graph and chunk index this pipeline depends on
- [[semantic-cache]] — sits in front of Stage 1 to short-circuit repeated questions
- [[hipporag-neurips-2024]] — research basis for Stages 2–3
- [[hybridrag-2024]] — research basis for combining dense+sparse in Stage 4
- [[louvain-community-detection]] — Louvain would add global query capability currently missing from this pipeline
- [[ladybug-rag-rs]] — Rust implementation that extends this pattern with Louvain + RRF
- [[semantic-router]] — formalises the Stage 1 routing step with multi-backend embedding and dynamic parameter extraction
- [[rippletide]] — MCP-based context graph as lightweight structured alternative to vector-first retrieval
- [[keplai]] — SPARQL query engine as alternative to PPR traversal for structured graph lookups
- [[edgequake]] — 6-query-mode superset of this pipeline (naive/local/global/hybrid/weighted/LLM-bypass) in production Rust
