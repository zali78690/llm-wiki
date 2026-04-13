# Wiki Operations Log

_Append-only audit trail. Never edit or delete entries. All wiki operations are recorded here._

**Format:** `[YYYY-MM-DD] [OPERATION] [[slug]] — description`

**Operations:** `INGEST` | `UPDATE` | `LINT FIX` | `LINT CONFLICT`

---

[2026-04-06] INGEST [[knowledge-bundle]] — KnowledgeBundle concept from research_docs/2026-04-02-knowledge-layer-design.md: property graph + chunk index architecture for business knowledge
[2026-04-06] INGEST [[graph-rag-retrieval-pipeline]] — 4-stage deterministic retrieval pipeline from knowledge-layer-design.md, backed by HippoRAG + HybridRAG
[2026-04-06] INGEST [[entity-extraction-resolution]] — Haiku+Sonnet extraction pipeline from knowledge-layer-design.md, backed by AutoSchemaKG 2025
[2026-04-06] INGEST [[semantic-cache]] — GPTCache-inspired 0.95-threshold semantic cache pattern from knowledge-layer-design.md
[2026-04-06] INGEST [[hipporag-neurips-2024]] — NeurIPS 2024 paper: PersonalisedPageRank for KG-grounded RAG
[2026-04-06] INGEST [[autoschemakg-2025]] — arXiv 2025 paper: auto schema induction, UUID5 IDs
[2026-04-06] INGEST [[hybridrag-2024]] — arXiv 2408.04948: KG + dense vector combination, 2.8× accuracy
[2026-04-06] INGEST [[maha-multimodal-kg]] — MAHA paper via LinkedIn post: multimodal RAG+KG with explicit relationship types
[2026-04-06] INGEST [[chunking-strategies]] — LinkedIn post (Vivek Nityanand): 4 indexing strategies, indexing ≠ retrieval context
[2026-04-06] INGEST [[vector-kg-combination]] — LinkedIn post (Shannon Lal): combining vectors + KG, MAHA architecture, dual-store pattern
[2026-04-06] INGEST [[llamaindex]] — chat notes: LlamaIndex framework for document ingestion and LLM apps
[2026-04-06] INGEST [[docling]] — chat notes: IBM Docling document parsing library
[2026-04-06] INGEST [[paddleocr]] — chat notes: PaddleOCR fast OCR library
[2026-04-06] INGEST [[langextract]] — chat notes: STUB - document extraction library, needs research
[2026-04-06] INGEST [[knwler]] — chat notes: STUB - auto KG creation tool, needs research
[2026-04-06] INGEST [[chandra-ocr]] — chat notes: STUB - OCR tool for images/PDFs, needs research
[2026-04-06] INGEST [[vendor-free-embedding-stores]] — chat notes: embedding store options without cloud vendor dependency
[2026-04-06] INGEST [[temporal-memory-rot]] — chat notes: concept of knowledge decay in persistent KBs
[2026-04-06] INGEST [[doc-type-routing]] — chat notes: routing different doc types to different parsers and chunking strategies
[2026-04-06] INGEST [[sirchmunk]] — github.com/modelscope/sirchmunk: embedding-free indexless search, keyword cascade + Monte Carlo sampling
[2026-04-06] INGEST [[ladybug-rag-rs]] — github.com/Volland/ladybug-rag-rs + Substack article: Rust hybrid Graph RAG, PageRank + Louvain + RRF, +109% multi-hop +195% global accuracy
[2026-04-06] INGEST [[reciprocal-rank-fusion]] — derived from ladybug-rag-rs: RRF rank fusion as alternative to weighted score fusion
[2026-04-06] INGEST [[louvain-community-detection]] — derived from ladybug-rag-rs: Louvain clustering for global query capability
[2026-04-06] INGEST [[semantic-router]] — github.com/aurelio-labs/semantic-router: semantic intent routing via cosine similarity, sub-ms decisions without LLM inference
[2026-04-06] INGEST [[memorybear]] — github.com/SuanmoSuanyangTechnology/MemoryBear: graph+hybrid-search memory system with biologically-inspired decay engine
[2026-04-06] INGEST [[rippletide]] — github.com/rippletideco/rippletide: agent governance starter kit; MCP context graph for structured persistent memory
[2026-04-06] INGEST [[semantica]] — github.com/Hawksight-AI/semantica: semantic layer with W3C PROV-O provenance, reasoning engines, conflict detection
[2026-04-06] INGEST [[keplai]] — github.com/mallahyari/keplai: SDK-first RDF KG platform with NL-to-SPARQL and Qdrant entity disambiguation
[2026-04-07] INGEST [[dbcopilot-schema-routing]] — EDBT 2025: reverse schema-to-question build-time generation, +19.88% table routing recall
[2026-04-07] INGEST [[tailorsql-workload-augmentation]] — VLDB 2025: workload-anchored offline NL2SQL augmentation, 10-22% accuracy gain
[2026-04-07] INGEST [[rethinking-schema-linking-bidirectional]] — EACL 2026: bidirectional retrieval, false-positive tables as primary failure mode
[2026-04-07] INGEST [[rubiksql-lifelong-nl2sql]] — VLDB 2026: lifelong learning NL2SQL with evolving KB, SOTA on BIRD Mini-Dev
[2026-04-07] INGEST [[siriusbi-kg-constraints]] — VLDB 2025: Tencent BI KG constraints preventing topic drift, 89-97% production accuracy
[2026-04-07] INGEST [[doc2query-minus-filtering]] — ECIR 2023: filtering hallucinated query expansions, +16% NDCG@10 -33% index size
[2026-04-07] INGEST [[doc2query-plus-plus-coverage]] — 2025: coverage-aware expansion, recall plateau at ~100 queries, 20-30 optimal
[2026-04-07] INGEST [[qpaug-question-augmentation]] — EMNLP 2024: structured KPI-grounded decomposition +34% HotpotQA vs bulk paraphrase
[2026-04-07] INGEST [[doctttttquery-build-time-expansion]] — canonical build-time doc expansion for BM25, MRR@10 27.2 vs 18.6 baseline
[2026-04-07] INGEST [[sigmod2025-data-aware-schema-matching]] — SIGMOD 2025: sample values/aliases in schema fingerprints improve cross-domain recall
[2026-04-13] INGEST [[claude-knowledge-graph-cookbook]] — Anthropic cookbook: prompt-driven KG construction (Haiku extract + Sonnet resolve + NetworkX)
[2026-04-13] INGEST [[dlthub-minimum-viable-context]] — dltHub blog: intent-first beats 20-questions; metacognition gap in LLM data modeling
[2026-04-13] INGEST [[vector-graph-rag-milvus]] — github.com/zilliztech/vector-graph-rag: Graph RAG without a graph DB; 87.8% avg Recall@5 SOTA
[2026-04-13] INGEST [[edgequake]] — github.com/raphaelmansuy/edgequake: Rust LightRAG with PG+AGE+pgvector, 6 query modes
[2026-04-13] INGEST [[agentic-mesh-blueprint]] — github.com/cloudbadal007/agentic-mesh-blueprint: MCP + OWL + SHACL for multi-agent semantic governance
[2026-04-13] INGEST [[mempalace]] — github.com/MemPalace/mempalace: local-first verbatim memory, palace hierarchy, 96.6% LongMemEval
[2026-04-13] INGEST [[wrenai]] — github.com/Canner/WrenAI: open-source NL→SQL BI with MDL semantic layer and Rust query engine
[2026-04-13] INGEST [[anamnesis]] — github.com/gayawellness/anamnesis: 4D retrieval (semantic/temporal/relational/strategic) with RRF + authority weights
