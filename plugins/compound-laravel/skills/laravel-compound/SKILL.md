---
name: laravel-compound
description: Capture reusable Laravel learnings after solving a problem so future agents can move faster in the same codebase.
argument-hint: "[summary, PR, bug, or completed plan]"
allowed-tools: Read, Grep, Glob, Bash, Edit, Write
---

# Laravel Compound

Document the reusable lesson, not the entire task history. The goal is to make the next related Laravel change easier.

## What To Capture

Capture a learning when the work revealed:

- A project-specific Laravel convention.
- A surprising route, middleware, policy, tenant, or auth boundary.
- A migration or data-safety pattern.
- A testing helper, factory state, fake, or assertion pattern.
- A queue, event, notification, mail, cache, or storage caveat.
- A deployment or configuration gotcha.
- A recurring review finding and its preferred fix.

Do not capture:

- Generic Laravel facts available in the docs.
- One-off implementation details unlikely to recur.
- Secrets or sensitive customer data.

## Artifact Location

Prefer:

- `docs/solutions/YYYY-MM-DD-short-laravel-learning.md`

If the project already has a knowledge directory, use it instead.

## Document Shape

```markdown
# Short Title

## Context

What problem or project area this applies to.

## Learning

The reusable rule or pattern.

## Laravel Pattern

Framework primitive, command, or convention to use next time.

## Example

Small code or command example if useful.

## Verification

How to confirm the pattern works.

## References

Files, PRs, docs, or tests that prove the learning.
```

## AGENTS.md Update

If the lesson changes future agent behavior, add a short note to `AGENTS.md`. Keep it actionable and project-specific.

## Plugin Improvement Capture

When improving this plugin itself, capture reusable process lessons in one of these places:

- `docs/plugin-quality.md` for broad quality gates.
- `docs/examples/` for output shapes future agents should imitate.
- `plugins/compound-laravel/AGENTS.md` for durable rules about maintaining this plugin.

Do not capture generic Laravel facts in plugin docs unless they directly improve a skill, agent, manifest, or example.

## Output

Return:

- Learning file path.
- `AGENTS.md` update, if any.
- One-line summary of how future work benefits.

See `docs/examples/laravel-compound-learning.md` for the expected learning shape.
