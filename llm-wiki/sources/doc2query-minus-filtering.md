# Doc2Query--: Filtering Hallucinated Query Expansions

**Type**: source
**Source**: https://arxiv.org/abs/2301.03266
**Related**: [[doc2query-plus-plus-coverage]], [[doctttttquery-build-time-expansion]], [[qpaug-question-augmentation]]
**Last updated**: 2026-04-07

## Summary
Doc2Query-- (ECIR 2023) shows that seq2seq query expansion models hallucinate — generating queries that don't reflect document content, polluting the index with irrelevant signals. Filtering generated queries with a relevance model before indexing recovers quality: +16% NDCG@10, -23% query execution time, -33% index size. The key lesson for our pipeline: raw LLM-generated questions need quality filtering before being baked into fingerprints.

## Key Insights
- **Unfiltered expansion hurts retrieval** — hallucinated queries add noise that overwhelms the signal; "more is worse" without a filter
- Relevance filter: score each generated query against the source document; discard those below threshold — simple but effective
- +16% NDCG@10 after filtering (vs unfiltered baseline)
- Index size drops 33% — fewer but higher-quality queries means cheaper BM25 and vector stores
- -23% query execution time — smaller index = faster retrieval
- **Takeaway for our `expand_questions()`**: generated questions should be scored for relevance to the table fingerprint before being stored

## Cross-References
- [[doc2query-plus-plus-coverage]] — extends this with coverage-aware generation to avoid needing post-hoc filtering
- [[doctttttquery-build-time-expansion]] — canonical unfiltered build-time expansion; Doc2Query-- shows why filtering matters
- [[qpaug-question-augmentation]] — structured decomposition as an alternative to filtering bulk paraphrases
