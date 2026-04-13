# docTTTTTquery: Canonical Build-Time Document Expansion

**Type**: source
**Source**: https://github.com/castorini/docTTTTTquery
**Related**: [[doc2query-minus-filtering]], [[doc2query-plus-plus-coverage]], [[dbcopilot-schema-routing]]
**Last updated**: 2026-04-07

## Summary
docTTTTTquery (docT5query) trains T5 to predict queries a document could answer, then appends predictions to documents before BM25 indexing — zero per-query inference latency. Per-passage expansion achieves MRR@10 of 27.2 vs BM25 baseline of 18.6 (~46% relative gain) at 64ms latency (comparable to BM25, vs 3500ms for BM25+BERT reranking). The canonical reference for neural BM25 improvement via build-time expansion. MS MARCO baseline everyone compares against.

## Key Insights
- **Build-time = zero query-time cost** — all inference happens during indexing; retrieval is pure BM25 speed
- Per-passage expansion outperforms per-document: MAP 0.3182 vs 0.2310, Recall@1000 0.9490 vs 0.8856 — granularity matters
- MRR@10: 27.2 (expanded) vs 18.6 (BM25 baseline) — 46% relative gain from query predictions alone, no reranker
- 64ms latency matches BM25; vs 3500ms for BM25+BERT reranking — makes the case that build-time expansion is strictly preferable to query-time reranking when latency matters
- **The schema-side analogue**: our `expand_questions()` does the same thing — generates "queries" the table could answer and bakes them into fingerprints at build time

## Cross-References
- [[doc2query-minus-filtering]] — shows unfiltered expansion degrades quality; filtering what docTTTTTquery generates helps
- [[doc2query-plus-plus-coverage]] — improves on docTTTTTquery with coverage-aware generation to avoid redundancy
- [[dbcopilot-schema-routing]] — applies the same build-time expansion paradigm to NL2SQL table routing
