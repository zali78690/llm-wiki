# Document Type Routing

**Type**: pattern
**Related**: [[chunking-strategies]], [[docling]], [[llamaindex]], [[paddleocr]], [[entity-extraction-resolution]]
**Last updated**: 2026-04-06

## Summary
Route different document types to different parsing and chunking strategies before ingestion into a knowledge pipeline. A PDF financial report, a scanned image, an API handbook, and a CSV each require different extraction approaches — applying one strategy to all degrades quality across the board.

## Routing Rules

| Doc type | Parser | Chunking strategy | Notes |
|----------|--------|------------------|-------|
| Structured PDF (tables, multi-column) | LlamaParse or [[docling]] | Segment-based (preserve table boundaries) | Docling preserves table structure as markdown |
| Scanned PDF / image | [[paddleocr]] → text → [[docling]] | Segment-based after OCR | OCR first, then treat as structured text |
| Narrative doc (handbook, policy) | [[docling]] | Segment-based with 1–2 sentence overlap | Preserve section/paragraph boundaries |
| Dense structured data (CSV, report) | pandas / direct parse | Summary indexing | LLM-generated summaries capture semantic intent better than raw rows |
| API documentation | [[llamaindex]] LlamaParse | Sub-chunk indexing | Fine-grained for precise method/endpoint retrieval |

## Key Insights
- **The routing decision happens before chunking**: parser choice determines what clean text you have; chunking strategy determines how that text is segmented. They are independent (see [[chunking-strategies]]).
- **Classify by content structure, not file extension**: a `.pdf` could be a scanned image, a structured report, or a narrative document. Use file size + page count + OCR confidence score to auto-classify.
- **Failure mode without routing**: applying segment-based chunking to a CSV produces meaningless fragments; applying summary indexing to an API doc loses precise method signatures.
- **For the [[entity-extraction-resolution]] pipeline**: the output of routing should be a list of `KnowledgeChunk` objects — routing normalises all doc types to the same schema before Stage 2 (Haiku extraction).

## Cross-References
- [[chunking-strategies]] — the strategy options available once doc type is classified
- [[docling]] — handles structured PDFs, DOCX, PPTX natively
- [[llamaindex]] — LlamaParse for complex multi-column PDFs; sub-chunk support built in
- [[paddleocr]] — for scanned documents before structured parsing
- [[entity-extraction-resolution]] — Stage 1 of this pipeline is where routing applies
