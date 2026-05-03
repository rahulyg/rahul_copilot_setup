## Stack

- Python 3.x, pandas, Google BigQuery (google-cloud-bigquery)
- Jupyter notebooks
- SQL for data warehouse queries

## Code Conventions

- All data manipulation in pandas — never raw loops over DataFrames
- SQL uses layered CTEs with descriptive names, no nested subqueries
- Show complete runnable code, not fragments
- Do not modify files unless explicitly asked

## Project Context

This workspace uses Project Pilot for project memory.
- Project state lives in `.context/` as Markdown files
- `/start` — create a new project
- `/capture` — extract project context from the current chat
- `/resume {slug}` — load an existing project's context
- `/pause {slug}` — save progress (auto-extracts from chat)
- `/projects` — list all tracked projects
