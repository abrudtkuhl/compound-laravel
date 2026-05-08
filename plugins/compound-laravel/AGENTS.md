# Compound Laravel Agent Notes

This plugin is for Laravel apps. Future agents should preserve Laravel-native defaults instead of turning the workflow into generic PHP guidance.

## Local Conventions

- Skill names use the `laravel-*` prefix so they install as slash commands such as `/laravel-review`.
- Each skill should include concrete Laravel commands where useful, but must first inspect the target project and use its existing scripts.
- Avoid hard-coding one stack. Laravel apps may use Blade, Livewire, Inertia, Vue, React, API-only controllers, Pest, PHPUnit, Sail, Herd, Valet, Horizon, Reverb, Sanctum, Passport, Cashier, Scout, or none of these.
- When adding new skills, include success criteria and a verification checklist.

## Review Bias

Prioritize:

- Authorization and validation gaps.
- Unsafe migrations, backfills, and production data changes.
- N+1 queries, lazy-loading surprises, and missing indexes.
- Queue idempotency, retries, transaction boundaries, and event/listener side effects.
- Test coverage that uses Laravel fakes, factories, database assertions, and HTTP assertions.
- Whether the change uses Laravel primitives before custom framework code.
