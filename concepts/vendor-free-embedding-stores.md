# Vendor-Free Embedding Stores

**Type**: concept
**Related**: [[knowledge-bundle]], [[graph-rag-retrieval-pipeline]]
**ADRs**: ADR-103
**Last updated**: 2026-04-06

## Summary
Embedding stores that run without cloud vendor dependency — no Pinecone, Weaviate, or OpenSearch required. Critical for this project because customer environments may not allow outbound connections to managed vector DBs, and the existing pattern (numpy arrays serialised to pickle) is already vendor-free.

## Key Insights
- The project already uses the simplest form: `np.ndarray` in pickle files → S3. Works well for sub-100K vectors.
- **LanceDB**: columnar vector store, embedded (no server), Apache 2.0. Supports 1B+ vectors, fast ANN search, integrates directly with numpy/pandas. Best option if numpy+pickle becomes insufficient.
- **FAISS** (Meta): gold standard for pure ANN search, CPU and GPU variants. No persistence layer — must pair with a metadata store. Best for pure vector search without graph traversal.
- **ChromaDB**: embedded SQLite-backed vector store, simple API. Good for prototyping; less suited for the project's hybrid retrieval (BM25+dense) pattern.
- **Recommendation**: stay with numpy+pickle for Phase 1 (consistent with `ParentModelBundle`). Evaluate LanceDB if bundle size exceeds 500K vectors.

## Cross-References
- [[knowledge-bundle]] — currently uses numpy+pickle; this page covers upgrade options
- [[graph-rag-retrieval-pipeline]] — retrieval pipeline that queries the embedding store
