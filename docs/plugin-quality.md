# Compound Laravel Plugin Quality Checklist

Use this checklist when improving this plugin itself. The goal is to keep every skill useful in real Laravel repositories, not just internally consistent as documentation.

## Manifest Checks

- `.codex-plugin/plugin.json`, `.claude-plugin/plugin.json`, and `.cursor-plugin/plugin.json` describe the same plugin name, version, repository, license, and skill directory.
- Root marketplace files point to `plugins/compound-laravel`.
- Version changes are reflected in `CHANGELOG.md` when behavior changes.
- Plugin descriptions explain the plan -> work -> review -> compound loop in Laravel terms.

## Skill Checks

- Every skill has a clear trigger, expected input, workflow, output shape, and verification guidance.
- Every implementation-facing skill says to inspect local conventions before applying defaults.
- Commands prefer project scripts from `composer.json`, `package.json`, and CI workflows before fallback commands.
- Risky actions call out approval boundaries, especially migrations, releases, branch changes, destructive Git operations, and production data access.
- Skills avoid hard-coding one Laravel stack. They should work across Blade, Livewire, Inertia, API-only apps, Pest, PHPUnit, Sail, Herd, Valet, Horizon, Reverb, Sanctum, Passport, Cashier, and Scout.

## Laravel Coverage Checks

- Planning covers routes, controllers, middleware, Form Requests, Policies/Gates, models, casts, observers, jobs, events, listeners, notifications, mailables, resources, migrations, seeders, factories, views/components, and frontend assets where relevant.
- Review covers authorization, validation, mass assignment, file uploads, secrets, rate limits, webhooks, unsafe migrations, indexes, N+1 queries, queue idempotency, retries, transaction boundaries, cache scoping, and side effects.
- Testing guidance uses factories, fakes, database assertions, HTTP assertions, time travel, and project-standard Pest/PHPUnit style.
- Release guidance covers CI checks, changelog/version updates, migration rollout notes, config/env changes, and rollback/failure recovery.

## Dogfooding Flow

1. Treat the plugin change as a normal Compound task.
2. Plan the desired improvement in `docs/plans/` when it touches several files.
3. Edit the smallest useful set of docs, skills, agents, or manifests.
4. Review the diff using the same risk lenses the plugin teaches.
5. Capture recurring lessons in `plugins/compound-laravel/AGENTS.md` or docs when they affect future plugin work.

## Done Criteria

- New guidance is actionable enough that another agent can follow it without guessing.
- Examples show concrete output shapes, not only descriptions.
- No skill tells agents to invent tools or project structure before checking the target repository.
- The root README and plugin README stay aligned on the skill list and workflow.
