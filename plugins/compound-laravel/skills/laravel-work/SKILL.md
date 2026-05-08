---
name: laravel-work
description: Execute a Laravel implementation plan using Artisan, project-native patterns, focused tests, Pint, and documentation updates.
argument-hint: "[plan path or task]"
allowed-tools: Read, Grep, Glob, Bash, Edit, Write, TodoWrite, TodoRead
---

# Laravel Work

Implement the requested Laravel change end to end. Prefer an existing plan; if none exists and the task is multi-step, create a short working plan before editing.

## Execution Rules

- Read the relevant plan, project instructions, and affected files first.
- Preserve existing project conventions even when this skill has a default preference.
- Use `php artisan make:* --no-interaction` for new Laravel classes when available.
- Keep changes scoped. Do not refactor unrelated code.
- Never revert user changes unless explicitly asked.
- Add or update tests for behavior changes.
- Run the narrowest useful tests first, then broader verification when the risk warrants it.
- Run Pint or the project formatter before finalizing PHP edits.

## Implementation Checklist

1. Confirm scope:
   - Current branch and working tree.
   - Files likely to change.
   - Test runner and formatting commands.
2. Implement domain behavior:
   - Models, casts, relationships, scopes, policies, events, jobs, notifications, services/actions only where locally established.
3. Implement HTTP or UI surface:
   - Routes, controllers, Form Requests, Resources, views, Livewire/Inertia components, frontend assets.
4. Implement data changes:
   - Migrations, indexes, constraints, seeders, factories, safe backfills.
5. Implement tests:
   - Feature tests for user-visible behavior.
   - Unit tests for pure domain logic when useful.
   - Queue/mail/event/storage/cache fakes where applicable.
6. Verify:
   - Focused `php artisan test --filter=...` or file-level tests.
   - `vendor/bin/pint --dirty` or project formatter.
   - Broader `php artisan test`, `composer run test`, `npm run build`, or CI-equivalent when needed.
7. Update docs:
   - `README.md`, `CHANGELOG.md`, `AGENTS.md`, or project docs when the change affects usage, setup, deployment, or future agent knowledge.

## Done Criteria

- Behavior is implemented with Laravel-native primitives.
- Tests cover happy path, failure path, and important edge cases.
- Formatter has run or the reason it could not run is stated.
- No debug statements remain: `dd()`, `dump()`, `ray()`, `var_dump()`, `console.log()`.
- Final response names changed files and verification results.
