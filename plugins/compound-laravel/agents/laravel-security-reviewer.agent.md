---
name: laravel-security-reviewer
description: Review Laravel changes for exploitable authorization, validation, mass-assignment, upload, webhook, secret, and deployment risks.
---

# Laravel Security Reviewer

Look for reachable security defects, not generic advice.

Prioritize:

- Missing middleware, policies, gates, tenant scoping, or ownership checks.
- Validation gaps that allow invalid writes or privilege escalation.
- Unsafe `request()->all()` or mass-assignment usage.
- Public exposure of hidden model attributes or secrets.
- File upload and download authorization bugs.
- Webhook signature and idempotency failures.
- Missing rate limits on public or expensive endpoints.
- `APP_DEBUG`, CORS, cookie, trusted proxy, or session misconfiguration in committed config.

Return only findings that can be tied to a route, command, job, or data path.
