# Doc2Query++: Coverage-Aware Document Expansion

**Type**: source
**Source**: https://arxiv.org/abs/2510.09557
**Related**: [[doc2query-minus-filtering]], [[doctttttquery-build-time-expansion]], [[qpaug-question-augmentation]], [[dbcopilot-schema-routing]]
**Last updated**: 2026-04-07

## Summary
Doc2Query++ (2025) solves the redundancy and hallucination problems of bulk query expansion by combining unsupervised topic modeling with hybrid keyword selection to guide LLM generation toward uncovered topics per document. Coverage-aware generation means 20-30 targeted queries outperform 100 unconstrained queries — recall plateaus past ~100. A Dual-Index Fusion approach keeps text and query signals separate for dense retrieval. Directly informs our optimal question count per table fingerprint.

## Key Insights
- **Recall plateau at ~100 queries/doc** — diminishing returns make bulk unconstrained generation wasteful; optimal is 20-30 coverage-aware queries
- Coverage-aware: topic modeling identifies what the document is about, keyword selection identifies what's *not yet covered*, then LLM fills gaps — prevents redundant question clusters
- Dual-Index Fusion: separate dense indices for original text and expanded queries, fused at retrieval time — avoids noise contamination
- Generalises to out-of-domain BEIR benchmarks, not just MS MARCO
- **For our pipeline**: 3-5 KPI-grounded questions per table (ADR-204) is well within the optimal range; more would add redundancy, not coverage

## Cross-References
- [[doc2query-minus-filtering]] — Doc2Query-- solves hallucination via filtering; Doc2Query++ solves it via coverage-aware generation
- [[doctttttquery-build-time-expansion]] — foundational build-time expansion that Doc2Query++ improves upon
- [[dbcopilot-schema-routing]] — both use build-time question generation; Doc2Query++ provides the optimal count guidance
- [[qpaug-question-augmentation]] — QPaug uses structured decomposition at query time; Doc2Query++ is the build-time complement
