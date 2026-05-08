---
name: laravel-setup
description: Inspect and bootstrap a Laravel project for Compound Laravel workflows. Use before planning or reviewing a Laravel app, or when onboarding to an unfamiliar Laravel codebase.
allowed-tools: Read, Grep, Glob, Bash, Edit, Write
---

# Laravel Setup

Inspect the target repository and produce a concise setup report. Make only low-risk edits when the user explicitly asks for setup changes.

## Workflow

1. Confirm the repository is a Laravel app:
   - Look for `artisan`, `composer.json`, `bootstrap/app.php`, `config/app.php`, `routes/`, `app/`, and `database/migrations/`.
   - If it is not Laravel, stop and report what is missing.
2. Read project instructions:
   - `AGENTS.md`, `CLAUDE.md`, `README.md`, `docs/`, `.env.example`, `composer.json`, `package.json`, `phpunit.xml`, `pint.json`, `rector.php`, `phpstan.neon`, `vite.config.*`.
3. Detect framework and app shape:
   - Laravel version from `composer.lock` or `composer.json`.
   - PHP version constraint.
   - Test runner: Pest, PHPUnit, or both.
   - Frontend: Blade, Livewire, Inertia, Vue, React, Alpine, Tailwind, Vite.
   - Auth: Breeze, Jetstream, Fortify, Sanctum, Passport, Socialite, custom.
   - Queues, cache, broadcasting, mail, Scout, Cashier, Horizon, Telescope, Reverb, Octane.
4. Detect available commands:
   - Prefer project scripts from `composer.json` and `package.json`.
   - Common commands include `composer install`, `composer run setup`, `composer run test`, `php artisan test`, `vendor/bin/pint --dirty`, `npm install`, `npm run build`, and `npm run test`.
5. Check Laravel Boost skills:
   - If `php artisan boost:add-skill` is available, note it.
   - Recommend relevant public Laravel skills only when useful, such as Laravel specialist, Laravel patterns, Laravel security, Laravel TDD, or Laravel verification.
6. Report setup status:
   - Ready commands.
   - Missing dependencies or configuration.
   - Safe next command to run.
   - Project-specific conventions future skills should honor.

## Laravel Defaults

- Do not invent setup scripts when the project already has Composer or npm scripts.
- Do not overwrite `.env`. If needed, copy `.env.example` to `.env` only with user approval.
- Do not run migrations against a non-local database unless the user confirms the environment.
- Prefer `composer run setup` when present because Laravel starter kits often encode the project-specific bootstrap there.

## Output

Return:

- Laravel detection result.
- Framework/package summary.
- Test, format, static-analysis, frontend, and queue commands.
- Known risks or missing prerequisites.
- Recommended next skill: `/laravel-plan`, `/laravel-work`, `/laravel-debug`, or `/laravel-review`.
