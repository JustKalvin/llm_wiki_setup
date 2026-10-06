Apply this gist: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f

Wiki folder: {your_llm_wiki_path}        <-- change this line only

This wiki folder contains a `setup\` folder with:

- setup\skills\llm-wiki-search\SKILL.md (search/answer-from-wiki skill)
- setup\skills\llm-wiki-add\SKILL.md (save-to-wiki skill)
- setup\opencode-patch.json (permission snippet to merge)

Do exactly this:

1. WIKI_PATH = the "Wiki folder" path above (the full absolute path to the
   wiki, e.g. C:\Users\budi\llm_wiki).

2. Wherever the placeholder `{your_llm_wiki_path}` appears in the files
   below, replace it with WIKI_PATH. Keep the backslash style you find:
   a pattern like `{your_llm_wiki_path}\AGENTS.md` becomes
   `WIKI_PATH\AGENTS.md` (e.g. `C:\Users\budi\llm_wiki\AGENTS.md`).

3. Copy, do not paraphrase — the files must stay byte-identical apart from
   the placeholder replacement:
   - setup\skills\llm-wiki-search -> ~/.config/opencode/skills/llm-wiki-search
   - setup\skills\llm-wiki-add -> ~/.config/opencode/skills/llm-wiki-add

4. Merge setup\opencode-patch.json into ~/.config/opencode/opencode.json
   (or .jsonc, whichever exists — prefer .jsonc if both exist):
   - deep-merge its `permission` block into the existing one, no duplicates
   - the `~/llm_wiki` patterns are correct as-is (no replacement needed) as
     long as the wiki lives at ~\llm_wiki; if WIKI_PATH is somewhere else,
     remove those two `~/llm_wiki` entries instead of replacing them
   - in merged JSON, `{your_llm_wiki_path}` becomes WIKI_PATH, and inside
     JSON strings every backslash is doubled (C:\Users\budi\llm_wiki is
     written C:\\Users\\budi\\llm_wiki)
   - preserve every other existing field, keep `$schema`
   - if the file is missing, create it with `$schema` plus the patch
   - never overwrite or remove anything the user already had

5. Do NOT add anything to the `instructions` array. The wiki must stay
   passive: it is used only when the user invokes the two skills. Ordinary
   sessions must not change behavior.

6. If WIKI_PATH is missing AGENTS.md, index.md, log.md, raw\, or wiki\,
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