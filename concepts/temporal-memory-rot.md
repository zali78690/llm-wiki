# Temporal Memory Rot

**Type**: concept
**Related**: [[knowledge-bundle]]
**Last updated**: 2026-04-06

## Summary
Temporal memory rot describes how persistent knowledge bases degrade in accuracy over time as the world changes but stored facts don't. In a knowledge graph or wiki, a fact recorded about a tool, API, or business process becomes silently wrong when that thing changes. The risk compounds as the knowledge base grows — more facts, more decay surfaces.

## Key Insights
- Time-based expiry is a poor mechanism: facts don't rot uniformly by age — a core algorithmic insight from 2019 might still be valid, while an API endpoint from last week might be dead
- Contradiction detection (via wiki-lint) is more reliable than timestamp decay: if new information conflicts with old, that's the signal
- For [[knowledge-bundle]]: business facts (what a "crew" is) are stable; API endpoints and product features rot fast — track provenance so stale claims can be traced to source docs
- The right design: log `source_doc` and `ingestion_date` on every entity/chunk, surface conflicts on re-ingestion rather than on a timer

## Cross-References
- [[knowledge-bundle]] — provenance tracking (source_doc on every edge) is the mechanism that makes rot detectable
- [[memorybear]] — concrete implementation: forgetting engine with dynamic decay (synaptic pruning) addresses rot at system level
- [[mempalace]] — SQLite KG with relationship invalidation enables "what was true in January?" temporal queries
- [[anamnesis]] — bank-level decay policies as another concrete decay implementation
