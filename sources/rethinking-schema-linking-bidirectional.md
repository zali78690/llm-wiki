# Rethinking Schema Linking: Bidirectional Retrieval

**Type**: source
**Source**: https://arxiv.org/abs/2510.14296
**Related**: [[dbcopilot-schema-routing]], [[rubiksql-lifelong-nl2sql]], [[sigmod2025-data-aware-schema-matching]]
**Last updated**: 2026-04-07

## Summary
This EACL 2026 paper identifies false-positive table inclusion as the primary schema linking failure mode — retrieving too many tables hurts SQL generation more than missing tables. It proposes bidirectional retrieval (table-first + column-first) combined with question decomposition and keyword extraction, narrowing the gap between full-schema and oracle-schema SQL performance by 50% on BIRD and Spider. Critical for calibrating recall vs. precision trade-offs in our child selection pipeline.

## Key Insights
- **False positives are the #1 failure mode** — wrong tables in context cause SQL hallucination more than missing tables; prioritise precision over recall at the table level
- Bidirectional retrieval: table-first retrieval (which tables?) + column-first retrieval (which columns?) combined is strictly better than either alone
- Question decomposition for keyword extraction improves context matching for complex multi-hop questions
- 50% gap reduction between full-schema and oracle (perfect) schema SQL on BIRD and Spider — validates that schema linking quality directly gates SQL quality
- **SQL generation with good schema ≈ oracle performance** — the bottleneck is schema selection, not generation

## Cross-References
- [[dbcopilot-schema-routing]] — DBCopilot addresses the same table routing problem from a build-time angle
- [[rubiksql-lifelong-nl2sql]] — RubikSQL also addresses precision vs. recall in industrial NL2SQL
- [[sigmod2025-data-aware-schema-matching]] — data-aware schema enrichment directly addresses false-positive reduction
