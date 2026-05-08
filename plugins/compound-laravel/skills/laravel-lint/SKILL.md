---
name: laravel-lint
description: Run and fix Laravel code quality issues using Pint, syntax checks, and project-configured static analysis. Use before finalizing PHP changes or when asked to lint a Laravel app.
allowed-tools: Read, Grep, Glob, Bash, Edit, Write
---

# Laravel Lint

Apply the project's existing quality tools first. Do not impose tools that are not configured unless the user asks.

## Detection

Inspect:

- `composer.json` scripts.
- `pint.json` or `pint.json.dist`.
- `phpstan.neon`, `phpstan.neon.dist`, `psalm.xml`, `rector.php`, `ecs.php`.
- `package.json` for frontend lint/build scripts.
- CI workflow files for canonical quality commands.

## Default Command Order

Use available project scripts when present. Otherwise prefer:

1. PHP syntax for changed PHP files:
   - `php -l <file>`
2. Formatting:
   - `vendor/bin/pint --dirty`
3. Static analysis if configured:
   - `vendor/bin/phpstan analyse`
   - `vendor/bin/psalm`
   - `vendor/bin/rector --dry-run`
4. Frontend quality if relevant:
   - `npm run lint`
   - `npm run build`

## Laravel Style Checks

Scan changed code for:

- `dd(`, `dump(`, `ray(`, `var_dump(`, `console.log(`.
- Missing return types where the project consistently uses them.
- Unused imports and dead code.
- Raw `DB::` queries where Eloquent would be clearer.
- Inline validation that should be a Form Request.
- Authorization missing near state-changing controller actions.
- Factories or tests using brittle hard-coded IDs.

## Fix Policy

- Run formatters automatically when linting is requested.
- Fix local, deterministic issues such as unused imports or debug statements.
- Ask before broad refactors, tool installation, or baseline regeneration.

## Output

Report:

- Commands detected and run.
- Issues fixed.
- Issues left for manual decision.
- Final quality status.
