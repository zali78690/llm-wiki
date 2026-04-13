# DBCopilot: Schema Routing for Massive NL2SQL

**Type**: source
**Source**: https://arxiv.org/abs/2312.03463
**Related**: [[tailorsql-workload-augmentation]], [[rethinking-schema-linking-bidirectional]], [[rubiksql-lifelong-nl2sql]], [[doctttttquery-build-time-expansion]]
**Last updated**: 2026-04-07

## Summary
DBCopilot (EDBT 2025) decouples NL2SQL into schema routing (which DB/tables to query) and SQL generation, using a differentiable search index trained via reverse schema-to-question generation at build time. By auto-generating representative questions for each table at index time and learning to route NL questions to the right tables without manual annotation, it achieves +19.88% table routing recall over baselines. Directly validates the schema-side question expansion strategy in ADR-204.

## Key Insights
- **Build-time question generation is the core primitive** — tables are indexed with auto-generated questions they could answer, not raw column names; this is exactly what our `expand_questions()` pipeline does
- **No manual annotation required** — the reverse generation (schema→questions) is self-supervised; training signal comes from schema structure alone
- Relation-aware joint retrieval handles FK relationships during routing — table links matter, not just individual table embeddings
- Scalability claim: single differentiable index works across massive multi-database settings, not just single-schema

## Cross-References
- [[tailorsql-workload-augmentation]] — complementary: uses workload history instead of synthetic question generation
- [[rethinking-schema-linking-bidirectional]] — addresses the false-positive failure mode that schema routing must also handle
- [[doctttttquery-build-time-expansion]] — same build-time expansion paradigm applied to IR (BM25) rather than NL2SQL
- [[qpaug-question-augmentation]] — provides evidence for structured decomposition over bulk paraphrase at query time
- [[wrenai]] — MDL stores similar schema-side fragment metadata to support NL→SQL routing
