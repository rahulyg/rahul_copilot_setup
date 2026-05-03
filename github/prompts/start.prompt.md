---
description: "Create a new project with context tracking. Usage: /start or /start {name} — {description}"
agent: 'pilot'
tools: ['editFiles', 'runTerminalCommand']
---

Create a new project. Follow the /start behavior defined in your agent instructions exactly.

Check for slug collisions before creating. If the user provides name and description inline, create everything without asking. Otherwise ask the minimum needed.
