# llm-wiki Schema

## What This Is

A persistent knowledge base for the ai-ops project. Captures concepts, tools, patterns, and research findings so they compound across conversations rather than being re-derived each time.

**Rule**: Before researching any concept, tool, or pattern — check `index.md` first.

---

## Focus Areas

This knowledge base is scoped to:

1. **Knowledge graph construction and retrieval** — GraphRAG, HippoRAG, entity extraction, PageRank traversal, property graphs
2. **Document intelligence and ingestion pipelines** — OCR, PDF parsing, chunking strategies, doc-type routing
3. **Embedding strategies and vector search** — hybrid retrieval (dense + sparse), embedding models, vendor-free stores
4. **LLM orchestration patterns** — structured extraction, determinism, caching, MLP rerankers, multi-stage pipelines
5. **Semantic modelling for SQL/analytics** — child model selection, fingerprints, FK graph traversal, Cortex integration

When ingesting a new source, ask: does this fall within one of these areas? If not, it probably doesn't belong here.

---

## What Belongs Here

| Belongs | Does Not Belong |
|---------|----------------|
| Evergreen concepts and tools | Ephemeral task notes or todos |
| Research findings with lasting relevance | One-off debugging steps |
| Design patterns applicable to this project | Linear ticket summaries |
| Synthesised insights from external sources | Code snippets (use the codebase) |
| External papers, posts, docs worth keeping | Meeting notes |

---

## Organisation Rules

- `sources/` — summaries of external references (papers, blog posts, PDFs, LinkedIn posts)
- `concepts/` — technologies, tools, domain concepts
- `patterns/` — design patterns and implementation strategies
- All filenames are kebab-case slugs: `chunking-strategies.md`, not `Chunking Strategies.md`
- Every page starts with a one-paragraph Summary
- Related pages are linked using `[[slug]]` format — bidirectional

---

## Page Template

    # [Title]

    **Type**: concept | pattern | source
    **Source**: [URL or filename]    ← sources/ only
    **Related**: [[slug-1]], [[slug-2]]
    **ADRs**: ADR-XXX               ← omit if no match
    **Last updated**: YYYY-MM-DD

    ## Summary
    One paragraph.

    ## Key Insights
    - Non-obvious findings and implications

    ## Cross-References
    - [[slug]] — reason for link

---

## What Good Looks Like

- Pages are **concise and dense** — insight per line, not prose padding
- Every page answers: *why does this matter to this project?*
- Stubs are allowed (mark with **TODO: needs research**) — better a placeholder than a gap
- Cross-links are bidirectional — if A links to B, B links back to A
