# Agentic Mesh Blueprint

**Type**: pattern
**Related**: [[rippletide]], [[semantica]], [[keplai]], [[semantic-router]]
**Last updated**: 2026-04-13

## Summary
Reference blueprint for multi-agent semantic interoperability. Three-layer stack: (1) MCP tool server validates responses against ontology constraints before tool execution, (2) OWL ontologies define shared formal data models with SHACL enforcing validation rules, (3) agent cards annotate A2A payloads with ontology references and a mesh orchestrator routes + detects version/capability drift. Addresses semantic-drift hallucinations in enterprise multi-agent deployments (Copilot, Agentforce, Cortex, LangChain).

## Key Insights
- **Semantic governance ≠ retrieval**: this is orthogonal to RAG. The question is "do all agents understand what information *means*?" rather than "does the agent have the right information?".
- **SHACL over runtime contracts**: formal shape validation at the MCP layer catches incompatible payloads before tool execution. Stronger than Pydantic because it's shared across agent runtimes.
- **Agent cards = ontology-versioned capability manifests**: enables the mesh orchestrator to block incompatible agent pairs and handle version drift. Richer than static MCP tool lists.
- **Ontology as contract, not knowledge**: the OWL graph here is a type system, not a knowledge base. Inverts the usual KG framing.
- **Positioned against RAG-first architectures**: explicitly argues that more retrieval cannot fix semantic-vocabulary mismatch between agents.

## Relevance to This Project
Our Cortex/MCP surface (ADR-405 dynamic tool registration, ADR-302 multi-model routing) is a simpler form of this — single-tenant, single-ontology, no cross-agent contract. Worth keeping as a reference design if/when the Cortex integration needs to interoperate with external agents (Copilot, Agentforce) under a shared schema.

## Cross-References
- [[rippletide]] — also MCP-based agent governance, but context-graph style rather than OWL/SHACL
- [[semantica]] — semantic-layer framework; overlaps on shared-contract theme, different primitive (PROV-O)
- [[keplai]] — RDF KG platform with NL-to-SPARQL; closer to ontology substrate the blueprint assumes exists
- [[semantic-router]] — lightweight alternative for intra-agent routing without full OWL/SHACL governance
