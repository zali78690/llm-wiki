# Reciprocal Rank Fusion (RRF)

**Type**: concept
**Related**: [[vector-kg-combination]], [[graph-rag-retrieval-pipeline]], [[ladybug-rag-rs]]
**ADRs**: ADR-202
**Last updated**: 2026-04-06

## Summary
RRF is a rank fusion algorithm that combines multiple ranked lists into a single ranking without requiring score normalisation. Each item is scored as the sum of `1 / (k + rank)` across all lists, where k is a constant (typically 60). Items appearing high in multiple lists score highest — making it ideal for fusing vector and graph retrieval results.

## Key Insights
- **No score normalisation needed**: vector similarity scores and graph-based scores live in different ranges. RRF works on ranks only, making it agnostic to the underlying scoring systems.
- **Double-appearing items win**: a chunk ranked 5th in vector results AND 5th in graph results scores far higher than a chunk ranked 1st in one list only. This is exactly the right behaviour for hybrid retrieval — items backed by both semantic similarity and structural connectivity are the most trustworthy.
- **k=60 is the standard default**: smooths the influence of top-ranked items. Lower k = more weight on top ranks. Empirically validated across many IR tasks.
- **Our current pipeline doesn't use RRF**: ADR-202 uses fixed 0.7/0.3 weighted fusion of normalised scores. RRF is a simpler, more principled alternative — no normalisation required, no weights to tune.
- **Worth evaluating as an alternative to weighted fusion**: if our 0.7/0.3 weights prove brittle on new domains, RRF is the natural upgrade path.

## Cross-References
- [[vector-kg-combination]] — RRF is the fusion mechanism for combining vector + graph retrieval
- [[graph-rag-retrieval-pipeline]] — Stage 4 currently uses weighted fusion; RRF is an alternative
- [[ladybug-rag-rs]] — uses RRF as its fusion mechanism with strong benchmark results
- [[anamnesis]] — uses RRF across 4 retrieval dimensions (semantic/temporal/relational/strategic)
