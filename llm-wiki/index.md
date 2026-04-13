# llm-wiki Index

_Catalog of all wiki pages. One-line summaries grouped by directory. Maintained by wiki-ingest and wiki-lint._

---

## Sources

_External sources ingested into the wiki (papers, blog posts, LinkedIn posts, PDFs)._

- [[dbcopilot-schema-routing]] — EDBT 2025: reverse schema-to-question generation at build time; +19.88% table routing recall for NL2SQL
- [[tailorsql-workload-augmentation]] — VLDB 2025: workload-anchored offline doc augmentation for NL2SQL; 10-22% accuracy gain vs baselines
- [[rethinking-schema-linking-bidirectional]] — EACL 2026: bidirectional retrieval + question decomposition; false-positive tables as primary failure mode
- [[rubiksql-lifelong-nl2sql]] — VLDB 2026: lifelong learning NL2SQL with domain-anchored build-time KB; SOTA on BIRD Mini-Dev
- [[siriusbi-kg-constraints]] — VLDB 2025: Tencent BI with Schema/Metric/Domain KG constraints; 89-97% production NL2SQL accuracy
- [[doc2query-minus-filtering]] — ECIR 2023: unfiltered synthetic query expansion causes hallucination; filtering improves NDCG@10 by 16%
- [[doc2query-plus-plus-coverage]] — 2025: recall plateaus past ~100 queries/doc; 20-30 coverage-aware queries beat unconstrained expansion
- [[qpaug-question-augmentation]] — EMNLP 2024: structured KPI-grounded decomposition +34% HotpotQA vs bulk paraphrase generation
- [[doctttttquery-build-time-expansion]] — canonical build-time document expansion for BM25; MRR@10 27.2 vs 18.6 baseline, 64ms latency
- [[sigmod2025-data-aware-schema-matching]] — SIGMOD 2025: schema fingerprint enrichment with sample values/aliases improves cross-domain table recall
- [[claude-knowledge-graph-cookbook]] — Anthropic cookbook: prompt-driven 4-stage KG construction with Claude + NetworkX; validates Haiku/Sonnet stratification
- [[dlthub-minimum-viable-context]] — dltHub blog: more context ≠ better prompt; intent-first beats 20-questions for LLM data modeling; metacognition gap
- [[hipporag-neurips-2024]] — NeurIPS 2024: Personalized PageRank over KG for multi-hop RAG; 20% better recall, 10× cheaper than GraphRAG
- [[autoschemakg-2025]] — arXiv 2025: auto schema induction for KG construction, 92% alignment with human schemas, UUID5 IDs
- [[hybridrag-2024]] — arXiv 2408.04948: combining KG traversal + dense vector search, 2.8× accuracy over vector-only
- [[maha-multimodal-kg]] — MAHA paper: multimodal RAG+KG with explicit relationship types (HAS-IMAGE etc.), 81% recall, Neo4j+MongoDB architecture
- [[ladybug-rag-rs]] — Rust hybrid Graph RAG engine: PageRank + Louvain + RRF fusion; +109% multi-hop, +195% global question accuracy

---

## Concepts

_Technologies, tools, and domain concepts relevant to this project._

- [[knowledge-bundle]] — core data structure: property graph + chunk index + MLP artifacts for business knowledge retrieval
- [[llamaindex]] — document intelligence framework; LlamaParse for PDF extraction, PaddleOCR integration
- [[docling]] — IBM document parsing library; structured extraction from PDFs/DOCX offline, strong table handling
- [[paddleocr]] — fast OCR library (PaddlePaddle); preferred for bulk scanned document processing
- [[temporal-memory-rot]] — concept: how persistent knowledge bases degrade silently; conflict detection > time-based expiry
- [[vendor-free-embedding-stores]] — embedding store options without cloud vendor lock-in; LanceDB, FAISS, numpy+pickle comparison
- [[knwler]] — STUB: tool for auto KG creation; candidate for entity extraction pipeline; needs research
- [[chandra-ocr]] — STUB: OCR tool for images/PDFs; compare vs PaddleOCR; needs research
- [[langextract]] — STUB: document extraction library; compare vs Docling/LlamaParse; needs research
- [[sirchmunk]] — embedding-free indexless search (ModelScope); no vector DB, keyword cascade + Monte Carlo sampling; contrast with our approach
- [[reciprocal-rank-fusion]] — RRF rank fusion algorithm; combines multiple ranked lists without score normalisation; alternative to our 0.7/0.3 weighted fusion
- [[louvain-community-detection]] — graph clustering for emergent topic communities; enables global queries missing from current pipeline
- [[semantic-router]] — intent routing via cosine similarity over example utterances; sub-ms decisions without LLM inference
- [[memorybear]] — graph+hybrid-search persistent memory system with biologically-inspired decay (Neo4j + FastAPI)
- [[rippletide]] — agent governance starter kit; MCP-based context graph for structured persistent memory
- [[semantica]] — semantic layer framework with reasoning engines, W3C provenance tracking, and conflict detection
- [[keplai]] — SDK-first RDF knowledge graph platform with NL-to-SPARQL and vector-based entity disambiguation
- [[vector-graph-rag-milvus]] — Zilliz/Milvus Graph RAG without a graph DB; SOTA Recall@5 87.8% avg (MuSiQue/HotpotQA/2WikiMultiHop)
- [[edgequake]] — Rust LightRAG framework (Postgres+AGE+pgvector); 6 query modes, ~3× better extraction, <200ms hybrid latency
- [[mempalace]] — local-first verbatim memory in ChromaDB+SQLite; 96.6% LongMemEval; palace hierarchy as retrieval signal
- [[wrenai]] — open-source generative BI agent (Canner); MDL semantic layer grounds NL→SQL across 12+ warehouses
- [[anamnesis]] — persistent agent memory with 4D retrieval (semantic/temporal/relational/strategic) + authority-weighted banks

---

## Patterns

_Design patterns and strategies captured from research and implementation experience._

- [[graph-rag-retrieval-pipeline]] — 4-stage deterministic pipeline: router → entity retrieval → PageRank → constrained chunk search (~35ms)
- [[entity-extraction-resolution]] — pipeline for building KG from docs: chunking → Haiku extract → Sonnet resolve → graph assembly
- [[semantic-cache]] — high-threshold (≥0.95 cosine) cache to short-circuit repeated retrieval queries; 60–70% hit rate
- [[chunking-strategies]] — 4 indexing strategies (chunk, sub-chunk, query, summary); indexing ≠ retrieval context
- [[vector-kg-combination]] — combining vector search + KG traversal as complementary layers; 2.8× accuracy gain
- [[doc-type-routing]] — route PDFs, scanned docs, CSVs to different parsers and chunking strategies before ingestion
- [[agentic-mesh-blueprint]] — MCP + OWL/SHACL + agent cards for multi-agent semantic governance; semantic contract ≠ retrieval
