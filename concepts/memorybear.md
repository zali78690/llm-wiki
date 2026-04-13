# MemoryBear

**Type**: concept
**Related**: [[knowledge-bundle]], [[temporal-memory-rot]], [[vector-kg-combination]], [[hipporag-neurips-2024]]
**ADRs**: ADR-202, ADR-407
**Last updated**: 2026-04-06

## Summary
MemoryBear is an AI memory system providing graph-based persistent memory across agents and sessions. It uses Neo4j for interconnected knowledge storage, hybrid keyword+semantic retrieval, and a biologically-inspired forgetting engine (synaptic pruning / dynamic decay) to prevent memory bloat. Exposed as FastAPI services for multi-agent integration.

## Key Insights
- Graph storage (Neo4j) + hybrid search (keyword + semantic) is their core architecture — same direction as our KnowledgeBundle + hybrid retrieval
- Memory Forgetting Engine: uses dynamic decay rates to prune stale memories — operationalises the [[temporal-memory-rot]] concept we identified as a risk
- Self-Reflection Engine: periodically re-evaluates and consolidates memories — a form of knowledge compaction we don't have
- 75% accuracy on complex reasoning (claimed); outperforms Mem0 and Zep on benchmarks
- Requires PostgreSQL + Neo4j + Redis — heavy infrastructure vs. our in-memory + pickle approach (ADR-103)
- Multi-agent memory sharing is a key design goal — agents share a unified memory store vs. isolated context windows

## Relevance to This Project
Demonstrates a production memory architecture that combines exactly what our project uses (graph + hybrid retrieval) but with decay and consolidation layers we lack. The forgetting engine is the most novel piece — directly addresses [[temporal-memory-rot]] with a concrete implementation.

## Cross-References
- [[knowledge-bundle]] — similar goal (persistent business knowledge), but MemoryBear adds decay and multi-agent sharing
- [[temporal-memory-rot]] — MemoryBear's forgetting engine is a concrete implementation of decay-based memory management
- [[vector-kg-combination]] — same hybrid architecture (graph + dense vectors) in a memory system context
- [[hipporag-neurips-2024]] — both use graph traversal for multi-hop retrieval; MemoryBear is a full system, HippoRAG is an algorithm
- [[mempalace]] — opposite storage philosophy (verbatim + ChromaDB/SQLite vs summarised + Neo4j/Redis)
- [[anamnesis]] — adjacent memory system with 4D retrieval and authority-weighted banks
