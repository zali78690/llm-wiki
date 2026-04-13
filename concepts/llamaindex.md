# LlamaIndex

**Type**: concept
**Related**: [[docling]], [[paddleocr]], [[chunking-strategies]]
**Last updated**: 2026-04-06

## Summary
LlamaIndex is a data framework for building LLM-powered applications over custom data. Relevant to this project for its document ingestion pipeline: LlamaParse handles structured extraction from complex PDFs (tables, multi-column layouts), and PaddleOCR integrates for image-heavy documents. Together they form a preprocessing layer that feeds clean text into knowledge graph pipelines.

## Key Insights
- LlamaParse produces structured markdown/JSON from PDFs — preserves table structure that naive text extraction destroys
- The indexing/retrieval separation (see [[chunking-strategies]]) is a first-class concept in LlamaIndex's architecture
- Lightweight alternative: combine LlamaParse for PDFs + PaddleOCR for scanned images, routing by doc type
- Relevant for [[entity-extraction-resolution]] pipeline's Stage 1 (chunking and doc preparation)

## Cross-References
- [[docling]] — IBM alternative for document parsing; compare before choosing
- [[paddleocr]] — OCR backend often used with LlamaIndex for image-heavy docs
- [[chunking-strategies]] — LlamaIndex's node parsing implements several of these strategies natively
- [[entity-extraction-resolution]] — LlamaIndex output feeds Stage 1 of this pipeline
