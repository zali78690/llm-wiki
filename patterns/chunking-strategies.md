# Chunking Strategies

**Type**: pattern
**Source**: https://www.linkedin.com/feed/update/urn:li:activity:7427379123209248768
**Related**: [[entity-extraction-resolution]], [[llamaindex]], [[doc-type-routing]]
**Last updated**: 2026-04-06

## Summary
Indexing strategy and retrieval context are independent decisions — what you index doesn't have to be what you feed the LLM. Four main strategies vary in what gets embedded vs what gets returned at query time. Choosing the right strategy by document type significantly affects retrieval precision.

## The Four Strategies

| Strategy | What's indexed | What's retrieved | Best for |
|----------|---------------|-----------------|---------|
| **Chunk** | Full chunks | Same chunks | Simple homogeneous docs |
| **Sub-chunk** | Small sub-chunks | Full parent chunk | Long docs where precision matters |
| **Query** | Hypothetical questions the chunk answers | Full chunk | Reducing semantic gap between question and content |
| **Summary** | LLM-generated summaries | Full original chunk | Dense/structured data (CSVs, tables, reports) |

## Key Insights
- **Sub-chunk indexing**: index at fine granularity for accurate matching, retrieve at coarse granularity for complete context. Best for narrative documents where small phrases are the key retrieval signal.
- **Query indexing**: generates a set of hypothetical questions per chunk at ingestion time, embeds those instead of the raw text. Closes the semantic gap — query embedding vs question embedding is a more natural match than query embedding vs passage embedding.
- **Summary indexing**: particularly effective for structured data (financial reports, CSVs) where the raw chunk is dense but the summary captures the semantic intent cleanly.
- **Combine sub-chunk + summary for financial documents**: sub-chunk handles precise term matching; summary handles conceptual retrieval. Mentioned in community comments as a high-performing combination.
- **Used in this project**: Stage 1 of [[entity-extraction-resolution]] uses segment-based chunking (a form of chunk strategy). Query indexing could improve entity retrieval accuracy — worth evaluating if retrieval recall is insufficient.

## Cross-References
- [[entity-extraction-resolution]] — Stage 1 uses segment-based chunking; these strategies inform future improvements
- [[llamaindex]] — LlamaIndex's node parsers implement sub-chunk and summary strategies natively
