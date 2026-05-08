---
name: laravel-review
description: Perform a Laravel-focused code review of the current branch or a supplied PR, with emphasis on Laravel conventions, security, data safety, tests, and production reliability.
argument-hint: "[blank for current branch, PR URL, PR number, branch, or base:<ref>]"
allowed-tools: Read, Grep, Glob, Bash, Edit, Write, TodoWrite, TodoRead
---

# Laravel Review

Review as a Laravel maintainer. Findings must be concrete, reproducible, and tied to code locations.

## Scope Detection

1. Parse optional arguments:
   - `base:<ref>` sets the diff base.
   - A PR URL/number or branch narrows the target.
   - Blank means review current branch against its merge base.
2. Inspect:
   - `git status --short`
   - `git diff --stat`
   - Relevant changed files and tests.
3. Do not switch branches in a shared checkout unless the user explicitly asks.

## Review Lenses

### Laravel Correctness

- Routes point to the intended controllers/actions and middleware.
- Route model binding is correctly scoped, especially for tenants and ownership.
- Controllers are thin enough and use Form Requests for meaningful validation.
- Policies/Gates cover protected actions.
- API Resources or response conventions are preserved.
- Model casts, accessors, mutators, relationships, and scopes match current Laravel conventions.

### Data And Migrations

- Migrations are reversible when possible and safe for existing production data.
- Columns have appropriate nullability, defaults, indexes, unique constraints, and foreign keys.
- Backfills are separated or chunked when large tables may be involved.
- Schema changes do not rely on SQLite-only test behavior.
- Data writes are transactional where consistency matters.

### Security

- Inputs are validated and authorization is explicit.
- Mass assignment is controlled.
- File uploads validate type, size, visibility, and storage disk.
- Secrets are not committed or logged.
- Rate limiting and CSRF expectations match route type.
- Webhooks verify signatures and are idempotent.

### Performance And Reliability

- Avoid N+1 queries with eager loading, counts, aggregates, or constrained relationships.
- Queue jobs are idempotent, retry-safe, and use `afterCommit()` when needed.
- Cache keys include tenant/user/context scope.
- External calls have timeouts and failure handling.
- Scheduled commands and listeners are safe to rerun.

### Tests

- New behavior has Feature tests or browser/component tests where appropriate.
- Domain behavior has focused Unit tests when useful.
- Tests use factories, fakes, database assertions, mail/notification/event/queue fakes, and time travel appropriately.
- Assertions prove authorization, validation failure, happy path, and important edge cases.

## Finding Format

Lead with findings, ordered by severity:

```text
P1 file.php:123 Missing policy check allows users to update another team's resource.
Why it matters: ...
Suggested fix: ...
Verification: ...
```

Use:

- `P0` critical exploit, data loss, or total breakage.
- `P1` high-impact likely defect.
- `P2` meaningful bug, security gap, reliability risk, or missing test.
- `P3` small maintainability or style issue.

If no findings exist, say that clearly and mention remaining test or verification gaps.

## Optional Autofix

Only apply fixes when the user asked for fixes or the issue is clearly safe and local. Never auto-apply behavior-changing authorization, migration, or data fixes without approval.

## Plugin Self-Review

When reviewing this plugin repository instead of a Laravel application:

- Use `docs/plugin-quality.md` as the checklist.
- Verify every changed skill has a concrete trigger, workflow, output shape, and verification guidance.
- Check that examples in `docs/examples/` match the behavior the skills ask agents to produce.
- Confirm root and plugin READMEs stay aligned with the actual skill list.
- Treat vague guidance as a finding when it would make an agent guess in a real Laravel codebase.

## Verification

Recommend or run:

- Focused `php artisan test --filter=...`
- Changed test files.
- `vendor/bin/pint --dirty`
- `composer run test`
- `npm run build`

State which commands ran and which did not.

See `docs/examples/laravel-review-output.md` for the expected finding shape.
