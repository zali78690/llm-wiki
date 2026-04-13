# Claude Knowledge Graph Cookbook — Anthropic

**Type**: source
**Source**: https://platform.claude.com/cookbook/capabilities-knowledge-graph-guide
**Related**: [[entity-extraction-resolution]], [[autoschemakg-2025]], [[knowledge-bundle]]
**Last updated**: 2026-04-13

## Summary
Anthropic's official cookbook for building knowledge graphs from unstructured text using Claude. Replaces traditional ML pipelines (trained NER, relation classifiers, string-similarity resolution) with a fully prompt-driven 4-stage flow: typed entity/relation extraction via `client.messages.parse()` + Pydantic → LLM-based entity resolution → NetworkX MultiDiGraph assembly → hub-node summarisation and subgraph-serialised multi-hop QA.

## Key Insights
- **Model stratification** mirrors our pipeline: Haiku for high-volume extraction, Sonnet for resolution and synthesis. Matches [[entity-extraction-resolution]] exactly.
- **Semantic entity resolution beats string similarity**: "Edwin Aldrin" ↔ "Buzz Aldrin" share zero characters but are unified via extraction-description context — syntactic similarity cannot catch this.
- **Grounded QA via subgraph serialisation**: multi-hop queries serialise the relevant subgraph as triples into the prompt. Produces traceable, edge-cited answers; ungrounded retrieval hallucinated facts ("Wapakoneta, Ohio").
- **F1 validation**: Apollo 11 raw F1=0.71 (P=1.00, R=0.55), Neil Armstrong raw F1=0.55 — precision is strong, recall is the weak link (same pattern flagged in [[rethinking-schema-linking-bidirectional]]).
- **Scaling tactics**: prompt caching, Batch API (50% cheaper), entity blocking before LLM arbitration, incremental resolution against existing canonicals, NetworkX ≤500K edges then Neo4j/Postgres.
- **First-party Anthropic source**: authoritative reference for prompt-driven KG construction on this project's stack.

## Cross-References
- [[entity-extraction-resolution]] — this project's pipeline is the same pattern; cookbook validates Haiku/Sonnet stratification
- [[autoschemakg-2025]] — academic counterpart for automatic schema induction
- [[knowledge-bundle]] — the property-graph structure the cookbook's MultiDiGraph resembles
