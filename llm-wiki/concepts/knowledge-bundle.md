# Knowledge Bundle

**Type**: concept
**Related**: [[graph-rag-retrieval-pipeline]], [[entity-extraction-resolution]], [[semantic-cache]]
**ADRs**: ADR-103, ADR-104
**Last updated**: 2026-04-06

## Summary
`KnowledgeBundle` is the project's business knowledge layer — a separate data structure from `ParentModelBundle` that holds a property graph of domain entities/relations plus a chunk index for passage retrieval. It grounds SQL generation in company-specific knowledge (what a "crew" is, how overtime is measured) that structural metadata alone can't provide.

## Key Insights
- Deliberately separate from `ParentModelBundle`: different data (business facts vs schema), different lifecycle (rebuild when docs change, not when schema changes)
- Phase 1 uses the same infrastructure patterns already in the project: NetworkX + numpy + pickle → S3
- All LLM calls happen at ingestion time only — query-time retrieval is fully deterministic
- MLP slots (fusion_mlp, router_mlp) are reserved but inactive in Phase 1; fixed weights (0.7/0.3) used until training data accumulates
- Phase 2 swaps NetworkX → Snowflake VECTOR tables without changing the MCP interface

## Structure
```
KnowledgeBundle
├── graph: nx.MultiDiGraph
│   ├── Node: {name, type, description, entity_emb[384d]}
│   └── Edge: {predicate, confidence, source_doc}
├── chunk_index: ChunkIndex
│   ├── chunk_embs: np.ndarray (N, 384)
│   ├── bm25_index: BM25Okapi
│   └── entity↔chunk mappings
├── fusion_mlp: None (Phase 1)
└── router_mlp: None (Phase 1)
```

## Cross-References
- [[graph-rag-retrieval-pipeline]] — the 4-stage pipeline that queries this bundle at runtime
- [[entity-extraction-resolution]] — the ingestion pipeline that builds this bundle
- [[semantic-cache]] — sits in front of the bundle's retrieval to avoid redundant queries
- [[semantic-router]] — child model selection over domain bundles is effectively semantic routing
- [[memorybear]] — alternative graph+vector memory architecture with decay and multi-agent sharing
- [[semantica]] — equivalent concept with reasoning engines and provenance; more complex but more explainable
- [[claude-knowledge-graph-cookbook]] — Anthropic's NetworkX MultiDiGraph matches this bundle's graph structure
- [[dlthub-minimum-viable-context]] — argues for narrower KPI-scoped bundles vs monolithic
