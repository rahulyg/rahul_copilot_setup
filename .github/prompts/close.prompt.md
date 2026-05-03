---
description: "Mark a project as complete. Usage: /close {slug}"
agent: 'pilot'
tools: ['editFiles']
---

Close the specified project. Follow the /close behavior defined in your agent instructions exactly.

Check for pending items and warn if found. Update STATE.md, LOG.md, and INDEX.md. Never delete folders. Closed projects can be reopened with /resume.
