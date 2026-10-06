# LLM wiki before web search / fetch

You maintain a personal LLM wiki (second brain) at `{your_llm_wiki_path}`.

- Whenever you are about to use **web search or web fetch**, check the wiki
  first: read `{your_llm_wiki_path}\index.md`, and grep `wiki\` for pages
  relevant to the query.
- If the wiki already holds the needed answer or context, use it and cite
  the wiki page; skip the redundant web call.
- If the wiki has nothing, too little, or contradictory material, do the web
  search/fetch normally. In the answer, label clearly which parts came from
  the wiki and which came from the web.
- After a web search/fetch yields durable knowledge (an article, docs, facts
  worth keeping), offer once: "Save this to the wiki?" If the user agrees,
  load the `llm-wiki-add` skill. Never save without explicit consent.
- This rule only cares about web search/fetch moments. Do not mention the
  wiki in sessions that never go to the web.
- Escape hatches: if the user asks for a plain web search without consulting
  the wiki, just do it (they may say "search the web, don't use the wiki").
  If the user explicitly asks to search the wiki, use the `llm-wiki-search`
  skill.