# MemPalace

**Type**: concept
**Related**: [[memorybear]], [[anamnesis]], [[temporal-memory-rot]], [[rippletide]], [[semantica]]
**ADRs**: ADR-103, ADR-407
**Last updated**: 2026-04-13

## Summary
Local-first AI memory system storing verbatim conversation text in ChromaDB (vectors) + SQLite (temporal KG). Organises memory via a "palace" metaphor (Wings → Rooms → Halls → Closets/Drawers → Tunnels). Claims 96.6% on LongMemEval benchmark with zero external API calls — positions itself as "store everything verbatim and make it findable" rather than "extract what matters".

## Key Insights
- **Verbatim storage over summarisation**: refuses the summarise-on-ingest design ([[memorybear]], Letta). Retrieval returns raw text, preserving nuance and reasoning. Cost model: ~$10/yr vs $507/yr for summarisation-based systems.
- **Hierarchical palace structure as retrieval signal**: +34% over flat semantic search (94.8% vs 60.9% on internal benchmarks). *Structure is retrieval*, not just organisation.
- **Layered context loading (L0-L3)**: identity always loaded (~50 tok), critical facts always loaded (~120 AAAK tok), room-specific on demand, deep semantic search explicit. Mirrors prompt-cache-aware patterns we use.
- **AAAK dialect honesty**: the abbreviation/compression scheme regresses performance (84.2% vs 96.6% raw) — project explicitly admits this. Rare transparency about a trade-off other memory systems hide.
- **Local-only**: no cloud, no external API. Heaviest contrast with [[anamnesis]] (PostgreSQL + optional Voyage/Claude) and [[memorybear]] (PG + Neo4j + Redis).
- **Temporal queries + relationship invalidation**: SQLite KG supports "what was true in January?" and updates when facts change — a concrete implementation of [[temporal-memory-rot]] beyond simple decay.

## Relevance to This Project
Validates verbatim-over-summarisation for knowledge retention. Our [[knowledge-bundle]] stores chunks (closer to verbatim) but summarises hub nodes — MemPalace suggests the hub summarisation may be lossy in ways we haven't measured. The palace hierarchy is also a candidate organising structure for the KnowledgeBundle if monolithic storage becomes a problem.

## Cross-References
- [[memorybear]] — closest peer (graph memory system) but uses summarisation + Neo4j + Redis stack
- [[anamnesis]] — also persistent agent memory; 4D retrieval vs palace-hierarchy retrieval
- [[temporal-memory-rot]] — MemPalace's SQLite KG with relationship invalidation is a concrete implementation
- [[rippletide]] — agent governance adjacent; different goal (governance vs retention)
- [[semantica]] — provenance angle is complementary; MemPalace doesn't track provenance explicitly
