# HippoRAG — NeurIPS 2024

**Type**: source
**Source**: HippoRAG: Neurobiologically Inspired Long-Term Memory for Large Language Models (NeurIPS 2024)
**Related**: [[graph-rag-retrieval-pipeline]], [[knowledge-bundle]], [[hybridrag-2024]]
**Last updated**: 2026-04-06

## Summary
HippoRAG proposes using Personalized PageRank (PPR) over a knowledge graph for multi-hop retrieval in RAG systems, inspired by the hippocampal indexing theory of human memory. Named entities form graph nodes; co-occurrence and relations form edges. PPR from seed entities traverses the graph to find related entity clusters. Result: 20% better multi-hop recall than standard RAG, 10× cheaper than GraphRAG community summaries.

## Key Insights
- **PPR is the retrieval mechanism**: seed nodes are entities matched by embedding similarity to the query. PPR propagates relevance through the graph to surface connected entities the query didn't explicitly mention.
- **10× cheaper than GraphRAG community summaries**: GraphRAG (Microsoft) pre-computes community summaries at ingestion, which is expensive and doesn't generalise to new queries. HippoRAG's PPR computes traversal at query time — cheap (~10ms) and query-adaptive.
- **Why it works for multi-hop**: "overtime concentrated by crew type, broken down by region" — the query mentions crew and region; PPR surfaces cost_centre and overtime_policy without them being in the query string.
- **This project's application**: Stages 2–3 of [[graph-rag-retrieval-pipeline]] directly implement the HippoRAG pattern. Seed entities via cosine+BM25 (Stage 2), PPR traversal (Stage 3).

## Cross-References
- [[graph-rag-retrieval-pipeline]] — Stages 2–3 implement this paper's core pattern
- [[knowledge-bundle]] — the graph structure HippoRAG's PPR traverses
- [[hybridrag-2024]] — complementary paper on combining dense+sparse search with graph retrieval
- [[memorybear]] — full memory system using similar graph traversal for multi-hop retrieval
- [[vector-graph-rag-milvus]] — benchmark competitor (87.8% vs 87.1% avg Recall@5) without an explicit graph DB
