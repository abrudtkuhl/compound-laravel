---
name: laravel-test
description: Design, write, and run Laravel tests with Pest or PHPUnit, factories, fakes, database assertions, and focused verification.
allowed-tools: Read, Grep, Glob, Bash, Edit, Write, TodoWrite, TodoRead
---

# Laravel Test

Use the target project's test style. Prefer Pest when the app uses Pest; preserve PHPUnit when that is the established style.

## Test Planning

1. Identify changed behavior and risk.
2. Choose the lowest level that proves user-visible behavior:
   - Feature tests for routes, controllers, Livewire/Inertia endpoints, auth, validation, and API behavior.
   - Unit tests for pure domain methods, casts, rules, services, or value objects.
   - Browser tests only when JavaScript behavior cannot be proven otherwise.
3. Cover:
   - Happy path.
   - Validation failure.
   - Authorization failure.
   - Important edge cases.
   - Side effects such as mail, notifications, events, queues, storage, cache, and database writes.

## Laravel Testing Tools

- Factories and states for data setup.
- `actingAs()` for authenticated flows.
- Policy and guard-specific tests where authorization is the risk.
- `RefreshDatabase` or the local equivalent.
- `Event::fake()`, `Queue::fake()`, `Mail::fake()`, `Notification::fake()`, `Storage::fake()`, `Http::fake()`.
- `Carbon::setTestNow()` or time travel helpers for time-sensitive logic.
- `assertDatabaseHas`, `assertDatabaseMissing`, response assertions, JSON assertions.

## Commands

Prefer project scripts when present:

- `composer run test`
- `php artisan test`
- `php artisan test tests/Feature/FooTest.php`
- `php artisan test --filter="can create team invitation"`
- `npm run test`

## Test Quality Bar

- Assertions must prove behavior, not just status codes.
- Tests should not depend on hard-coded database IDs.
- Fakes should be asserted.
- Avoid excessive mocking of Eloquent and Laravel facades in feature tests.
- Use transactions and factories instead of shared fixture state unless the project has another standard.

## Output

Report:

- Tests added or changed.
- Commands run.
- Failures fixed.
- Coverage gaps that remain.
