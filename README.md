# llm-wiki

Persistent knowledge base for this project. Captures concepts, tools, and patterns so they compound across conversations rather than being re-derived each time.

Inspired by [Karpathy's LLM wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

**Rule:** Before researching any concept, tool, or pattern — check `index.md` first.

---

## Structure

```
llm-wiki/
├── README.md       # this file
├── SCHEMA.md       # focus areas, what belongs, page template
├── index.md        # catalog of all pages (start here)
├── log.md          # append-only operations audit trail
├── queue.md        # ingestion pipeline tracker
├── raw/
│   ├── urls.txt    # URLs pending ingestion (clear after ingest)
│   └── pdfs/       # PDFs pending ingestion (deleted after)
├── sources/        # summaries of ingested external sources
├── concepts/       # technologies, tools, domain concepts
└── patterns/       # design patterns and strategies
```

**log.md vs queue.md:**
- `queue.md` tracks what raw sources are pending/done
- `log.md` is the full audit trail of every wiki operation (ingests, queries, lint results, conflict resolutions)

---

## Page format

All pages use kebab-case slug filenames (e.g. `concepts/bm25-retrieval.md`) and this structure:

```markdown
# [Title]

**Type**: concept | pattern | source
**Source**: [URL or filename]    ← sources/ only
**Related**: [[slug-1]], [[slug-2]]
**ADRs**: ADR-XXX                ← omit if no match
**Last updated**: YYYY-MM-DD

## Summary
One paragraph — what this is and why it matters to this project.

## Key Insights
- Non-obvious findings or implications
- What this changes or confirms about our approach

## Cross-References
- [[related-slug]] — reason for link
```

**ADRs field**: informational only — points to existing decisions that govern this space. Only present when the wiki page overlaps with an implemented or accepted ADR. Never updated from research alone; ADRs are updated when implementations change.

---

## Skills

| Skill | When to use | What it does |
|-------|-------------|--------------|
| `/wiki-ingest` | Adding a new source or chat notes | Checks schema scope → fetches → synthesises → creates page → scans for related ADRs → updates index, queue, log |
| `/wiki-query "question"` | Specific question you want answered from the wiki | Answers from wiki only, cites pages, offers to save new insights |
| `/wiki-update` | New info changes an existing page | Updates page, cascades cross-links, logs change |
| `/wiki-lint` | Periodic health check | Resolves conflicts, fixes orphans and missing links |
| `/wiki-synthesize` | No specific question — want the wiki to reason about itself | Gap analysis, cross-source comparison, domain briefings — saves output back as new pages |

### Ingestion sources
- **URLs**: add to `raw/urls.txt`, then run `/wiki-ingest` (clear urls.txt after)
- **PDFs**: drop into `raw/pdfs/`, then run `/wiki-ingest` (file deleted after)
- **Chat notes**: paste in chat and ask Claude to `/wiki-ingest` them

---

## Relationship to other docs

| Directory | Purpose |
|-----------|---------|
| `llm-wiki/` | Evergreen knowledge — concepts, tools, patterns |
| `adr_docs/` | Implementation decisions (what we chose and why) — updated when code changes |
| `research_docs/` | Legacy long-form design docs — do not add new files |
