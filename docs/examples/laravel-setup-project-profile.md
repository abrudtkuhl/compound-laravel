# Example: `/laravel-setup` Project Profile

This is an example output shape for a Laravel app after setup inspection. Values are illustrative; agents must inspect the target project before writing real setup notes.

```markdown
# Compound Laravel Project Profile

## App Shape

- Laravel version: 11.x from `composer.lock`
- PHP version: `^8.3` from `composer.json`
- Frontend: Inertia + React + Vite
- Auth: Sanctum for API routes, web guard for dashboard routes
- Queues/cache/mail/broadcasting: Redis queues, Redis cache, log mailer locally, Reverb not installed

## Local Commands

- Setup: `composer install`, `npm install`, `php artisan key:generate`
- Test: `composer run test`
- Format: `vendor/bin/pint --dirty`
- Static analysis: `vendor/bin/phpstan analyse`
- Frontend build: `npm run build`

## Conventions To Preserve

- Validation: Form Requests for non-trivial controller writes
- Authorization: Policies for tenant-owned models
- Data access: Eloquent relationships with explicit eager loading for index pages
- Testing: Pest feature tests with factories and `RefreshDatabase`
- Deployment/config: queue dispatch from transactions should use `afterCommit()`

## Risks To Recheck

- Migrations/data: large customer tables need chunked backfills
- Queues/events: invoice jobs must be idempotent across retries
- External services: payment webhook signatures must be verified before database writes
- Security: admin bypasses require explicit policy tests
```
