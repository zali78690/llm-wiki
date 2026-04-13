# MAHA — Multimodal RAG with Knowledge Graphs

**Type**: source
**Source**: Shannon Lal (BCA Research) — LinkedIn post on MAHA paper, 2024/2025
**Related**: [[vector-kg-combination]], [[graph-rag-retrieval-pipeline]], [[paddleocr]]
**Last updated**: 2026-04-06

## Summary
MAHA extends knowledge graph RAG to multimodal documents (text, images, tables, equations) by encoding explicit graph relationship types for non-text content. Uses Neo4j as the graph control plane and MongoDB for vectors/content. Achieves 81% recall vs ~50% for competitors, 0.486 ROUGE-L vs 0.28–0.33, and 100% modality coverage.

## Key Insights
- **Explicit multimodal relationship types**: `HAS-IMAGE`, `HAS-TABLE`, `HAS-FORMULA`, `NEXT-IMAGE`, `NEXT-TEXT`. Rather than flattening all content to text chunks, the graph preserves modality-specific relationships and traversal paths.
- **Dual-store architecture**: Neo4j as the relationship/eligibility control plane; MongoDB for vector embeddings and content storage. Each store does what it's built for — no trying to make a graph DB do vector search.
- **100% modality coverage**: competing systems miss equations or certain image types. Explicit relationship types in the graph ensure every modality is queryable.
- **Relevance to this project**: if the [[knowledge-bundle]] ingestion pipeline needs to handle documents with tables, charts, or diagrams, MAHA's relationship-type approach is the model to follow. Currently out of scope (text-only docs) but worth tracking.
- **Community flag**: version control for revised docs and ontology-based parsing with confidence scoring were raised as open problems in comments — relevant to [[temporal-memory-rot]].

## Cross-References
- [[vector-kg-combination]] — MAHA is a multimodal implementation of this pattern
- [[graph-rag-retrieval-pipeline]] — MAHA's dual-store approach vs this project's single-store approach
- [[temporal-memory-rot]] — version control for revised docs is an open problem raised in MAHA comments
