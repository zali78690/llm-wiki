# Vector Graph RAG (Zilliz / Milvus)

**Type**: concept
**Related**: [[hybridrag-2024]], [[ladybug-rag-rs]], [[hipporag-neurips-2024]], [[vector-kg-combination]], [[edgequake]]
**ADRs**: ADR-202, ADR-203
**Last updated**: 2026-04-13

## Summary
Zilliz/Milvus open-source implementation of Graph RAG that deliberately eliminates the graph database entirely — KG entities and relations are encoded as vectors in Milvus and retrieved via pure vector similarity. Reports SOTA Recall@5 on multi-hop QA benchmarks (MuSiQue 73.0, HotpotQA 96.3, 2WikiMultiHopQA 94.1, average 87.8%) — matching/exceeding HippoRAG 2 (87.1% avg).

## Key Insights
- **"Graph RAG with pure vector search — no graph database needed"** — contrasts sharply with [[ladybug-rag-rs]] (Apache AGE/graph DB) and [[memorybear]] (Neo4j). Operational simplicity at the cost of losing explicit traversal.
- **Single-pass reranking** — not iterative agent loops (e.g. IRCoT). LLM is called once to rerank retrieved triplet subgraphs. Lower latency, fewer LLM calls.
- **Indexing**: LLM-based triplet extraction → embed triplets → Milvus. Retrieval: entity extraction → vector search → subgraph expansion → LLM rerank.
- **SOTA vs HippoRAG 2**: 87.8% vs 87.1% avg Recall@5. The gap is small but demonstrates graph-database-free designs can match graph-traversal-based designs on standard benchmarks.
- **Stack**: Milvus (Lite for zero-config, Zilliz Cloud for managed), GPT-4o, text-embedding-3-large, React frontend, FastAPI backend.
- **Relevance to this project**: validates our use of Milvus-equivalent vector stores for KG-style retrieval. The "no graph DB" claim is worth scrutinising — we get the traversal signal via [[graph-rag-retrieval-pipeline]]'s explicit PageRank, which this system approximates via neighbour embedding similarity.

## Cross-References
- [[hybridrag-2024]] — another KG+vector hybrid; this one collapses the graph into the vector store
- [[ladybug-rag-rs]] — opposite design choice (explicit graph DB + PageRank + Louvain); good comparison point
- [[hipporag-neurips-2024]] — benchmark competitor (87.1% vs 87.8%)
- [[vector-kg-combination]] — general pattern this project is an extreme form of
- [[edgequake]] — also LightRAG-style but keeps an explicit graph (Apache AGE)
