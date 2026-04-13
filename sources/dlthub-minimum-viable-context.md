# Minimum Viable Context — dltHub Blog

**Type**: source
**Source**: https://dlthub.com/blog/minimum-viable-context
**Related**: [[autoschemakg-2025]], [[semantic-router]], [[knowledge-bundle]]
**Last updated**: 2026-04-13

## Summary
dltHub blog post on LLM-driven canonical data modeling. Core claim: **more context is not a better prompt** — comprehensive business descriptions cause hallucinated irrelevant entities and departmentally-incoherent models. Compares three elicitation strategies (20-Questions, Business Scenarios, Intent-First) and concludes that the Intent-First approach (company name + brief description + single development goal) produces the most focused ontologies via LLM web-search bootstrapping.

## Key Insights
- **The metacognition gap**: LLMs cannot distinguish "this relationship exists in reality" from "this relationship serves my current goal". They follow every thread without self-limiting — the opposite of human modelers' instinctive scope control.
- **Departmental scoping is essential**: connections spanning marketing/sales/operations all exist but produce incoherent models when combined. SWVL example — mixing vehicle-capacity, driver-employment, route-ownership and payment-flows destroys usability.
- **Constrain the problem, not the context**: the actionable reframing of the entire post. Applies directly to child-model selection and MDL scoping.
- **Intent-First approach**: three inputs only — company, optional description, development goal. Model web-searches to bootstrap a scoped ontology. Minimises user burden AND output noise simultaneously.
- **20-Questions and Scenarios fail similarly**: dense context feeds "too much to work with and not enough direction" into downstream CDM steps, modeling irrelevant entities alongside legitimate ones.

## Relevance to This Project
Directly challenges the assumption that richer child-model inputs produce better selection. Validates our use of KPI-anchored scoping (ADR-411) — the KPI *is* the intent filter. Also suggests [[semantic-router]]-style intent classification at query time could replace part of the context we currently pass.

## Cross-References
- [[autoschemakg-2025]] — academic counterpart: auto schema induction with minimal input
- [[semantic-router]] — intent-first routing aligns with this post's thesis
- [[knowledge-bundle]] — departmental scoping argues for narrower bundles per KPI rather than monolithic
