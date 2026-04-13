# AutoSchemaKG — arXiv 2025

**Type**: source
**Source**: AutoSchemaKG: Autonomous Knowledge Graph Construction with Large Language Models (arXiv 2025)
**Related**: [[entity-extraction-resolution]], [[knowledge-bundle]]
**Last updated**: 2026-04-06

## Summary
AutoSchemaKG demonstrates that LLMs can automatically induce entity type schemas and predicate labels from text without any predefined ontology, achieving 92% semantic alignment with human-crafted schemas at 900M+ node scale. Key contributions: auto schema induction, UUID5 for deterministic chunk identity, and a two-stage extraction pipeline (extract then normalise).

## Key Insights
- **92% alignment with human schemas, zero manual design**: the paper validates that letting the LLM discover entity types (rather than fixing an enum upfront) produces schemas that human experts would have designed. This is the basis for the [[entity-extraction-resolution]] pattern in this project.
- **UUID5 deterministic IDs**: `UUID5(source + chunk_index)` ensures the same document re-ingested produces the same chunk IDs. Prevents duplicate nodes on re-ingestion — critical for incremental updates.
- **Scale proof**: tested at 900M nodes. The pattern holds at enterprise scale, not just toy datasets.
- **Two-stage validates the project's approach**: the paper uses extract-then-normalise (equivalent to Haiku extraction + Sonnet resolution in this project). Both stages are validated independently.

## Cross-References
- [[entity-extraction-resolution]] — Stage 2 (auto schema induction) and UUID5 ID scheme directly from this paper
- [[knowledge-bundle]] — the output data structure built using this paper's patterns
- [[semantica]] — also does entity extraction into typed graphs; uses RDF/OWL standards vs property graphs
- [[keplai]] — also does typed entity extraction; adds RDF standards and vector-based entity disambiguation
- [[claude-knowledge-graph-cookbook]] — Anthropic cookbook operationalises this paper's extract-then-normalise pattern
- [[dlthub-minimum-viable-context]] — complementary thesis: minimal input produces focused ontologies
