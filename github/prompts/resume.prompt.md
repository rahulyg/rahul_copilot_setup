---
description: "Resume a project. Loads context so Copilot knows where you left off. Usage: /resume {slug}"
agent: 'pilot'
tools: ['editFiles']
---

Resume the specified project. Follow the /resume behavior defined in your agent instructions exactly.

Read BRIEF.md and STATE.md (not LOG.md). Handle missing files, closed projects, and missing slugs as specified. End with "Ready to continue. What do you want to work on?"
