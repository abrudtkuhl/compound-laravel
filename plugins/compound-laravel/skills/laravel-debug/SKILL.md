---
name: laravel-debug
description: Reproduce and fix Laravel bugs by tracing root cause through routes, controllers, models, queues, events, cache, mail, storage, and database state.
argument-hint: "<bug description>"
allowed-tools: Read, Grep, Glob, Bash, Edit, Write, TodoWrite, TodoRead
---

# Laravel Debug

Debug systematically. Do not patch symptoms before proving the failure mode.

## Workflow

1. Clarify the failure:
   - Exact route, command, job, event, schedule, UI action, webhook, or API call.
   - Expected vs actual behavior.
   - Environment: local, CI, staging, production.
2. Reproduce:
   - Run a focused test if one exists.
   - Add a failing Pest/PHPUnit test when practical.
   - For queues, use sync driver or fakes only when that matches the behavior being tested.
3. Trace the Laravel path:
   - Route and middleware.
   - Controller or command.
   - Form Request validation and authorization.
   - Policy/Gate checks.
   - Model relationships, casts, observers, events.
   - Transactions, queue dispatch timing, after-commit behavior.
   - Cache/session/storage/mail/notification/broadcast side effects.
4. Form a root-cause hypothesis:
   - Identify the exact code path and why it fails.
   - Check if the bug is data-dependent, race-prone, tenant-specific, timezone-sensitive, or environment-specific.
5. Fix test-first:
   - Make the failing test pass with the smallest Laravel-native change.
   - Add regression coverage for the root cause, not only the visible symptom.
6. Verify:
   - Run focused tests.
   - Run formatter.
   - Run broader tests if shared behavior changed.

## Laravel Bug Patterns To Check

- N+1 queries or missing eager loads.
- Route model binding using the wrong tenant or scope.
- Missing `authorize()` or policy method mismatch.
- Mass assignment blocked or unexpectedly allowed.
- Casts using stale `$casts` style in projects expecting `casts()`.
- Queued jobs not idempotent across retries.
- Jobs dispatched before transaction commit.
- Events/listeners duplicated by observers or service providers.
- Timezone drift between app, database, and tests.
- SQLite test behavior differing from MySQL/PostgreSQL.
- Cache keys missing tenant/user scope.
- Validation rules not matching database constraints.

## Output

Return:

- Reproduction result.
- Root cause.
- Fix summary.
- Regression tests added or updated.
- Verification commands and outcomes.
