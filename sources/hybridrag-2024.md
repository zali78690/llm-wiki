# HybridRAG — arXiv 2024

**Type**: source
**Source**: HybridRAG: Integrating Knowledge Graphs and Vector Retrieval Augmented Generation for Efficient Information Extraction (arXiv 2408.04948)
**Related**: [[vector-kg-combination]], [[graph-rag-retrieval-pipeline]], [[knowledge-bundle]]
**Last updated**: 2026-04-06

## Summary
HybridRAG combines knowledge graph traversal with dense vector retrieval in a unified pipeline, achieving 2.8× accuracy improvement over vector-only RAG on complex information extraction tasks. The paper validates that graph and vector retrieval are complementary: graph handles relational/multi-hop questions, vector handles semantic similarity over unstructured text.

## Key Insights
- **2.8× accuracy over vector-only**: the combination isn't marginal — it's a substantial gain on the question types that matter most for this project (multi-entity, multi-hop business questions).
- **Complementary failure modes**: vector-only fails on multi-hop relational questions; graph-only fails on fuzzy semantic matching. Neither alone is sufficient for analytical business queries.
- **Unified pipeline justification**: the paper shows that combining the two in sequence (graph to narrow the search space, then vector search within that space) outperforms running them in parallel and fusing results.
- **Used in Stage 4**: the [[graph-rag-retrieval-pipeline]]'s constrained chunk search (Stage 4) implements this paper's core idea — use graph traversal to gate the vector search space.

## Cross-References
- [[vector-kg-combination]] — the general pattern this paper validates
- [[graph-rag-retrieval-pipeline]] — Stage 4 implements the constrained search from this paper
- [[hipporag-neurips-2024]] — complementary paper on graph traversal specifically via PageRank
- [[vector-graph-rag-milvus]] — opposite design: collapses the graph into the vector store entirely
