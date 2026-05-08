# Compound Laravel

Compound Laravel is a Compound Engineering plugin for Laravel applications. It keeps the plan-work-review-compound loop, but grounds every step in Laravel conventions and tooling.

## Workflow

Use the skills as a loop:

```text
/laravel-setup
/laravel-plan "add team invitations"
/laravel-work docs/plans/team-invitations-plan.md
/laravel-review
/laravel-compound
```

For bugs:

```text
/laravel-debug "queued invoice emails are duplicated"
/laravel-review
/laravel-compound
```

## Skills

| Skill | Purpose |
| --- | --- |
| `/laravel-setup` | Detect Laravel project shape, local tooling, test stack, frontend stack, queues, and Laravel Boost skills. |
| `/laravel-plan` | Turn a feature or bug into an implementation plan that names Laravel primitives, migrations, tests, and verification gates. |
| `/laravel-work` | Execute a plan with Laravel-native generators, focused tests, Pint, and documentation updates. |
| `/laravel-debug` | Reproduce failures, trace root cause across HTTP, queues, events, database, cache, and mail, then fix test-first. |
| `/laravel-review` | Review changed Laravel code for correctness, security, database safety, N+1s, tests, and framework conventions. |
| `/laravel-lint` | Run formatting and static quality checks with Pint and project-configured analyzers. |
| `/laravel-style` | Apply Laravel architecture and code-style guidance while writing or refactoring code. |
| `/laravel-security` | Audit auth, validation, mass assignment, policies, file uploads, secrets, rate limits, and deployment exposure. |
| `/laravel-test` | Design and run Pest/PHPUnit tests with factories, fakes, database assertions, and coverage-sensitive checks. |
| `/laravel-boost-skills` | Recommend or install specialized Laravel Cloud skills through Laravel Boost when the project supports it. |
| `/laravel-release` | Validate an open PR, run CI/local checks, update changelog, merge, tag, and release when requested. |
| `/laravel-compound` | Capture solved Laravel patterns in `docs/solutions/` and update `AGENTS.md` for future agents. |

## Laravel Principles

- Use Artisan generators (`php artisan make:* --no-interaction`) when creating Laravel files.
- Prefer Laravel primitives before custom infrastructure: Form Requests, Policies, Gates, Jobs, Events, Notifications, Resources, Casts, Collections, Factories, Seeders, and Schedules.
- Keep controllers thin. Put validation in Form Requests, authorization in Policies/Gates, serialization in Resources, and durable domain behavior on models or focused action classes.
- Use Eloquent relationships and eager loading before raw queries. When raw SQL is warranted, isolate it and explain why.
- Treat migrations and data changes as production risk. Plan rollback, locking, backfills, defaults, and data integrity.
- Use Pint before finalizing PHP changes. Use the project test runner, usually `php artisan test` or `composer run test`.
- Prefer Pest when the project uses Pest; preserve PHPUnit if that is the existing stack.

## Installation

For Codex local development, register this repository as a marketplace and install `compound-laravel` from the plugin UI:

```bash
codex plugin marketplace add /path/to/compound-laravel
```

Claude Code and Cursor-compatible plugin manifests are included under `.claude-plugin/` and `.cursor-plugin/`.

## Sources

This plugin is shaped by the public Compound Engineering workflow from Every and Laravel skill patterns from the Laravel skills directory and the Laravel AgentKit demo skills.
