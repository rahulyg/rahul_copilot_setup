---
name: 'SQL Conventions'
description: 'BigQuery SQL standards for data analytics'
applyTo: '**/*.sql'
---

- Layered CTEs with descriptive names (raw_data, filtered, aggregated)
- No nested subqueries — refactor into CTEs
- QUALIFY for deduplication, not subquery-based dedup
- Date filtering with DATE() or TIMESTAMP_TRUNC, never string casting
- snake_case for column aliases
- Comment header on every query: purpose and source table(s)
