---
name: relative-paths
description: >-
  In markdown files only: replaces user- or machine-specific absolute paths with repo- or file-relative paths. Use relative links (e.g. [file](path/to/file.md)), relative paths in code blocks and examples; avoid /Users/..., $HOME, ~/, C:\Users\.... Use when editing or generating .md files, markdown documentation, or markdown content that contains file paths or links.
---

# Use Relative Paths in Markdown

## Scope

**This skill applies only to markdown (`.md`) files.** When editing or generating markdown, use relative paths for all file references and links.

## Rule

**Never emit user-specific or machine-specific absolute paths in markdown.** Use paths relative to the repo root or to the current file.

**Example:** `./scripts/run-pytest.sh` ✓ — not `/Users/jane/project/scripts/run-pytest.sh` ✗

## Actions

- **Replace** any absolute path in markdown (links, code blocks, inline paths) with a path relative to repo root or current file.
- **Write** markdown links as repo-relative: `[label](path/to/file.md)` or `[label](path/to/file.ts)`.
- **Emit** paths in markdown code blocks as if from project root (e.g. `./scripts/run-pytest.sh`).
- **Avoid** `/Users/...`, `/home/...`, `~/...`, `$HOME/...`, or `C:\Users\...` in any markdown content.

## When This Applies

- Editing or creating `.md` files
- Adding or changing links in markdown (`[text](url)`)
- Writing file paths or example commands inside markdown code blocks
- Referencing scripts, config files, or other repo files in documentation

## Do

| Context | Use |
|--------|-----|
| Any file in the project | `src/utils.ts`, `package.json`, `apps/koku-ui-sources/src/api/api.ts` |
| Path from repo root | `scripts/run-pytest.sh`, `cost-onprem/values.yaml` |
| Path relative to current file | `./components/Button.tsx`, `../api/client.ts` |
| Generic placeholder | `path/to/file`, `<project-root>/src/...` |

## Don't

| Avoid | Why |
|-------|-----|
| `/Users/john/project/src/utils.ts` | Exposes username and machine path |
| `$HOME/projects/repo/...` | User-specific |
| `C:\Users\jane\...` | Machine- and OS-specific |
| `~/Projects/docs-store/...` | User-specific home path |
| Any path containing a real username or hostname | Not portable, not shareable |

## In Markdown

- **Links:** Use repo-relative paths in link URLs, e.g. `[api.ts](src/api/api.ts)` or `[plan](docs/plans/plan.md)`.
- **Code blocks:** Use paths as if from project root: `./scripts/run-pytest.sh`, not `/Users/me/project/scripts/run-pytest.sh`.
- **Inline paths:** Write `path/to/file` or `scripts/foo.sh`; never embed absolute or user-specific paths.

## Quick Check

Before returning markdown, scan for:

- `/Users/`, `/home/`, `C:\Users\`
- Expanded `$HOME` or `~` with a specific path
- Any path that would change on another developer’s machine

If found, replace with a relative path or a generic placeholder.
