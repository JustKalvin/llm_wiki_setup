---
name: llm-wiki-add
description: >
  Save important content into the personal LLM wiki (second brain) at
  {your_llm_wiki_path}. Use ONLY when the user explicitly asks to
  save, add, or record something — "add this to wiki", "save to the wiki",
  "note this down", "ingest this", "remember this", "keep this" — whether
  the content is an article, URL, pasted text, a file, book/chapter, or the
  important points of the current conversation. Distill only what matters;
  never dump a whole chat. A bare URL or pasted file with no save instruction
  is NOT a trigger. Do NOT trigger on ordinary chat, code files being worked
  on, or when the user says "don't save".
---

# llm-wiki-add

Wiki root (hardcoded): `{your_llm_wiki_path}`

## First step, every time

Read `{your_llm_wiki_path}\AGENTS.md` (the schema) and
`{your_llm_wiki_path}\index.md`. Follow the **ingest** workflow in
AGENTS.md.

## Workflow

1. **Announce what will be saved** — 3-5 bullets of the points worth keeping
   and the pages that will be created or updated. The announcement is the
   confirmation; continue unless the user objects.
2. **Land the source** (if the content comes from a source): save it to
   `raw\YYYY-MM-DD-kebab-slug.md` (download its images into `raw\assets\`).
   `raw\` is immutable — add only, never edit or delete anything there.
3. **Distill, do not dump.** From a conversation, save only the durable
   claims, decisions, facts, and connections — not the back-and-forth.
4. **Write pages**: a source summary page in `wiki\`, plus new/updated
   entity and concept pages, with YAML frontmatter and reciprocal links.
   A single source usually touches 10-15 pages.
5. **Contradictions**: never silently overwrite — mark the old claim with
   its source and date ("As of 2026-03, X reported Y") and state which
   source supersedes it.
6. **Update `index.md`** and **append a `log.md` entry**
   (`## [YYYY-MM-DD] ingest | Title`).
7. **Lint-lite while touching pages**: fix broken links, missing frontmatter,
   and index drift on the pages you touch. A full pass is a separate request
   ("lint the wiki") — still handled by this skill.

## Edge cases — follow literally

- **Already in `raw\`** (same URL/filename) → do not duplicate; ask:
  skip or re-ingest.
- **Huge source** (whole book, full manual) → confirm scope first: chapter
  or whole thing.
- **Secrets/credentials in the content** → do not ingest; flag it to the
  user instead.
- **Ambiguous scope** ("save this" with a pile of files) → ask one short
  question instead of guessing.

## Rules

- Never save when the user said "don't save" — that overrides everything.
- If the session cwd is a different folder, still operate on the wiki by its
  absolute path above. Global config allows edits there; if a write is
  denied, report the permission error instead of writing elsewhere.