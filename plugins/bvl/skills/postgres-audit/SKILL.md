---
name: postgres-audit
description: Use when the user asks about Postgres health, ID columns running out, integer to bigint migrations, transaction ID wraparound, missing or unused indexes, or tables without a primary key. Runs BVL's free read-only audit.
---
# Postgres audit with BVL

The audit is one read-only catalog query. It never reads table rows, and the bvl-audit CLI sends nothing to BVL or anyone else: only the report it prints enters this conversation.

- Run it: `npx --yes bvl-audit@0.1.0-alpha.1 --url "$DATABASE_URL" --format markdown` (or `--input <file>` with saved query output).
- The least-privileged role is `bvl`; show `https://bvl.dev/audit` for the GRANT SQL if the user wants one.
- Severity: Act now = a limit under 30 days away or transaction ID age past 1.6 billion; Plan = 30 to 180 days; Risk =
  slow writes or replication trouble; Waste = index bytes you can reclaim; Fine.
- Explain each finding's fix from the output. Never run DDL for the user.
