# PaddleOCR

**Type**: concept
**Related**: [[llamaindex]], [[docling]], [[chandra-ocr]]
**Last updated**: 2026-04-06

## Summary
PaddleOCR is a fast, lightweight OCR library from Baidu's PaddlePaddle framework. Supports 80+ languages, handles scene text (printed and handwritten), and is significantly faster than Tesseract for production workloads. Often used as the OCR backend in document intelligence pipelines when dealing with scanned PDFs or image-based documents.

## Key Insights
- Much faster than Tesseract at inference — relevant for bulk ingestion of customer document libraries
- PP-OCRv4 model (latest) achieves strong accuracy on both printed and handwritten text
- Integrates directly into LlamaIndex's document pipeline as an optional reader
- The layout analysis component (PaddleOCR's PP-Structure) handles tables and figures, not just text
- For scanned PDFs in the [[knowledge-bundle]] ingestion pipeline, this is the preferred OCR layer

## Cross-References
- [[llamaindex]] — primary integration point; LlamaIndex uses PaddleOCR as an optional reader
- [[docling]] — Docling uses Tesseract/EasyOCR by default; PaddleOCR is faster for bulk workloads
- [[chandra-ocr]] — another OCR option mentioned; needs research to compare
