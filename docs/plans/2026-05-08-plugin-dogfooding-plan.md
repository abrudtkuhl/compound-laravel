# Compound Laravel Plugin Dogfooding Plan

## Problem And Goal

The plugin teaches a plan -> work -> review -> compound loop, but the plugin repository did not yet include enough self-review guidance or concrete output examples for agents improving the plugin itself.

Goal: make the plugin easier to improve by adding plugin QA guidance, reusable example outputs, and skill instructions that explicitly support dogfooding.

## Non-Goals

- Do not change the public skill names.
- Do not add new runtime dependencies.
- Do not make the plugin specific to one Laravel starter kit or frontend stack.
- Do not replace the existing skill set with generic PHP guidance.

## Existing Behavior And Constraints

- The repository is a plugin repository, not a Laravel app.
- The plugin already includes setup, planning, work, debug, review, lint, style, security, testing, release, Boost, and compound skills.
- Root and plugin README files both describe the workflow and must stay aligned.
- Marketplace manifests should continue pointing to `plugins/compound-laravel`.

## Planned Changes

- Add `docs/plugin-quality.md` as the canonical checklist for reviewing this plugin.
- Add examples under `docs/examples/` for setup profiles, review findings, and compound learning capture.
- Update `/laravel-setup` so it can produce a persistent `docs/compound-laravel/project-profile.md` in target Laravel apps.
- Update `/laravel-review` so it knows how to review this plugin repository using the quality checklist.
- Update `/laravel-compound` so plugin-specific learnings have clear destinations.
- Update `AGENTS.md`, `README.md`, and plugin README references so future agents can discover the workflow.

## Verification

- Check Git diff for scope.
- Validate JSON manifests with `python3 -m json.tool`.
- Search for stale skill counts and broken references.
- Confirm markdown examples are readable and use valid fenced code blocks.

## Done Criteria

- Plugin improvements are documented in a reusable way.
- Skills link to examples or quality gates where useful.
- Future agents have a concrete checklist for improving the plugin.
- `CHANGELOG.md` records the improvement.
