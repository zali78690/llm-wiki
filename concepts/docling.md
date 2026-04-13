# Docling

**Type**: concept
**Related**: [[llamaindex]], [[langextract]], [[entity-extraction-resolution]]
**Last updated**: 2026-04-06

## Summary
Docling is IBM Research's open-source document parsing library. It converts PDFs, DOCX, PPTX, images and HTML into structured markdown or JSON while preserving layout: tables export as proper markdown tables, figures are identified, reading order is maintained across multi-column layouts. Strong alternative to LlamaParse for local/offline document processing with no API cost.

## Key Insights
- Fully local — no API calls, important for customer documents that can't leave the environment
- Table extraction is a standout feature: exports to markdown tables or pandas DataFrames directly
- OCR built in for scanned PDFs via Tesseract or EasyOCR backend (configurable)
- Output format is ready for chunking pipelines without post-processing
- Pairs well with the [[entity-extraction-resolution]] pipeline: Docling handles Stage 1 (doc prep), Haiku handles Stage 2 (extraction)

## Cross-References
- [[llamaindex]] — LlamaParse is the main alternative; LlamaParse has better multi-column PDF handling, Docling is better for offline/local use
- [[langextract]] — another extraction library; unclear differentiation, needs research
- [[entity-extraction-resolution]] — Docling output is the ideal input to Stage 1 of this pipeline
- [[edgequake]] — alternative vision-mode PDF path using GPT-4o/Claude/Gemini for scanned docs
