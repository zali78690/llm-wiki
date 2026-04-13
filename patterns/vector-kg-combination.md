# Combining Vectors and Knowledge Graphs

**Type**: pattern
**Source**: https://www.linkedin.com/feed/update/urn:li:activity:7429898758274002944
**Related**: [[graph-rag-retrieval-pipeline]], [[knowledge-bundle]], [[hybridrag-2024]], [[maha-multimodal-kg]]
**ADRs**: ADR-202, ADR-203
**Last updated**: 2026-04-06

## Summary
Using vectors and knowledge graphs as complementary retrieval layers — vectors for semantic similarity over unstructured text, graphs for explicit relationship traversal. Neither alone is sufficient: vector-only misses multi-hop relational reasoning; graph-only misses fuzzy/semantic matching. The combination (HybridRAG) achieves 2.8× accuracy over vector-only on complex questions.

## Architectural Approaches

| Architecture | Vector role | Graph role | Infrastructure |
|---|---|---|---|
| **Sequential** (this project) | Entity retrieval (Stage 2) | Relationship traversal (Stage 3) | NetworkX + numpy |
| **MAHA paper** | MongoDB for content vectors | Neo4j for relationship control plane | Separate stores per concern |
| **HybridRAG** | Dense passage retrieval | Entity-linked graph expansion | Unified index |

## Key Insights
- **Two stores, two roles (MAHA)**: Neo4j handles eligibility/relationships as a control plane; MongoDB handles vectors and content. Clean separation of concerns — graph DB doesn't need to store embeddings, vector DB doesn't need to reason about relationships.
- **Multimodal extension (MAHA)**: explicit relationship types for non-text content: `HAS-IMAGE`, `HAS-TABLE`, `HAS-FORMULA`, `NEXT-IMAGE`, `NEXT-TEXT`. 81% recall vs ~50% for competitors on multimodal benchmarks.
- **This project's approach**: sequential pipeline (graph traversal gates chunk search) is simpler than dual-store and runs on existing infrastructure. Switch to Neo4j+MongoDB only if the complexity of multimodal content demands it.
- **Critical insight**: the graph constrains the vector search space. Searching all passages is O(N); searching only passages linked to the entity cluster found via graph traversal is O(k) where k << N. This is why Stage 4 constrained search is the key performance win.

## Cross-References
- [[graph-rag-retrieval-pipeline]] — the project's implementation of this pattern
- [[knowledge-bundle]] — data structure that holds both the graph and the vector index
- [[hybridrag-2024]] — research backing: 2.8× accuracy over vector-only
- [[maha-multimodal-kg]] — MAHA paper: multimodal extension with explicit graph relationship types
- [[ladybug-rag-rs]] — Rust implementation with RRF fusion + Louvain; +195% global question accuracy
- [[reciprocal-rank-fusion]] — RRF is the fusion mechanism used in ladybug-rag-rs
- [[louvain-community-detection]] — Louvain adds global topic clustering layer missing from current pipeline
- [[memorybear]] — applies this pattern to persistent agent memory (Neo4j + hybrid search) with decay layer
- [[semantica]] — adds conflict detection and W3C provenance tracking on top of the vector+KG combination
- [[vector-graph-rag-milvus]] — extreme form of this pattern: graph exists only as vectors in Milvus
