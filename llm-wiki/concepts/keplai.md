# KeplAI

**Type**: concept
**Related**: [[entity-extraction-resolution]], [[graph-rag-retrieval-pipeline]], [[autoschemakg-2025]]
**ADRs**: ADR-203, ADR-412
**Last updated**: 2026-04-06

## Summary
KeplAI is an SDK-first knowledge graph platform built on Apache Jena Fuseki (RDF triplestore) with a Pythonic SDK abstracting raw SPARQL. Key capabilities: LLM-based entity extraction and disambiguation (Qdrant for vector-based disambiguation), NL-to-SPARQL query generation, multi-schema management with conflict detection, and Docker-containerised infrastructure provisioning. Backend is Python FastAPI + React/TypeScript frontend.

## Key Insights
- NL-to-SPARQL: converts natural language queries into SPARQL — directly analogous to our NL-to-SQL pipeline but for RDF knowledge graphs
- Qdrant for entity disambiguation: uses vector similarity to resolve which entity a mention refers to before inserting into the graph — prevents duplicate/fragmented nodes
- RDF/OWL standards compliance: triples are W3C-standard, enabling SPARQL federation across graphs and import/export with existing ontologies
- Multi-schema management with conflict detection: multiple graph schemas coexist; conflicts are detected at merge time — relevant to our multi-source build orchestration (ADR-421)
- SDK-first design: raw SPARQL is never exposed to callers; the Python SDK is the interface — good abstraction pattern
- LLM-based extraction + Qdrant disambiguation is a two-phase approach (extract then disambiguate) that's cleaner than our single-phase Haiku+Sonnet pattern

## Relevance to This Project
The entity disambiguation via vector search is the most actionable insight — our current extraction pipeline doesn't explicitly handle entity deduplication before graph insertion. The NL-to-SPARQL approach is directly analogous to our Cortex NL-to-SQL but for a different query language. Multi-schema conflict detection maps to our multi-source build challenges.

## Cross-References
- [[entity-extraction-resolution]] — KeplAI adds explicit vector-based entity disambiguation step before graph insertion; worth considering for our pipeline
- [[graph-rag-retrieval-pipeline]] — KeplAI's SPARQL query engine is an alternative to our PageRank-based traversal for structured graph queries
- [[autoschemakg-2025]] — both do automated entity extraction into typed graphs; KeplAI uses RDF standards, AutoSchemaKG uses property graphs
- [[agentic-mesh-blueprint]] — KeplAI's RDF substrate is a candidate ontology backend for the blueprint's OWL/SHACL contract
