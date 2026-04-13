# QPaug: KPI-Grounded Question and Passage Augmentation

**Type**: source
**Source**: https://arxiv.org/abs/2406.14277
**Related**: [[doc2query-minus-filtering]], [[doc2query-plus-plus-coverage]], [[dbcopilot-schema-routing]]
**Last updated**: 2026-04-07

## Summary
QPaug (EMNLP 2024) augments both query and passage sides: it decomposes complex questions into sequential sub-questions for targeted retrieval, and synthesises passage-level context to address distractor passages. Structured decomposition rather than bulk paraphrase is the key insight — +34% on HotpotQA vs bulk paraphrase generation. Directly supports our decision (ADR-204) to use KPI-grounded decomposition for schema-side question expansion rather than generic paraphrase.

## Key Insights
- **Structured decomposition >> bulk paraphrase** — breaking a question into specific sub-questions yields +34% on HotpotQA vs generating many paraphrases of the same question
- Dual augmentation: query side (sub-questions for retrieval) + passage side (synthesised context) — both contribute
- Particularly strong on multi-hop QA where distractor passages are common; sub-questions filter to relevant passages early
- **KPI-grounded = structured** — our `expand_questions()` generates questions anchored to specific KPIs/metrics, which is exactly the structured decomposition QPaug validates
- The bulk-paraphrase baseline is a common naive approach; this paper provides the evidence it's inferior

## Cross-References
- [[doc2query-minus-filtering]] — filtering hallucinated bulk paraphrases; QPaug avoids the problem by using structure instead
- [[doc2query-plus-plus-coverage]] — coverage-aware build-time expansion; QPaug is the query-time structured equivalent
- [[dbcopilot-schema-routing]] — both use structured question generation to improve retrieval
