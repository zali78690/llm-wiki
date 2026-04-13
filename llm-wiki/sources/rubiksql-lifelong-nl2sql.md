# RubikSQL: Lifelong Learning NL2SQL with Knowledge Base

**Type**: source
**Source**: https://arxiv.org/abs/2508.17590
**Related**: [[tailorsql-workload-augmentation]], [[rethinking-schema-linking-bidirectional]], [[siriusbi-kg-constraints]]
**Last updated**: 2026-04-07

## Summary
RubikSQL (PVLDB Vol.19 / VLDB 2026) frames industrial NL2SQL as a lifelong learning task requiring continuous Knowledge Base (KB) maintenance. It builds a KB via database profiling, information extraction, rule mining, and CoT SQL profiling at build time, then uses a multi-agent workflow against this KB at query time. Achieves SOTA on KaggleDBQA and BIRD Mini-Dev. The "lifelong" framing — KB grows and improves with usage — is the key differentiator.

## Key Insights
- **KB as a living artifact** — unlike static schema augmentation (TailorSQL, DBCopilot), RubikSQL treats the KB as continuously maintained; new domain jargon and query patterns are fed back in
- Build-time: DB profiling + info extraction + rule mining + CoT SQL profiling; creates rich semantic representations before any user query
- Multi-agent query-time workflow: different agents handle disambiguation, KB lookup, and SQL generation
- **Domain-anchored augmentation** is the secret to SOTA on KaggleDBQA (domain-specific DBs with implicit business rules)
- Introduces RubikBench for more realistic industrial evaluation than BIRD/Spider

## Cross-References
- [[tailorsql-workload-augmentation]] — similar build-time enrichment but static; RubikSQL extends to continuous/lifelong
- [[rethinking-schema-linking-bidirectional]] — addresses same false-positive problem RubikSQL's KB lookup must handle
- [[siriusbi-kg-constraints]] — both deployed in enterprise/industrial settings; SiriusBI uses KG constraints, RubikSQL uses evolving KB
- [[wrenai]] — open-source NL→SQL with MDL semantic layer; shares the "anchor generation in explicit schema artifact" thesis
