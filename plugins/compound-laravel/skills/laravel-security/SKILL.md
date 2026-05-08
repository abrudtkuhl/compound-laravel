---
name: laravel-security
description: Audit Laravel applications for authentication, authorization, validation, mass assignment, file uploads, secrets, rate limiting, webhooks, and deployment exposure.
allowed-tools: Read, Grep, Glob, Bash, Edit, Write
---

# Laravel Security

Review security in Laravel terms. Tie every finding to a reachable route, command, job, webhook, or data path.

## Audit Checklist

### Authentication And Sessions

- Auth middleware protects private routes.
- Guards match the route surface: web, api, sanctum, passport, custom.
- Session fixation, remember tokens, password resets, and email verification follow Laravel defaults unless intentionally customized.

### Authorization

- State-changing actions call Policies or Gates.
- Route model binding is tenant/user scoped.
- Policies cover view, create, update, delete, restore, force delete, and custom abilities as needed.
- Admin bypasses are explicit and tested.

### Validation And Input

- Form Requests or validated data are used before writes.
- Validation matches database constraints.
- User-controlled IDs are authorized after lookup.
- Redirects and URLs are constrained to avoid open redirects.

### Mass Assignment And Serialization

- Models use `$fillable` or `$guarded` intentionally.
- Request data is not passed wholesale into sensitive model creation/update.
- Hidden attributes and API Resources do not expose secrets or internal flags.

### Files, Storage, And Downloads

- Uploads validate MIME, extension, size, and dimensions where relevant.
- Private files are stored on private disks and served through authorized routes.
- Paths are not user-controllable.

### Webhooks, Queues, And External Calls

- Webhook signatures are verified.
- Duplicate delivery is idempotent.
- Jobs avoid logging secrets and are retry-safe.
- External HTTP calls use timeouts and handle failures.

### Configuration And Deployment

- `.env` files and secrets are not committed.
- `APP_DEBUG=false` in production.
- Trusted proxies, CORS, cookies, and session domains are configured intentionally.
- Rate limiting protects login, password reset, webhooks, public APIs, and expensive actions.

## Search Hints

Look for:

- `Route::`
- `withoutMiddleware`
- `authorize(`
- `Gate::`
- `Policy`
- `validate(`
- `request()->all()`
- `->all()`
- `fillable`
- `guarded`
- `Storage::`
- `Http::`
- `Log::`
- `APP_DEBUG`

## Output

Lead with exploitable findings. For each one include:

- Route or entry point.
- Affected data or capability.
- Exploit scenario.
- Laravel-native fix.
- Test to prove the fix.
