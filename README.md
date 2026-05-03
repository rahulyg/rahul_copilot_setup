# Project Pilot

A lightweight project context system for VS Code + GitHub Copilot. Track multiple projects and switch between them without losing state — Copilot reads your context files and picks up where you left off.

No git required. No npm. No external dependencies. Just Markdown files on disk.

## Problem

Copilot Chat has no memory between sessions. When you switch projects or close a chat, all context is lost. You re-explain what you're working on, which files matter, and where you left off — every single time.

## Solution

Project Pilot stores project context as Markdown files in a `.context/` folder. When you resume a project, Copilot reads those files and instantly knows the objective, key files, current status, and what's next.

## Setup

### Option A: Clone (if Git is available)

```
VS Code → Ctrl+Shift+P → "Git: Clone" → paste this repo URL
```

Then copy to your workspace:

```powershell
# Windows
Copy-Item -Recurse rahul_copilot_setup\.github  YOUR_WORKSPACE\.github
Copy-Item -Recurse rahul_copilot_setup\.vscode  YOUR_WORKSPACE\.vscode
```

```bash
# Mac/Linux
cp -r rahul_copilot_setup/.github  YOUR_WORKSPACE/.github
cp -r rahul_copilot_setup/.vscode  YOUR_WORKSPACE/.vscode
```

### Option B: Download ZIP (no Git needed)

Download ZIP from this repo → extract → copy `.github/` and `.vscode/` to your workspace.

### After setup

Reload VS Code: `Ctrl+Shift+P` → "Reload Window"

Type `/start` in Copilot Chat to verify it works.

## Commands

| Command | What it does |
|---------|-------------|
| `/start` | Create a new project. Accepts name + description inline, or asks questions. |
| `/capture` | Extract project context from the current chat conversation. |
| `/resume {slug}` | Load a project's context. Copilot reads brief + state and is ready to work. |
| `/pause {slug}` | Auto-extracts progress from chat, shows summary for confirmation, saves. |
| `/update {slug} {notes}` | Quick mid-session save. No interruption — just "✓ Saved." |
| `/status {slug}` | One-line status check. |
| `/projects` | List all projects grouped by status. |
| `/close {slug}` | Mark project complete. Context preserved. Can be reopened with /resume. |

## How It Works

All state lives in `.context/` as plain Markdown:

```
.context/
├── INDEX.md                       ← master registry of all projects
├── sales-dashboard/
│   ├── BRIEF.md                   ← objective, key files, tables, decisions
│   ├── STATE.md                   ← done / in progress / next / blockers
│   └── LOG.md                     ← session history (append-only)
├── forecast-model/
│   └── ...
└── etl-pipeline-fix/
    └── ...
```

## Example Workflows

### Starting fresh

```
/start
→ "Sales Dashboard Rework"
→ Copilot asks for objective, key files, data sources
→ Creates .context/sales-dashboard-rework/
→ Start working...
```

### Starting with details upfront

```
/start Sales Dashboard Rework — migrate all queries from old_schema to new_schema, 
key files are dashboard.sql and transform.py, source table is analytics.sales_raw
→ Creates everything without asking questions
```

### Capturing an existing chat

```
(you've been working with Copilot for 30 minutes)
/capture sales-dashboard-rework
→ Copilot reads the entire conversation above
→ Extracts objectives, decisions, progress, pending items
→ Creates .context/sales-dashboard-rework/ with everything populated
```

### Pausing (auto-extract)

```
/pause sales-dashboard-rework
→ Copilot reads the chat, extracts what was accomplished
→ Shows: "Here's what I captured: migrated 3 queries, decided to use CTE pattern..."
→ You confirm or edit
→ Saves to STATE.md and LOG.md
```

### Pausing (quick, with inline notes)

```
/pause sales-dashboard-rework — finished query migration, need to validate row counts
→ Saves immediately, no questions asked
```

### Switching projects

```
/pause sales-dashboard-rework — done for now
/resume forecast-model
→ "Forecast Model — Paused
   Objective: Build v2 of the weekly forecast model
   Done: Feature engineering, baseline model
   In Progress: None
   Next: Hyperparameter tuning
   Blockers: None
   Ready to continue. What do you want to work on?"
```

### Quick mid-session save

```
/update sales-dashboard-rework migrated the revenue CTE, found a date format issue
→ ✓ Saved.
(keeps working, no interruption)
```

### Reopening a completed project

```
/resume old-etl-fix
→ (project was marked Complete)
→ Copilot reopens it, sets status to Active
→ Shows context and asks what to work on
```

## Edge Cases Handled

- **Slug collision:** `/start` checks if the project already exists before creating.
- **Missing slug:** Commands that need a slug will ask for it if not provided.
- **Corrupted files:** `/resume` detects missing BRIEF.md or STATE.md and offers to recreate.
- **Closed projects:** `/resume` on a completed project reopens it automatically.
- **Done list bloat:** STATE.md keeps only the 10 most recent completed items.
- **Index drift:** `/projects` reconciles INDEX.md against actual folders on disk.
- **Multi-topic chats:** `/capture` asks which topic to capture if the chat covers multiple subjects.
- **Empty chats:** `/capture` tells you if there's nothing project-relevant to extract.

## Token Cost

| Component | Tokens | When loaded |
|-----------|--------|-------------|
| `copilot-instructions.md` | ~130 | Every request (always-on) |
| `python.instructions.md` | ~80 | Only when editing `.py` files |
| `sql.instructions.md` | ~70 | Only when editing `.sql` files |
| Agent + prompt file | ~900 | Only when you invoke a `/command` |
| BRIEF.md + STATE.md | ~200-400 | Only on `/resume` |

**Always-on cost: ~130 tokens.** Everything else is on-demand only.

## What's Included

```
.github/
├── copilot-instructions.md             ← global coding conventions (always loaded)
├── agents/
│   └── pilot.agent.md                  ← context manager brain
├── prompts/
│   ├── start.prompt.md                 ← /start
│   ├── capture.prompt.md              ← /capture (extract from chat)
│   ├── resume.prompt.md                ← /resume
│   ├── pause.prompt.md                 ← /pause (auto-extract + confirm)
│   ├── update.prompt.md                ← /update (quick save)
│   ├── status.prompt.md                ← /status
│   ├── projects.prompt.md              ← /projects
│   └── close.prompt.md                 ← /close
└── instructions/
    ├── python.instructions.md           ← auto-applies to .py files
    └── sql.instructions.md              ← auto-applies to .sql files

.vscode/
└── settings.json                        ← enables customizations + token-saving settings
```

## Customization

- Edit `copilot-instructions.md` to match your stack and conventions.
- Add more `.instructions.md` files for other languages or frameworks.
- The `.vscode/settings.json` disables Copilot for YAML, JSON, and config files to save tokens. Adjust to your needs.

## License

MIT
