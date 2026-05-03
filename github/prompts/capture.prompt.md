---
description: "Extract project context from the current chat. Creates or updates a project from the conversation. Usage: /capture or /capture {slug}"
agent: 'pilot'
tools: ['editFiles', 'runTerminalCommand']
---

Extract project context from this chat conversation. Follow the /capture behavior defined in your agent instructions exactly.

Read the entire conversation above. Extract objective, key files, data sources, decisions, completed work, pending work, and blockers. Create a new project or update an existing one based on whether the slug exists.
