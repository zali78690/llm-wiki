# Sirchmunk

**Type**: concept
**Related**: [[vendor-free-embedding-stores]], [[graph-rag-retrieval-pipeline]], [[vector-kg-combination]]
**Last updated**: 2026-04-06

## Summary
Sirchmunk (ModelScope) is an embedding-free, indexless search library that operates directly on raw files. Eliminates the vector DB entirely — no indexing step, no embedding approximation, no stale data. Uses a two-level keyword cascade, Monte Carlo Evidence Sampling, and ripgrep-all to search raw files, with DuckDB for knowledge persistence and SHA256 deterministic IDs.

## Key Insights
- **Direct challenge to the RAG paradigm**: no embeddings, no vector DB — queries raw files via keyword cascade + LLM rewriting. Trades semantic similarity for zero infrastructure and always-fresh data.
- **Three modes**: FAST (2 LLM calls, 2–5s), DEEP (Monte Carlo sampling, 10–30s), FILENAME_ONLY — the deep mode is the interesting one for complex queries.
- **Monte Carlo Evidence Sampling**: randomly samples context windows across the corpus to build evidence for a query — non-deterministic but thorough. Very different from our deterministic pipeline.
- **MCP server integration**: ships with an MCP server, making it easy to drop into any LLM assistant workflow.
- **When to consider this over our approach**: if the corpus is small, changes frequently, and semantic similarity is less important than keyword precision. Our project's KnowledgeBundle approach wins on semantic multi-hop reasoning; Sirchmunk wins on zero-infra freshness.
- **No formal benchmarks**: all claims are qualitative. Compare carefully before adopting.

## Cross-References
- [[vendor-free-embedding-stores]] — Sirchmunk is the extreme end of vendor-free: no embeddings at all
- [[graph-rag-retrieval-pipeline]] — our approach; contrast with Sirchmunk's embedding-free design
- [[vector-kg-combination]] — Sirchmunk rejects both sides of this combination
