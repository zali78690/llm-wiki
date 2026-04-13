# Ingestion Queue

_Tracks sources pending ingestion. Updated by `/wiki-ingest` — mark `ingested | YYYY-MM-DD` when done._

| Source | Type | Notes | Status |
|--------|------|-------|--------|
| Knwler — auto knowledge graph creation | chat-notes | Tool for automated KG creation from text | ingested | 2026-04-06 |
| Chandra OCR 2 — images and PDF processing | chat-notes | OCR tool for extracting content from images/PDFs | ingested | 2026-04-06 |
| LlamaIndex — LiteParse and PaddleOCR | chat-notes | Document parsing pipeline using LlamaIndex | ingested | 2026-04-06 |
| Tony Seale — anchor knowledge graph in ROI/KPI | chat-notes | Approach for grounding KGs in business metrics | pending |
| Vectors.db or lightweight vendor-free embedding store | chat-notes | Evaluate options for embedding storage without vendor lock-in | ingested | 2026-04-06 |
| Combine vectors and KG (LinkedIn post) | url | https://www.linkedin.com/feed/update/urn:li:activity:7429898758274002944 | ingested | 2026-04-06 |
| Chunking Strategy (LinkedIn post) | url | https://www.linkedin.com/feed/update/urn:li:activity:7427379123209248768 | ingested | 2026-04-06 |
| Langextract and Docling | chat-notes | Document extraction libraries | ingested | 2026-04-06 |
| Different strategies for different doc types | chat-notes | Classification approach for document ingestion by type | ingested | 2026-04-06 |
| Temporal memory rot — knowledge decay handling | chat-notes | Concept: how to handle stale knowledge in a growing KB | ingested | 2026-04-06 |
| research_docs/2026-04-02-knowledge-layer-design.md | local-file | Applicable patterns: KnowledgeBundle, graph-RAG pipeline, entity extraction, semantic cache, research papers | ingested | 2026-04-06 |
| https://github.com/modelscope/sirchmunk | url | Embedding-free indexless search library | ingested | 2026-04-06 |
| https://github.com/Volland/ladybug-rag-rs | url | Rust hybrid Graph RAG engine with Louvain + RRF | ingested | 2026-04-06 |
| https://volodymyrpavlyshyn.substack.com/p/beyond-vector-search-building-a-hybrid | url | Companion article to ladybug-rag-rs (same author, folded into source page) | ingested | 2026-04-06 |
| https://github.com/aurelio-labs/semantic-router | url | Semantic routing library for LLM intent classification | ingested | 2026-04-06 |
| https://github.com/SuanmoSuanyangTechnology/MemoryBear | url | AI memory system with graph storage and decay engine | ingested | 2026-04-06 |
| https://github.com/rippletideco/rippletide | url | Agent governance starter kit with MCP context graph | ingested | 2026-04-06 |
| https://github.com/Hawksight-AI/semantica | url | Semantic layer framework with provenance and reasoning engines | ingested | 2026-04-06 |
| https://github.com/mallahyari/keplai | url | SDK-first RDF knowledge graph platform with NL-to-SPARQL | ingested | 2026-04-06 |
| https://arxiv.org/abs/2312.03463 | url | DBCopilot (EDBT 2025): reverse schema-to-question generation at build time | ingested | 2026-04-07 |
| https://arxiv.org/abs/2505.23039 | url | TailorSQL (VLDB 2025): workload-anchored offline doc augmentation for NL2SQL | ingested | 2026-04-07 |
| https://arxiv.org/abs/2510.14296 | url | Rethinking Schema Linking (2025): bidirectional retrieval + question decomposition | ingested | 2026-04-07 |
| https://arxiv.org/abs/2508.17590 | url | RubikSQL (2025): industrial NL2SQL with domain-anchored build-time augmentation | ingested | 2026-04-07 |
| https://arxiv.org/abs/2411.06102 | url | SiriusBI (VLDB 2025): Tencent BI with KG constraints preventing topic drift | ingested | 2026-04-07 |
| https://arxiv.org/abs/2301.03266 | url | Doc2Query-- (ECIR 2023): filtering hallucinated synthetic query expansions | ingested | 2026-04-07 |
| https://arxiv.org/abs/2510.09557 | url | Doc2Query++ (2025): coverage-aware expansion, recall plateau at ~100 queries | ingested | 2026-04-07 |
| https://arxiv.org/abs/2406.14277 | url | QPaug (EMNLP 2024): structured KPI-grounded decomposition for QA augmentation | ingested | 2026-04-07 |
| https://github.com/castorini/docTTTTTquery | url | docTTTTTquery: canonical build-time document expansion for BM25 recall | ingested | 2026-04-07 |
| https://dl.acm.org/doi/pdf/10.1145/3767695.3769489 | url | SIGMOD 2025: data-aware schema fingerprint enrichment with sample values/aliases | ingested | 2026-04-07 |
| https://platform.claude.com/cookbook/capabilities-knowledge-graph-guide | url | Anthropic cookbook: prompt-driven 4-stage KG construction with Claude | ingested | 2026-04-13 |
| https://dlthub.com/blog/minimum-viable-context | url | dltHub blog: minimum viable context for LLM data modeling; intent-first approach | ingested | 2026-04-13 |
| https://github.com/zilliztech/vector-graph-rag | url | Zilliz Vector Graph RAG: Milvus-only LightRAG, SOTA multi-hop QA Recall@5 87.8% | ingested | 2026-04-13 |
| https://github.com/raphaelmansuy/edgequake | url | EdgeQuake: Rust LightRAG with Postgres+AGE+pgvector, 6 query modes | ingested | 2026-04-13 |
| https://github.com/cloudbadal007/agentic-mesh-blueprint | url | Agentic Mesh Blueprint: MCP + OWL + SHACL for multi-agent semantic governance | ingested | 2026-04-13 |
| https://github.com/MemPalace/mempalace | url | MemPalace: local-first verbatim memory with palace hierarchy, 96.6% LongMemEval | ingested | 2026-04-13 |
| https://github.com/Canner/WrenAI | url | WrenAI: open-source NL→SQL BI agent with MDL semantic layer | ingested | 2026-04-13 |
| https://github.com/gayawellness/anamnesis | url | Anamnesis: 4D retrieval agent memory with authority-weighted banks and RRF | ingested | 2026-04-13 |
