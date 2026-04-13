# TailorSQL: Workload-Anchored NL2SQL Augmentation

**Type**: source
**Source**: https://arxiv.org/abs/2505.23039
**Related**: [[dbcopilot-schema-routing]], [[rubiksql-lifelong-nl2sql]], [[siriusbi-kg-constraints]]
**Last updated**: 2026-04-07

## Summary
TailorSQL (VLDB 2025) augments NL2SQL systems using historical query workloads as implicit domain knowledge at build time — capturing join patterns and column semantics not visible from schema alone. By performing offline documentation augmentation from past queries rather than relying solely on schema, it achieves 10-22% accuracy gains and up to 2× improvement on specialised benchmarks. The workload-anchoring differentiates it from schema-only approaches like DBCopilot.

## Key Insights
- **Past queries are a semantic goldmine** — historical SQL encodes implicit join paths, column usage patterns, and business logic not in schema comments
- Build-time augmentation: the offline enrichment step is a one-time cost, zero query-time overhead (same paradigm as our `expand_questions()`)
- 10-22% accuracy gain vs schema-only baselines; up to 2× on workload-aligned benchmarks
- **Latency also improves** — richer index reduces LLM inference needed at query time
- Key limitation: requires historical workload access; new deployments (cold-start) benefit less

## Cross-References
- [[dbcopilot-schema-routing]] — complementary: uses synthetic questions where TailorSQL uses real query history
- [[rubiksql-lifelong-nl2sql]] — RubikSQL extends this to continuous KB maintenance as workload evolves
- [[siriusbi-kg-constraints]] — both target enterprise/production NL2SQL; SiriusBI uses KG constraints, TailorSQL uses workload history
- [[wrenai]] — MDL captures workload-style semantics explicitly as a build-time semantic layer artifact
