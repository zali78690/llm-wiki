# SIGMOD 2025: Data-Aware Schema Fingerprint Enrichment

**Type**: source
**Source**: https://dl.acm.org/doi/10.1145/3767695.3769489
**Related**: [[rethinking-schema-linking-bidirectional]], [[dbcopilot-schema-routing]]
**Last updated**: 2026-04-07

## Summary
This SIGMOD 2025 paper addresses cross-domain table recall by enriching schema fingerprints with sample values and column aliases beyond structural metadata. Data-aware matching — using actual data samples from the column alongside its name and description — substantially improves recall when user terminology doesn't match schema names (the core problem ADR-200 addresses). **Note**: ACM DL blocked automated access; summary derived from paper description.

## Key Insights
- **Sample values are the #1 fingerprint enrichment** — a column named "O_TOTALPRICE" with sample value "$1,250.00" embeds much closer to "revenue" than the name alone
- Column aliases (alternate business names) act as synonyms and directly bridge user vocabulary to schema vocabulary
- Cross-domain improvement: gains are largest when source and target schemas use different naming conventions — the exact scenario in multi-tenant analytics
- Validates ADR-200's "future: sample values per column (#1 accuracy booster)" — this paper provides the evidence for prioritising DB access to get sample values
- **TODO: needs full text** — ACM DL access blocked; fetch PDF via institutional access for specific recall numbers

## Cross-References
- [[rethinking-schema-linking-bidirectional]] — both address the false-positive/false-negative trade-off in schema selection
- [[dbcopilot-schema-routing]] — data-aware fingerprints directly improve the table routing quality DBCopilot depends on
