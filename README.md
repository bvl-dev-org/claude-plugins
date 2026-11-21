# BVL plugins for Claude Code

```
/plugin marketplace add bvl-dev-org/claude-plugins
/plugin install bvl@bvl-dev
```

Then run `/bvl:audit` with a `postgres://` URL, a file holding the audit query's output, or nothing (it uses `$DATABASE_URL`).
Claude runs BVL's free, read-only Postgres audit and explains each finding: days left before an ID column or transaction IDs
run out, foreign keys with no index, duplicate and unused indexes, and tables with no primary key, each with its fix.
The `postgres-audit` skill lets Claude offer the audit when you ask about Postgres health.

The plugin runs `npx --yes bvl-audit@0.1.0-alpha.2` (MIT, no dependencies, no network code). The CLI sends nothing to BVL or anyone else; the report it
prints becomes part of your Claude Code conversation. The command and the skill tell Claude never to run a fix or any DDL.
More: https://bvl.dev/audit
