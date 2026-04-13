# Semantica

**Type**: concept
**Related**: [[entity-extraction-resolution]], [[knowledge-bundle]], [[vector-kg-combination]], [[autoschemakg-2025]]
**ADRs**: ADR-200, ADR-412
**Last updated**: 2026-04-06

## Summary
Semantica (Hawksight-AI) is a Python framework for building semantic layers and context graphs with explainability and provenance tracking. It combines NER/relation extraction (LLM-enhanced), multiple reasoning engines (forward chaining, Rete networks, SPARQL, deductive/abductive), and W3C PROV-O compliance for full decision audit trails. Integrates with LangChain, LlamaIndex, AutoGen, and 100+ LLM providers via LiteLLM.

## Key Insights
- W3C PROV-O provenance: every output is linked to its source entities and reasoning steps — addresses black-box criticism of LLM systems
- Conflict detection in vector stores: validates stored knowledge for consistency before retrieval — operationalises what our [[temporal-memory-rot]] concept describes as a risk
- Multiple reasoning engines in one framework: Rete networks (rule-based), SPARQL (graph query), deductive + abductive — allows switching reasoning strategy per query type
- 20+ specialised modules; supports AWS Neptune, Apache AGE, FalkorDB as graph backends
- SHACL validation for graph constraints — structural integrity checking on the KG, not just semantic
- NER + relation extraction pipeline with LLM enhancement mirrors our [[entity-extraction-resolution]] pattern

## Relevance to This Project
The provenance and conflict detection layers are the most differentiated pieces relative to our current pipeline. Our entity extraction produces a KG but doesn't track which chunk each relationship came from — Semantica's W3C PROV-O approach would add that. SHACL validation could enforce schema constraints post-extraction.

## Cross-References
- [[entity-extraction-resolution]] — Semantica's extraction pipeline is a superset with provenance; our pipeline is simpler and deterministic
- [[knowledge-bundle]] — Semantica's context graph is analogous to our KnowledgeBundle but with reasoning engines and provenance
- [[vector-kg-combination]] — Semantica supports both graph and vector retrieval as complementary layers
- [[autoschemakg-2025]] — Semantica does schema induction via NER; AutoSchemaKG does it via automated clustering
- [[agentic-mesh-blueprint]] — also semantic-contract focused; uses OWL/SHACL primitives instead of PROV-O
- [[mempalace]] — opposite philosophy: MemPalace stores verbatim, Semantica adds reasoning and provenance layers
- [[wrenai]] — concrete BI-focused semantic layer using MDL; Semantica is the framework Wren-style products could build on
