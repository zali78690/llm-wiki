# WrenAI

**Type**: concept
**Related**: [[siriusbi-kg-constraints]], [[rubiksql-lifelong-nl2sql]], [[dbcopilot-schema-routing]], [[tailorsql-workload-augmentation]], [[semantica]]
**ADRs**: ADR-204, ADR-411, ADR-414
**Last updated**: 2026-04-13

## Summary
Open-source generative BI agent (Canner, 14.9k stars) for NL→SQL with an explicit semantic layer. Three-tier stack: Next.js + GraphQL UI, Python/FastAPI AI service (intent classification + Qdrant RAG + LLM + correction loops), and a Rust + Apache DataFusion query engine (wren-engine) that resolves MDL (Modeling Definition Language) semantics before SQL reaches the database. Supports 12+ warehouses (PG, BigQuery, Snowflake, Redshift, Databricks, etc.).

## Key Insights
- **MDL is the whole point**: "the LLM doesn't guess what your metrics mean; the semantic layer tells it". Directly parallels our child-model/KPI pipeline (ADR-411) and [[siriusbi-kg-constraints]]'s Schema/Metric/Domain KG.
- **Rust query engine (wren-engine) on Apache DataFusion**: MDL resolution happens *before* SQL execution — analogous to our column-budget + Steiner-tree pre-resolution (ADR-203, ADR-413).
- **Correction loops, not single-shot**: iterative SQL refinement with error feedback. Matches ADR-401 (cortex feedback loop).
- **Qdrant-based RAG for schema/metric context**: vector retrieval of MDL fragments before prompt assembly. Functionally similar to our hybrid retrieval (ADR-202) over parent-bundle fingerprints.
- **Works with any LLM**: OpenAI, Claude, Gemini, Groq, DeepSeek, Azure, Vertex, Bedrock, Ollama. Frontier models recommended for accuracy.
- **No published accuracy metrics** on BIRD/Spider — unlike [[siriusbi-kg-constraints]] (89-97% production), [[rubiksql-lifelong-nl2sql]] (SOTA BIRD Mini-Dev), [[dbcopilot-schema-routing]] (+19.88% recall). Community traction (14.9k stars) is the main signal.

## Relevance to This Project
WrenAI = our architecture if open-sourced. MDL ≈ parent-model YAML + child fingerprints. wren-engine ≈ cortex runtime. Correction loop ≈ ADR-401. Worth watching as a reference for how to productise the child-model + semantic-grounding pattern for external users.

## Cross-References
- [[siriusbi-kg-constraints]] — shares the "metric layer prevents drift" thesis; SiriusBI uses KG, WrenAI uses MDL
- [[rubiksql-lifelong-nl2sql]] — both anchor NL2SQL in an explicit, evolvable schema artifact
- [[dbcopilot-schema-routing]] — schema-side question expansion; MDL stores similar fragment metadata
- [[tailorsql-workload-augmentation]] — offline workload augmentation pairs naturally with MDL
- [[semantica]] — semantic-layer framework; MDL is a concrete semantic layer with a BI focus
