# Louvain Community Detection

**Type**: concept
**Related**: [[graph-rag-retrieval-pipeline]], [[vector-kg-combination]], [[ladybug-rag-rs]], [[knowledge-bundle]]
**Last updated**: 2026-04-06

## Summary
Louvain is a graph clustering algorithm that partitions nodes into communities by maximising modularity — the density of edges within communities vs between them. It requires no predefined number of clusters or categories: communities emerge from the graph structure itself. In knowledge graph RAG, it enables two capabilities our current pipeline lacks: scoped retrieval (restrict search to a topic community) and global synthesis (answer "what are the main themes?" questions).

## Key Insights
- **Emergent clustering**: no predefined topic taxonomy needed. Communities form from how entities actually co-occur and relate in your documents. Works especially well for domain-specific corpora where category labels aren't obvious upfront.
- **Enables global queries**: our current pipeline (PageRank traversal from seed entities) is fundamentally local — it expands from what the query mentions. Louvain makes global queries possible by identifying topic clusters independent of any specific query.
- **+195% on global questions** (from ladybug-rag-rs benchmarks): this is the most compelling number. "What are the main themes in our documentation?" is a query class our pipeline currently can't serve well.
- **Complementary to PageRank, not a replacement**: PageRank traversal (Stages 2–3 of our pipeline) handles local multi-hop reasoning. Louvain handles global structure. Use both.
- **Phase 2 candidate for KnowledgeBundle**: Louvain clustering could run at ingestion time on the assembled graph, storing community labels on each node. Adds a community-scoped retrieval mode to `precog_retrieve_context` with no query-time cost.
- **O(n log n) complexity**: fast enough for large graphs. Runs at ingestion time, not query time.

## Cross-References
- [[graph-rag-retrieval-pipeline]] — our pipeline is missing the global query capability Louvain enables
- [[knowledge-bundle]] — community labels from Louvain could be stored on graph nodes at ingestion time
- [[ladybug-rag-rs]] — uses Louvain alongside PageRank; +195% global question accuracy
- [[vector-kg-combination]] — Louvain adds a third retrieval signal alongside vector + graph traversal
