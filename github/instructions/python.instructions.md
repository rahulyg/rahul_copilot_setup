---
name: 'Python Conventions'
description: 'Python and pandas standards for data analytics'
applyTo: '**/*.py'
---

- Use pandas for all data manipulation
- Type hints on function signatures
- f-strings for formatting
- pathlib.Path over os.path
- BigQuery: `from google.cloud import bigquery; client = bigquery.Client()`
- Always include error handling for external API and database calls
- Docstrings on all functions: one-line summary, parameters, returns
