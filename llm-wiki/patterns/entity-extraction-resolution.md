# Entity Extraction and Resolution Pipeline

**Type**: pattern
**Related**: [[knowledge-bundle]], [[graph-rag-retrieval-pipeline]], [[autoschemakg-2025]], [[chunking-strategies]], [[docling]]
**ADRs**: ADR-200, ADR-205
**Last updated**: 2026-04-06

## Summary
A 5-stage pipeline for building a knowledge graph from raw documents. Haiku extracts entities and relations per chunk; Sonnet resolves surface-form variants to canonical names; NetworkX assembles the final graph. Key design principle: **no fixed schema** — entity types and predicates are auto-induced from the documents themselves.

## Stages

| Stage | Tool | Input → Output |
|-------|------|----------------|
| 1. Chunking | Segment-based splitter | Source doc → `KnowledgeChunk` list with UUID5 IDs |
| 2. Extraction | Haiku (Pydantic structured output) | Chunk → entities + relations |
| 3. Resolution | Sonnet | Surface variants → `alias_to_canonical` dict |
| 4. Graph Assembly | NetworkX MultiDiGraph | Canonical entities → graph nodes + edges |
| 5. Chunk Index | numpy + BM25Okapi | Chunks → dual embedding index |

## Key Insights
- **Auto schema induction**: entity types (`org_unit`, `metric`, etc.) and predicate labels (`BELONGS_TO`, `MEASURES`) are discovered by Haiku, not hardcoded. Sonnet normalises across variants. Based on AutoSchemaKG 2025 — 92% semantic alignment with zero manual ontology design.
- **UUID5 for chunk IDs**: `UUID5(source_doc + chunk_index)` — deterministic. Same document re-ingested produces the same IDs, preventing duplicates.
- **Segment-based chunking**: split on natural boundaries (section headers, paragraph breaks) with 1–2 sentence overlap. NOT character-count splitting — preserves semantic coherence.
- **Dual embeddings**: node embeddings (entity description) and chunk embeddings (passage text) are separate. Node embs power entity retrieval; chunk embs power passage search.
- **Single Haiku call per chunk** via Pydantic structured output — no multi-turn, no parsing.

## Cross-References
- [[knowledge-bundle]] — this pipeline builds the bundle
- [[graph-rag-retrieval-pipeline]] — queries the graph and chunk index produced here
- [[autoschemakg-2025]] — research basis for auto schema induction
- [[chunking-strategies]] — Stage 1 uses segment-based chunking; see this page for strategy tradeoffs
- [[docling]] — recommended document parser to run before Stage 1
- [[semantica]] — adds W3C PROV-O provenance and SHACL validation on top of the same extraction pattern
- [[keplai]] — adds vector-based entity disambiguation before graph insertion; worth adopting for dedup
- [[claude-knowledge-graph-cookbook]] — Anthropic's first-party reference for this exact Haiku+Sonnet extraction pattern
- [[edgequake]] — quantifies gleaning (+18% recall) and normalisation (36-40% dedup); production Rust implementation
