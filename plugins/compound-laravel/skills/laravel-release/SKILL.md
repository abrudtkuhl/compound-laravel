---
name: laravel-release
description: Validate and release a Laravel PR or current branch after review, including CI checks, local tests, changelog update, merge, branch cleanup, and tagging when requested.
argument-hint: "[PR URL or number]"
allowed-tools: Read, Grep, Glob, Bash, Edit, Write
---

# Laravel Release

Use this only when the user explicitly wants to release, merge, tag, or approve a PR. Do not merge without confirmation where the host requires it.

## Preflight

1. Identify the current branch and PR:
   - `git branch --show-current`
   - `gh pr list --head <branch> --state open`
2. Confirm the PR exists and is open.
3. Review current status:
   - `git status --short`
   - `gh pr checks <number>`
   - `gh pr view <number>`

## Release Review

Perform a quick Laravel release gate:

- Are `/laravel-review` findings resolved or intentionally deferred?
- Do tests cover the changed behavior?
- Do migrations and data changes have safe rollout/rollback notes?
- Are env/config/deployment changes documented?
- Does the code still follow Laravel conventions?

## Verification

Run the project-native checks:

- `php artisan test` or `composer run test`.
- `vendor/bin/pint --dirty` if PHP changed.
- `npm run build` if frontend assets changed.
- Any CI-required command from workflow files.

Abort release if checks fail unless the user explicitly decides to proceed.

## Changelog And Tagging

- Update `CHANGELOG.md` when the project maintains one.
- Determine version from existing tags and the PR type.
- Prefer semantic versioning when the project already uses it.
- Create a release tag only when the user requested a release, not merely a merge.

## Merge

Use the repository's existing merge strategy. If unclear, prefer squash merge for feature branches:

- `gh pr merge <number> --squash --delete-branch`

Do not delete local branches with unmerged local-only work.

## Output

Return:

- PR number/link.
- Checks run and result.
- Release review outcome.
- Changelog/version/tag result.
- Merge result or blocker.
