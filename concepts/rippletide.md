# Rippletide

**Type**: concept
**Related**: [[graph-rag-retrieval-pipeline]]
**Last updated**: 2026-04-06

## Summary
Rippletide is a multi-language agent governance starter kit that adds a runtime authority layer over LLM agents. Its core components are: an Agent Evaluation CLI (TypeScript) for hallucination detection, a Context Graph MCP Server (Rust) providing persistent structured memory via Model Context Protocol, and coding agent hooks enforcing conventions at execution time.

## Key Insights
- Context Graph MCP Server (Rust): provides persistent memory to Claude Code and other MCP clients as a structured knowledge graph — not a vector store, but typed entities and relationships
- Hallucination reduction to <1% claimed — achieved by constraining agent actions through a validation layer, not by model fine-tuning
- Decision traceability: every agent action is logged with a decision chain, enabling audit and replay
- MCP protocol integration: memory is surfaced as MCP resources, making it composable with any MCP-compatible client
- Multi-language by design (TypeScript CLI + Rust MCP server) — reflects separating concerns: evaluation vs. runtime memory

## Relevance to This Project
Primarily interesting for the MCP-based context graph pattern — a lightweight alternative to a full Neo4j graph for providing structured memory to Claude Code sessions. The guardrails architecture is less directly applicable but the decision-audit pattern is worth noting for explainability requirements.

## Cross-References
- [[graph-rag-retrieval-pipeline]] — Rippletide's context graph is a structured alternative to our vector-first retrieval; the MCP interface makes it composable
- [[agentic-mesh-blueprint]] — heavier multi-agent governance (OWL + SHACL) vs Rippletide's lightweight MCP-context-graph approach
- [[mempalace]] — both retain context; Rippletide for governance/audit, MemPalace for verbatim retention
- [[anamnesis]] — adjacent agent-memory space; Anamnesis adds authority-weighted banks Rippletide lacks
