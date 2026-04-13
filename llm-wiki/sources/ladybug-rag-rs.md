# ladybug-rag-rs — Hybrid Graph RAG Engine

**Type**: source
**Source**: https://github.com/Volland/ladybug-rag-rs + https://volodymyrpavlyshyn.substack.com/p/beyond-vector-search-building-a-hybrid
**Related**: [[vector-kg-combination]], [[graph-rag-retrieval-pipeline]], [[hipporag-neurips-2024]], [[hybridrag-2024]], [[reciprocal-rank-fusion]], [[louvain-community-detection]]
**Last updated**: 2026-04-06

## Summary
ladybug-rag-rs is a Rust implementation of a hybrid Graph RAG engine combining HNSW vector search with knowledge graph algorithms (PageRank, Louvain community detection, BFS traversal). Retrieval signals are fused via Reciprocal Rank Fusion (RRF). The Substack article by the same author (Volodymyr Pavlyshyn) is the companion explanation. Benchmarks on 500 technical documents: +21% context precision, +30% answer completeness, +109% multi-hop accuracy, +195% global question accuracy over vector-only.

## Key Insights
- **RRF fusion is the key move**: chunks appearing in both vector results AND graph results get a double boost. This rewards contextually important chunks that are also semantically similar — exactly the right signal.
- **Louvain community detection adds a layer our pipeline lacks**: instead of just traversing from seed entities (our PageRank approach), Louvain clusters the full graph into topic communities. Enables scoped retrieval (stay within a topic) AND global synthesis queries ("what are the main themes?").
- **+195% on global questions**: this is the result our current pipeline can't replicate — questions about the whole corpus. PageRank traversal is local; Louvain is global. This is the gap.
- **Three edge types**: MENTIONS, RELATES_TO, NEXT_CHUNK. The NEXT_CHUNK edge preserves document reading order in the graph — useful for sequential reasoning that pure embedding similarity destroys.
- **Explicit non-use cases**: corpora under 50 docs, direct factual lookups, sub-100ms latency requirements. Our project fits the use case (large corpora, multi-hop, latency budget ~35ms).
- **Rust + icebug (NetworKit fork)**: PageRank on 100K-node graphs in milliseconds. We use NetworkX (Python) which is fine at our current scale but would hit limits at 100K+ nodes.
- **LadybugDB**: embedded property graph DB unifying vectors + graphs in one store — interesting alternative to our separate numpy/NetworkX approach.

## Cross-References
- [[vector-kg-combination]] — ladybug-rag-rs is a full implementation of this pattern with RRF fusion
- [[graph-rag-retrieval-pipeline]] — our pipeline uses PageRank but not Louvain; +195% global accuracy is the gap
- [[hipporag-neurips-2024]] — also uses PageRank for traversal; ladybug-rag-rs adds Louvain on top
- [[hybridrag-2024]] — validates the hybrid approach; ladybug-rag-rs is a concrete Rust implementation
- [[reciprocal-rank-fusion]] — RRF is the fusion mechanism ladybug-rag-rs uses
- [[louvain-community-detection]] — the global clustering layer that enables "main themes" queries
- [[vector-graph-rag-milvus]] — competitor that drops the graph DB entirely; SOTA Recall@5 on multi-hop benchmarks
- [[edgequake]] — sister Rust Graph RAG with production scaffolding (multi-tenant, OpenAPI, SSE)
