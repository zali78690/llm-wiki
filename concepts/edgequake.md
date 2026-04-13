# EdgeQuake

**Type**: concept
**Related**: [[ladybug-rag-rs]], [[vector-graph-rag-milvus]], [[graph-rag-retrieval-pipeline]], [[entity-extraction-resolution]], [[docling]]
**ADRs**: ADR-202, ADR-203
**Last updated**: 2026-04-13

## Summary
Rust-based Graph RAG framework implementing the LightRAG algorithm. Uses PostgreSQL with Apache AGE (graph ops) + pgvector (embeddings). Async-first Tokio architecture across 11 specialised crates. Claims ~3× better entity extraction, 5× faster hybrid query latency (<200ms), 2.4× faster document processing, and 10× more concurrent users vs traditional RAG.

## Key Insights
- **Same lane as [[ladybug-rag-rs]] (Rust + graph RAG)**: differentiating feature is LightRAG specifically, plus production scaffolding (auth, multi-tenant workspaces, OpenAPI, SSE streaming, K8s-ready). Rust performance advantages apply to both.
- **Postgres+AGE+pgvector single-datastore** — avoids [[memorybear]]-style heterogeneous infra (PG + Neo4j + Redis). Unified storage model simplifies ops.
- **Gleaning (second-pass extraction)** yields ~18% entity recall boost; normalisation reduces duplicates by 36-40%. Quantifies the benefit of the same two-stage pattern we use in [[entity-extraction-resolution]].
- **Six query modes**: naive vector, entity-local traversal, community-based global, hybrid local+global, weighted vector+graph mix, LLM-only bypass. Mirrors [[graph-rag-retrieval-pipeline]] plus a Louvain-style global mode.
- **Six domain presets** (General, Manufacturing, Healthcare, Legal, Research, Finance) + up to 50 custom entity types per workspace — configurable ontology without code changes.
- **Vision-mode PDF** support with GPT-4o / Claude / Gemini for scanned docs — overlaps with [[docling]] / [[paddleocr]] responsibilities.

## Relevance to This Project
Closest architectural match for what a production version of [[graph-rag-retrieval-pipeline]] could look like: same retrieval modes, same ontology-first extraction, packaged with the production concerns (multi-tenant, auth, streaming) we would need.

## Cross-References
- [[ladybug-rag-rs]] — sister Rust Graph RAG; different internals (Louvain + RRF), same language and perf goals
- [[vector-graph-rag-milvus]] — alternative LightRAG implementation that ditches the graph DB entirely
- [[graph-rag-retrieval-pipeline]] — EdgeQuake's six modes are a superset of our 4-stage pipeline
- [[entity-extraction-resolution]] — gleaning numbers (+18% recall) validate multi-pass extraction
- [[docling]] / [[paddleocr]] — EdgeQuake's vision-mode PDF overlaps this layer
