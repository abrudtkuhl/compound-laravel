# Compound Laravel Plugin

The Laravel-native companion to [Compound Engineering](https://every.to/guides/compound-engineering).

Compound Laravel packages the plan -> work -> review -> compound loop for agents building real Laravel applications. It keeps the core Compound Engineering idea, but grounds every step in the framework primitives Laravel teams already use: Artisan, Eloquent, Form Requests, Policies, API Resources, Jobs, Events, Notifications, migrations, factories, queues, Pint, Pest, PHPUnit, and the conventions of the target app.

The goal is not to make an agent write more code. The goal is to make every Laravel task leave the project easier for the next task.

## The Philosophy

Laravel projects get slower when each change adds a little more hidden behavior: another controller branch, another unchecked migration, another queue edge case, another undocumented convention. Compound Laravel pushes work in the opposite direction.

Each feature should teach the system something reusable. Each bug fix should remove a category of future bugs. Each review should capture a pattern that future agents can find. Over time, the app should become easier to understand, safer to modify, and faster to extend.

For Laravel, that means the agent should prefer the framework's own vocabulary before inventing new structure:

- Form Requests for validation.
- Policies and Gates for authorization.
- Jobs, Events, Notifications, Schedules, and Mailables for application behavior.
- Eloquent relationships, scopes, casts, factories, seeders, and resources for data flow.
- Pint, Pest, PHPUnit, static analysis, and project CI for safety nets.

## The Main Loop

```text
Setup -> Plan -> Work -> Review -> Compound -> Repeat
```

The loop works for a five-minute bug or a multi-day feature. Spend more time planning and reviewing when the blast radius is high; keep it light when the change is obvious and well-covered.

### 1. Setup

First, teach the agent what kind of Laravel app it is inside:

- Detect the Laravel version, PHP version, package manager, frontend stack, queue driver, cache driver, mail setup, database, and test runner.
- Check whether the project uses Pest or PHPUnit.
- Find local scripts for Pint, static analysis, CI, and browser tests.
- Look for Laravel Boost skills when the project supports `php artisan boost:add-skill`.

### 2. Plan

Planning turns a feature or bug into a Laravel-aware implementation blueprint:

- Name the models, controllers, routes, requests, policies, jobs, events, notifications, resources, migrations, factories, and tests likely to change.
- Identify production risks in migrations, backfills, locks, defaults, and data integrity.
- Decide which validation gates prove the change works.
- Keep the plan concrete enough that an agent can execute without guessing.

### 3. Work

Execution follows the plan with Laravel-native tooling:

- Use Artisan generators (`php artisan make:* --no-interaction`) when creating Laravel files.
- Preserve existing project patterns before introducing new abstractions.
- Run focused tests while working, then broader checks when risk warrants it.
- Use Pint before finalizing PHP changes.
- Track what changed and what remains.

### 4. Review

Review catches correctness issues before they ship and turns the findings into stronger future constraints:

- Check authorization, validation, mass assignment, file uploads, secrets, rate limits, and exposed debug state.
- Look for unsafe migrations, data loss, missing indexes, N+1 queries, and queue or transaction hazards.
- Confirm tests cover the behavior and the failure mode.
- Prioritize findings so the agent fixes the highest-risk issues first.

### 5. Compound

The compound step is what makes the next task easier:

- Capture the solved pattern in `docs/solutions/`.
- Update `AGENTS.md` when the project has a convention the agent should remember.
- Record verification commands and known pitfalls.
- Make the learning findable so future sessions do not rediscover it from scratch.

## Quick Start

### Codex

Register this repository as a local marketplace, then install `compound-laravel` from Codex's plugin UI:

```bash
codex plugin marketplace add /path/to/compound-laravel
```

### Claude Code

Use this repository as a plugin source and install `compound-laravel`:

```text
/plugin marketplace add /path/to/compound-laravel
/plugin install compound-laravel
```

### Cursor

Use the plugin marketplace entry in `.cursor-plugin/marketplace.json` and install `compound-laravel`.

## Core Workflow

For features:

```text
/laravel-setup
/laravel-plan "add team invitations"
/laravel-work docs/plans/team-invitations-plan.md
/laravel-review
/laravel-compound
```

For improving this plugin itself, use the same loop with the plugin quality checklist:

```text
/laravel-plan "improve the compound-laravel plugin"
/laravel-review
/laravel-compound
```

The self-review checklist lives in `docs/plugin-quality.md`, with example outputs in `docs/examples/`.

For bugs:

```text
/laravel-debug "invoice webhook sometimes creates duplicates"
/laravel-review
/laravel-compound
```

## What's In The Box

- 12 Laravel-focused skills for setup, planning, implementation, debugging, review, linting, testing, security, release, and learning capture.
- 4 review agents for conventions, security, data safety, and testing.
- Codex, Claude Code, and Cursor marketplace manifests.
- Agent instructions that bias toward Laravel's existing conventions and the target application's local patterns.
- Plugin QA guidance and example outputs for dogfooding the plugin itself.

## Where Things Live

```text
compound-laravel/
|-- README.md
|-- docs/
|   |-- plugin-quality.md
|   |-- examples/
|   `-- plans/
|-- .agents/plugins/marketplace.json
|-- .claude-plugin/marketplace.json
|-- .cursor-plugin/marketplace.json
`-- plugins/
    `-- compound-laravel/
        |-- AGENTS.md
        |-- README.md
        |-- agents/
        |   |-- laravel-conventions-reviewer.agent.md
        |   |-- laravel-data-safety-reviewer.agent.md
        |   |-- laravel-security-reviewer.agent.md
        |   `-- laravel-testing-reviewer.agent.md
        `-- skills/
            |-- laravel-setup/
            |-- laravel-plan/
            |-- laravel-work/
            |-- laravel-debug/
            |-- laravel-review/
            |-- laravel-lint/
            |-- laravel-style/
            |-- laravel-security/
            |-- laravel-test/
            |-- laravel-boost-skills/
            |-- laravel-release/
            `-- laravel-compound/
```

## Core Skills

### `/laravel-setup`

Detects Laravel project shape, local tooling, test stack, frontend stack, queues, and Laravel Boost skills.

### `/laravel-plan`

Turns a feature or bug into an implementation plan that names Laravel primitives, migrations, tests, and verification gates.

```text
/laravel-plan "add team invitations"
```

### `/laravel-work`

Executes a plan with Laravel-native generators, focused tests, Pint, and documentation updates.

```text
/laravel-work docs/plans/team-invitations-plan.md
```

### `/laravel-debug`

Reproduces failures, traces root cause across HTTP, queues, events, database, cache, and mail, then fixes test-first.

```text
/laravel-debug "queued invoice emails are duplicated"
```

### `/laravel-review`

Reviews changed Laravel code for correctness, security, database safety, N+1s, tests, and framework conventions.

### `/laravel-lint`

Runs formatting and static quality checks with Pint and project-configured analyzers.

### `/laravel-style`

Applies Laravel architecture and code-style guidance while writing or refactoring code.

### `/laravel-security`

Audits auth, validation, mass assignment, policies, file uploads, secrets, rate limits, and deployment exposure.

### `/laravel-test`

Designs and runs Pest/PHPUnit tests with factories, fakes, database assertions, and coverage-sensitive checks.

### `/laravel-boost-skills`

Recommends or installs specialized Laravel Cloud skills through Laravel Boost when the project supports it.

### `/laravel-release`

Validates an open PR, runs CI/local checks, updates changelog, merges, tags, and releases when requested.

### `/laravel-compound`

Captures solved Laravel patterns in `docs/solutions/` and updates `AGENTS.md` for future agents.

## Review Agents

- `laravel-conventions-reviewer` checks Laravel structure, naming, controller boundaries, framework idioms, and unnecessary custom infrastructure.
- `laravel-security-reviewer` checks authorization, validation, mass assignment, secrets, uploads, rate limits, and exposed debug state.
- `laravel-data-safety-reviewer` checks migrations, indexes, transactions, backfills, rollbacks, queues, and production data risk.
- `laravel-testing-reviewer` checks whether Pest/PHPUnit coverage proves the changed behavior and the likely failure modes.

## Beliefs To Let Go

### "Laravel is just PHP with routes"

Laravel is a set of strong defaults. Agents work better when they lean into those defaults instead of treating the app like a generic PHP codebase.

### "A passing test is enough"

Tests matter, but Laravel changes often carry operational risk outside the assertion: queue timing, migration locks, cache invalidation, policy gaps, and N+1 queries. Review should include those risks explicitly.

### "Documentation happens after shipping"

The compound step is part of the work. If a solution teaches the project a reusable pattern, capture it while the context is still fresh.

## Beliefs To Adopt

### Use Laravel primitives first

Reach for Form Requests, Policies, Jobs, Events, Notifications, Resources, factories, casts, scopes, and schedules before custom infrastructure. Custom structure should earn its keep.

### Make database changes boring

Treat migrations and data changes as production risk. Plan rollback, locking, backfills, defaults, indexes, and integrity before implementation.

### Put project taste where agents can read it

When a review finding reflects a project preference, add the preference to `AGENTS.md` or a solution document. Do not rely on the next session rediscovering it.

### Let safety nets carry more work

If the agent should be trusted to modify the app, it needs access to the same evidence a developer would use: tests, Pint, logs, browser checks, queue behavior, migrations, and CI output.

## Sources

This package follows the public Compound Engineering plugin shape and workflow from Every's `compound-engineering-plugin`, incorporates Laravel-specific workflow ideas from the Laravel AgentKit demo skills, and points agents toward the Laravel Skills directory when a project supports `php artisan boost:add-skill`.
