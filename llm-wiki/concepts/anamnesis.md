# Anamnesis

**Type**: concept
**Related**: [[memorybear]], [[mempalace]], [[temporal-memory-rot]], [[reciprocal-rank-fusion]], [[rippletide]]
**ADRs**: ADR-202
**Last updated**: 2026-04-13

## Summary
Open-source persistent memory engine for AI agents using PostgreSQL + pgvector. 4-dimensional retrieval — semantic (30%), temporal (20%), relational (20%), strategic (30%) — fused via Reciprocal Rank Fusion. Memories live in isolated "banks" with mission statements, standing directives, and configurable decay. Weight system calibrates authority: explicit user memories start at 8.0 → 10.0, extracted at 2.0 → 6.0, inferred at 1.0 → 4.0.

## Key Insights
- **4D retrieval with explicit weights**: extends standard hybrid (semantic + relational) with *temporal* and *strategic* dimensions. Strategic weight is a first-class signal — an authority/validation-derived scalar, not an embedding. No other memory system in this wiki has an explicit strategic axis.
- **RRF fusion** across dimensions: same algorithm as [[reciprocal-rank-fusion]] / [[ladybug-rag-rs]]. Avoids score-normalisation issues when combining heterogeneous signals (cosine, recency, graph proximity, authority).
- **Authority-calibrated weight ceilings**: human-intent memories cap at 10.0; system-extracted at 6.0; inferred at 4.0. Prevents inferred memories from ever outranking explicit user directives — a safety invariant for persistent agent memory.
- **Reflect endpoint** synthesises ranked memories into directives via Claude — a reasoning layer on top of pure retrieval. Distinct from [[mempalace]]'s verbatim-return philosophy.
- **Postgres + pgvector single-store** — same architectural choice as [[edgequake]]. No Neo4j/Redis dependency.
- **Bank-scoped decay policies** + "reboot problem" framing: seed → configure boot → retain outcomes. Explicit workflow for agent memory lifecycle.
- **Small project** (15 stars, 11 commits) — early but the design choices are distinctive.

## Cross-References
- [[memorybear]] — different dimensional model (no explicit strategic axis) and different stack (Neo4j + Redis)
- [[mempalace]] — verbatim-return vs synthesised directives; opposite philosophies on retrieval output
- [[temporal-memory-rot]] — bank-level decay policies are a concrete implementation
- [[reciprocal-rank-fusion]] — Anamnesis uses RRF across its 4 retrieval dimensions
- [[rippletide]] — agent memory adjacent; Rippletide emphasises governance, Anamnesis emphasises weight calibration
