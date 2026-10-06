---
name: llm-wiki-search
description: >
  Search the personal LLM wiki (second brain) at {your_llm_wiki_path}
  to answer a question. Use ONLY when the user explicitly asks to check the
  wiki / second brain first — "search the wiki", "wiki: X", "dari wiki",
  "cek wiki soal X", "what does my wiki say about X", "apa yang kita tahu
  soal X", "X vs Y dari wiki". If the wiki lacks the answer or its sources
  are insufficient, browse the web instead, then offer to file the result
  back with llm-wiki-add. Do NOT trigger for saving content, for ordinary
  questions the user never linked to the wiki, for coding tasks, or for
  files being actively worked on.
---

# llm-wiki-search

Wiki root (hardcoded): `{your_llm_wiki_path}`

## First step, every time

Read `{your_llm_wiki_path}\AGENTS.md` (the schema) and
`{your_llm_wiki_path}\index.md` (the catalog). Follow the **query**
workflow in AGENTS.md.

## Workflow

1. Pick the 2-10 relevant pages from `index.md`; read them (plus their direct
   links if needed). Grep across `wiki\` when the index is not enough.
2. **Answer with citations** — every factual claim names the wiki page, and
   where relevant the underlying source in `raw\`.
3. **If the wiki cannot answer** — nothing relevant, or sources too thin or
   contradictory — say exactly what is missing, then **browse the web** for
   the gap. Label clearly which parts came from the wiki and which came from
   the web.
4. **File valuable answers back**: if the answer is a comparison, analysis,
   or new connection worth keeping, stop and offer to save it via
   **llm-wiki-add**. Never save without being asked.

## Rules

- Never write to `raw\`. It is immutable.
- Never create or edit pages yourself — saving is **llm-wiki-add**'s job.
- If the session cwd is a different folder, still operate on the wiki by its
  absolute path above. Global config allows edits there; if a write is
  denied, report the permission error instead of writing elsewhere.