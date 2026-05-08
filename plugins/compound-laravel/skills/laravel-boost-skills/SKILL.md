---
name: laravel-boost-skills
description: Discover, recommend, and install Laravel Cloud skills through Laravel Boost using php artisan boost:add-skill when the target project supports it.
argument-hint: "[skill name or task]"
allowed-tools: Read, Grep, Glob, Bash, Edit, Write
---

# Laravel Boost Skills

Use this when the user asks for Laravel-specific skills, Laravel Cloud skills, Boost skills, or when a task would benefit from a specialized Laravel/PHP skill.

## Source

The public Laravel skills directory lists reusable skills and installs them with:

```bash
php artisan boost:add-skill <owner/repo>
```

Examples from the directory include:

- `jeffallan/laravel-specialist`
- `jeffallan/php-pro`
- `affaan-m/laravel-patterns`
- `affaan-m/laravel-security`
- `affaan-m/laravel-tdd-affaan-m`
- `affaan-m/laravel-verification`
- `iserter/eloquent-best-practices-iserter`
- `asyrafhussin/laravel-best-practices`
- `thienanblog/laravel-11-12-app-guidelines`

## Workflow

1. Confirm the project has Laravel Boost available:
   - Check `composer.json` for Boost packages or run `php artisan list` if safe.
   - Confirm `php artisan boost:add-skill` exists before recommending an install command as executable.
2. Match the task to a skill:
   - General Laravel build: `jeffallan/laravel-specialist`
   - Architecture and framework patterns: `affaan-m/laravel-patterns`
   - Security audit: `affaan-m/laravel-security`
   - Test-first development: `affaan-m/laravel-tdd-affaan-m`
   - Full verification loop: `affaan-m/laravel-verification`
   - Eloquent query and relationship review: `iserter/eloquent-best-practices-iserter`
3. Ask before installing:
   - Installing modifies the target Laravel project.
   - Use `php artisan boost:add-skill <owner/repo>` only after user approval.
4. After install:
   - Read the installed skill.
   - Apply it together with the relevant Compound Laravel workflow skill.
   - Document any project-specific learning in `AGENTS.md` if it should persist.

## Rules

- Do not invent owner/repo names. If the owner is unknown, ask the user or inspect the Laravel Skills page.
- Do not install skills in non-Laravel projects.
- Do not install broad overlapping skills without a clear task need.
- Prefer this plugin's built-in `/laravel-*` workflow for compound planning/review; use Boost skills as specialized Laravel knowledge packs.

## Output

Return:

- Whether Boost is available.
- Recommended skill and why.
- Exact install command, if known.
- Any approval needed before running it.
