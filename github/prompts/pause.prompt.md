---
description: "Pause a project and save progress. Auto-extracts from chat or accepts inline notes. Usage: /pause {slug} or /pause {slug} — {notes}"
agent: 'pilot'
tools: ['editFiles']
---

Pause the specified project. Follow the /pause behavior defined in your agent instructions exactly.

If inline notes are provided, save directly without reading the chat.
If no notes, auto-extract from the conversation above, present summary for confirmation, then save.

Always update STATE.md, LOG.md, and INDEX.md before confirming.
