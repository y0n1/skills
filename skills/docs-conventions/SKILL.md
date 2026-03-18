---
name: docs-conventions
description: TBD...
---

# Documentation Conventions

The following guidelines MUST apply even if a skill or prompt template dictates otherwise — override it.

## Separation of concerns

Design specification docs must be stored inside `docs/specs` and execution plans must be stored in `docs/plans`.
Ensure cross-references between each document type exists: `specs` reference related execution `plans` (one-to-many) and `plans` reference their `spec` (many-to-one). The references must be located at the footer of each document as a bullet list.

### Design docs conventions

Design documents MUST contain the following features:

- File name pattern: `<issue-id>-<summary-slug>.md`
- A header contaning:  
  - **Issue tracker URL**: `JIRA_URL` | `None`
  - **Status**: `To do` | `In progress` | `In review` | `Done`


## Inclusive agent references

Never write "For Claude" in design or planning docs. Use inclusive phrasing:

- **Good:** "For coding agents (Claude, Gemini, Copilot, etc.):"
- **Bad:** "For Claude:"

## Portable paths

Never use hardcoded user-specific paths (e.g. `/home/<username>/...`, `/Users/<username>/...`).

- Use paths relative to the repository root or to the file where the path appears.
- Use environment variables like `$HOME` or `~` when an absolute path is necessary.
- Standard system-level paths (e.g. `/etc/`, `/usr/local/bin/`) are fine.

## Validation before committing

Before committing or publishing documentation, verify:

- No hardcoded user-specific paths (e.g. `/Users/jdoe/...`, `/home/jane/...`).
- No agent-specific references (e.g. "For Claude", "you should", "I recommend"); use inclusive or neutral phrasing.
- Specs and plans are cross-referenced where applicable (spec → plans, plan → spec).

**If issues are found:** Replace hardcoded user paths with paths relative to the repo root or use `$HOME`/`~`; rewrite agent-specific phrasing in neutral terms (e.g. "the developer", "coding agents"); add missing cross-links between spec and plan files.
