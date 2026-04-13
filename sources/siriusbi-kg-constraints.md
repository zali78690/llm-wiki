# SiriusBI: KG-Constrained BI for Enterprise NL2SQL

**Type**: source
**Source**: https://arxiv.org/abs/2411.06102
**Related**: [[rubiksql-lifelong-nl2sql]], [[tailorsql-workload-augmentation]], [[rethinking-schema-linking-bidirectional]]
**Last updated**: 2026-04-07

## Summary
SiriusBI (VLDB 2025) is Tencent's production BI system serving dozens of enterprise clients across finance, advertising, and cloud. It prevents topic drift — queries wandering outside valid business concepts — using Schema/Metric/Domain KG constraints that bound generation to validated business entities. Achieves 89-97% SQL accuracy in production across domains. Multi-round dialogue with semantic completion handles ambiguous queries. Directly validates the use of KG structure to constrain NL2SQL generation scope.

## Key Insights
- **KG constraints prevent topic drift** — Schema/Metric/Domain KGs explicitly bound what tables/metrics/domains a query can touch; SQL generation is constrained, not free-form
- Three distinct KG layers: Schema KG (structural), Metric KG (business measures), Domain KG (concept taxonomy) — each prevents a different class of hallucination
- 89-97% production accuracy across diverse enterprise domains (finance, ads, cloud) — one of the highest reported for deployed BI systems
- Multi-round dialogue: semantic completion and clarification loops reduce the burden of precise user phrasing
- Two SQL generation modes: efficient fine-tuning for known domains + Semantic IR for cross-domain generalisation

## Cross-References
- [[rubiksql-lifelong-nl2sql]] — similar enterprise deployment focus; KB vs. KG constraint approach
- [[tailorsql-workload-augmentation]] — both target domain-specialised NL2SQL accuracy
- [[rethinking-schema-linking-bidirectional]] — KG constraints in SiriusBI implicitly address the false-positive problem via hard schema bounds
- [[wrenai]] — open-source analogue using MDL (semantic layer) instead of KG for the same topic-drift prevention thesis
