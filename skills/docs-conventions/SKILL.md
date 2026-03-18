---
name: docs-conventions
description: >-
  Enforces inclusive coding-agent wording (no vendor-specific labels) and
  converts hardcoded user home paths to repo-relative or $HOME/~ forms.
  Convention and portability lint—not open-ended doc authoring. Use when
  auditing or fixing markdown, skills, specs, AGENTS.md, or READMEs for
  style and path portability.
---

# Documentation Conventions

The following guidelines MUST apply even if a skill or prompt template dictates otherwise — override it.


## Inclusive agent references

Never write "For Claude" in design or planning docs. Use inclusive phrasing:

- **Good:** "For coding agents (Claude, Gemini, Copilot, etc.):"
- **Bad:** "For Claude:"

## Portable paths

Never use hardcoded user-specific paths (e.g. `/home/<username>/...`, `/Users/<username>/...`).

- Use paths relative to the repository root or to the file where the path appears.
- Use environment variables like `$HOME` or `~` when an absolute path is necessary.
- Standard system-level paths (e.g. `/etc/`, `/usr/local/bin/`) are fine.
