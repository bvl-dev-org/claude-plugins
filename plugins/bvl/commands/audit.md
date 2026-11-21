---
description: Audit a Postgres database for time bombs (ID and transaction ID exhaustion, index problems, missing primary keys)
argument-hint: "[postgres url, or a file with the query output]"
---
Run the BVL audit and explain the result.

1. If $ARGUMENTS is a file path, run `npx --yes bvl-audit@0.1.0-alpha.2 --input "$ARGUMENTS" --format markdown`.
2. Otherwise, if $ARGUMENTS is a postgres:// or postgresql:// URL, run
   `npx --yes bvl-audit@0.1.0-alpha.2 --url "<that URL>" --format markdown`. Never print the URL or its password back.
   If $ARGUMENTS is empty and DATABASE_URL is set, run `npx --yes bvl-audit@0.1.0-alpha.2 --format markdown` with no `--url`: the
   CLI reads DATABASE_URL itself. Never expand, echo or print DATABASE_URL.
3. If psql is missing or there is no URL, show the user `npx --yes bvl-audit@0.1.0-alpha.2 --print-query`, ask them to run it in
   their SQL client and save the output to a file, then run step 1 with that file.
4. Explain the findings in order: Act now, Plan, Risk, Waste. For each, say what breaks, the fix SQL from the output,
   and when a fix_link is present, that https://bvl.dev page shows how Migration check rates that change.
5. Do not run any fix yourself. Do not run DDL on the database.
