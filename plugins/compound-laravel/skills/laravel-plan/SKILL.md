---
name: laravel-plan
description: Create a Compound Engineering implementation plan for a Laravel feature, bug, refactor, or migration. Use before making multi-file Laravel changes.
argument-hint: "<feature, bug, or requirements doc>"
allowed-tools: Read, Grep, Glob, Bash, Edit, Write, TodoWrite, TodoRead
---

# Laravel Plan

Turn the request into a concrete plan that is small enough to execute and specific to the Laravel app in front of you.

## Inputs

Accept a rough idea, bug report, PR comment, or path to an existing requirements document. If the request is ambiguous, ask only the questions needed to avoid rework.

## Research

1. Read project instructions and setup evidence:
   - `AGENTS.md`, `CLAUDE.md`, `README.md`, relevant docs, `composer.json`, `routes/*`, affected models/controllers/views/tests.
2. Identify the Laravel surface area:
   - Routes, controllers, middleware, Form Requests, Policies/Gates, models, casts, observers, jobs, events, listeners, notifications, mailables, resources, migrations, seeders, factories, views/components, Livewire/Inertia assets.
3. Check existing patterns before proposing new ones:
   - Naming, namespaces, service/action class usage, test style, factories, API response conventions, auth and tenant boundaries.
4. If framework behavior is uncertain, verify from official Laravel documentation or the installed code instead of guessing.

## Plan Shape

Write a plan under `docs/plans/YYYY-MM-DD-###-short-name-plan.md` unless the user asks for a different location.

Include:

- Problem and goal.
- Non-goals.
- Existing behavior and constraints.
- Laravel primitives to use and why.
- Data model and migration plan, including indexes, foreign keys, defaults, backfills, rollback notes, and lock risk.
- HTTP/API/UI flow, including routes, validation, authorization, response/resource shape, and error states.
- Queue/event/mail/cache/search implications.
- Testing plan with Pest/PHPUnit examples at the right level.
- Verification commands.
- Rollout, observability, and failure recovery for risky changes.
- Task checklist with file-level ownership where possible.

## Laravel Way Heuristics

- Use Form Requests for non-trivial validation.
- Use Policies or Gates for authorization. Do not hide authorization in controllers by accident.
- Use Eloquent relationships and eager loading before raw SQL.
- Use API Resources for JSON response shape when the app already uses them.
- Keep controllers thin. Prefer model behavior, Jobs, Events, Notifications, or focused action classes according to existing project style.
- Use migrations for schema, factories for test data, fakes for side effects, and `RefreshDatabase` or the project-standard database testing approach.
- Generate files with `php artisan make:* --no-interaction` during implementation.

## Confidence Gate

Before handing off to work, state whether confidence is high, medium, or low. Low confidence plans must list the missing facts and the exact inspection needed next.

## Output

Return the plan path and the shortest useful summary of the tasks and verification gates.
