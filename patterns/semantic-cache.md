# Semantic Cache

**Type**: pattern
**Related**: [[graph-rag-retrieval-pipeline]], [[knowledge-bundle]]
**ADRs**: ADR-102
**Last updated**: 2026-04-06

## Summary
Cache layer that short-circuits retrieval when an incoming question is semantically near-identical to a previously answered one. Uses cosine similarity between question embeddings at a high threshold (≥0.95) to return cached context rather than re-running the full retrieval pipeline.

## Key Insights
- **Threshold at 0.95+ is deliberate**: lower thresholds return wrong context for semantically adjacent but distinct questions (e.g. "crew overtime in Q1" vs "crew overtime in Q2"). High threshold keeps cache hits safe.
- **GPTCache (Nov 2024)**: 60–70% hit rate on repeated analytical questions at 0.95+ threshold. Most business analytics workloads are dominated by recurring question patterns.
- **In-memory LRU only**: keyed by `(workspace_id, question_emb)`. Not persisted — rebuilt from question log on restart. Keeps the design simple; persistence adds complexity for marginal gain.
- **Not a semantic search layer**: this cache does not rank or synthesise — it's a strict hit/miss gate. On miss, falls through to [[graph-rag-retrieval-pipeline]] Stage 1.
- **Where it sits**: between question arrival and `precog_retrieve_context`. Costs ~1ms to check; saves ~35ms on a hit.

## Cross-References
- [[graph-rag-retrieval-pipeline]] — what the cache bypasses on a hit
- [[knowledge-bundle]] — the retrieval target the cache protects
- [[semantic-router]] — extends cosine-similarity matching into multi-route intent classification; semantic-cache is a degenerate 2-route case (hit/miss)
