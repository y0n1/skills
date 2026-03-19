---
name: relative-paths
description: In markdown files only: replaces user- or machine-specific absolute paths with repo- or file-relative paths. Use relative links (e.g. [file](path/to/file.md)), relative paths in code blocks and examples; avoid /Users/..., $HOME, ~/, C:\Users\.... Absolute paths to standard system directories (e.g. /usr, /etc, /var, /tmp) are fine. Use when editing or generating .md files, markdown documentation, or markdown content that contains file paths or links.
---

# Use Relative Paths in Markdown

## Scope

**This skill applies only to markdown (`.md`) files.** When editing or generating markdown, use relative paths for all file references and links.

## Rule

**Never emit user-specific or machine-specific absolute paths in markdown.** Use paths relative to the repo root or to the current file.

**Exception:** Absolute paths to standard system-wide directories are fine (e.g. `/usr`, `/etc`, `/var`, `/tmp`, `/opt` on Unix; `C:\Windows`, `C:\Program Files` on Windows). Only avoid paths that include usernames, home directories, or project locations that vary by machine.

**Example:** `./scripts/run-pytest.sh` ✓ — not `/Users/jane/project/scripts/run-pytest.sh` ✗

## Actions

- **Replace** user-specific absolute paths in markdown (links, code blocks, inline paths) with paths relative to repo root or current file.
- **Links:** Use repo-relative URLs: `[label](path/to/file.md)` or `[api.ts](src/api/api.ts)`.
- **Code blocks:** Use paths as if from project root (e.g. `./scripts/run-pytest.sh`).
- **Inline paths:** Use `path/to/file` or `scripts/foo.sh`; avoid `/Users/...`, `/home/...`, `~/...`, `$HOME/...`, `C:\Users\<username>\...`.

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
| `C:\Users\jane\...` | User-specific (Windows profile) |
| `~/Projects/docs-store/...` | User-specific home path |
| Any path containing a real username or hostname | Not portable, not shareable |

## Quick Check

Before returning markdown, scan for user-specific paths only (system paths: see Exception in Rule):

- `/Users/`, `/home/`, or `C:\Users\<username>\`
- Expanded `$HOME` or `~` with a specific path
- Project or home paths that vary by machine

Replace only those with a relative path or placeholder; leave system paths unchanged.
