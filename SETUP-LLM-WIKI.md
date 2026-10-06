Apply this gist: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f

Wiki folder: C:\Users\kalvi\llm_wiki

This wiki folder contains a `setup\` folder with:

- setup\skills\llm-wiki-search\SKILL.md (search/answer-from-wiki skill)
- setup\skills\llm-wiki-add\SKILL.md (save-to-wiki skill)
- setup\opencode-patch.json (permission snippet to merge)

Do exactly this:

1. WIKI_PATH = the "Wiki folder" path above. Wherever the placeholder
   `C:\Users\kalvi\llm_wiki` appears (any slash direction), replace it with
   WIKI_PATH's user part as a real absolute path.

2. Copy, do not paraphrase — the files must stay byte-identical apart from
   the placeholder replacement:
   - setup\skills\llm-wiki-search -> ~/.config/opencode/skills/llm-wiki-search
   - setup\skills\llm-wiki-add -> ~/.config/opencode/skills/llm-wiki-add

3. Merge setup\opencode-patch.json into ~/.config/opencode/opencode.json
   (or .jsonc, whichever exists — prefer .jsonc if both exist):
   - deep-merge its `permission` block into the existing one, no duplicates
   - preserve every other existing field, keep `$schema`
   - if the file is missing, create it with `$schema` plus the patch
   - never overwrite or remove anything the user already had

4. Do NOT add anything to the `instructions` array. The wiki must stay
   passive: it is used only when the user invokes the two skills. Ordinary
   sessions must not change behavior.

5. If WIKI_PATH is missing AGENTS.md, index.md, log.md, raw\, or wiki\,
   build that scaffold from the gist (ingest/query/lint workflows in
   AGENTS.md). If everything already exists, leave it untouched.

Finish with:

- a reminder that opencode must be restarted to load the skills, and
- these tests to run from a DIFFERENT folder:
  1. "search the wiki for <topic>" -> answer cites wiki pages.
  2. Ask something not in the wiki -> agent says what is missing and
     browses the web instead.
  3. "add this to the wiki" with some content -> new entry in log.md.
  4. Ordinary session ("fix this file") -> NO wiki mention, NO log entry.
  5. Paste a bare URL, no instruction -> NO wiki action.

Rules:

- Do not rewrite the template files; they are versioned and tested as-is.
- Do not restart opencode yourself; the user will.
