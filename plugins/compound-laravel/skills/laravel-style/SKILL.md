---
name: laravel-style
description: Laravel-specific architecture, conventions, and best-practice guidance for writing or refactoring Laravel application code.
allowed-tools: Read, Grep, Glob, Bash, Edit, Write
---

# Laravel Style

Use this skill when generating, refactoring, or reviewing Laravel code. The goal is not generic PHP; it is code that feels native to the target Laravel app.

## Core Principles

- Start with framework primitives before custom abstractions.
- Preserve the existing app's conventions unless they are actively harmful.
- Keep controllers focused on HTTP orchestration.
- Put validation in Form Requests for non-trivial input.
- Put authorization in Policies or Gates.
- Put serialization in API Resources when the app uses them.
- Put durable domain behavior close to Eloquent models or existing action/service patterns.
- Use Jobs, Events, Listeners, Notifications, Mailables, Observers, Casts, Collections, and Schedules when they fit the lifecycle.
- Prefer readable Eloquent over raw SQL. Use raw SQL only when it is justified by performance or expressiveness.

## Models

- Define relationships with return types.
- Use `casts()` when the project targets modern Laravel conventions; preserve `$casts` if the app consistently uses it.
- Protect mass assignment with `$fillable` or `$guarded` according to project style.
- Name scopes in domain language.
- Avoid hidden lazy loading in views, resources, notifications, and queued jobs.
- Use custom casts or value objects for repeated data transformation.

## Controllers And Requests

- Use invokable controllers for single-purpose endpoints when the project does.
- Use resource controllers for CRUD where it maps cleanly.
- Avoid custom verbs when a nested resource is clearer.
- Use Form Requests for validation and authorization together when appropriate.
- Return redirects, views, JSON resources, or response objects consistently with nearby code.

## Database

- Name tables and columns with Laravel conventions.
- Add indexes for foreign keys, unique lookups, filters, and ordering used by new queries.
- Consider existing data before adding non-null columns.
- Prefer constraints that encode real invariants.
- Plan large backfills separately or chunk them.

## Tests

- Match Pest or PHPUnit style already in the repository.
- Use factories, states, fakes, and database assertions.
- Test policies, validation failures, happy paths, and edge cases.
- Avoid testing implementation details when feature tests can prove behavior.

## Common Anti-Patterns

- Fat controllers with validation, authorization, data access, and side effects inline.
- Service classes that only wrap one Eloquent call without reducing complexity.
- Raw request access spread through models or jobs.
- Boolean state columns when a timestamp, enum, or related state record is more expressive.
- Jobs that are not safe to retry.
- API responses hand-built inconsistently across controllers.

## Output

When advising, include:

- Current pattern found.
- Laravel-native alternative.
- Why it fits this app.
- Migration or test implications.
