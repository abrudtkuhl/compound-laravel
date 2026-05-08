# Example: `/laravel-review` Output

This example shows the expected level of specificity for review findings. It is illustrative and does not refer to this repository.

```text
P1 app/Http/Controllers/TeamInvitationController.php:48 Missing policy check allows members to invite users to teams they do not own.
Why it matters: The route accepts a team ID and only checks that the requester is authenticated. A user who can guess another team ID can create invitations outside their team.
Suggested fix: Add `authorize('invite', $team)` in the controller or move authorization into `StoreTeamInvitationRequest::authorize()`, backed by a Team policy method.
Verification: Add a feature test where a member from Team A posts to Team B's invitation route and receives 403.

P2 database/migrations/2026_05_08_120000_add_status_to_invoices.php:14 New non-null column lacks a default for existing rows.
Why it matters: Production deploys can fail or leave existing invoices in an invalid state depending on the database engine and table size.
Suggested fix: Add a safe default, split the backfill from the schema change, or make the column nullable until a chunked backfill completes.
Verification: Run the migration against a database with existing invoice rows and add a regression test for default status behavior.
```

When there are no findings, the review should still report residual risk:

```text
No findings.

Verification run:
- `php artisan test tests/Feature/TeamInvitationTest.php` passed
- `vendor/bin/pint --dirty` passed

Residual risk: Full test suite and frontend build were not run.
```
