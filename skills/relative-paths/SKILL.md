---
name: relative-paths
description: >-
  Prefer relative paths and workspace-relative references over user-specific absolute paths. Use when generating file paths, links in code or docs, example commands, or any output that could contain /Users/username, $HOME, or machine-specific absolute paths.
---

# Use Relative Paths, Not User-Specific Links

## Rule

**Never emit user-specific or machine-specific absolute paths in generated output.** Use paths relative to the project/workspace root or to the current file.

## When This Applies

- File paths in code, config, or documentation
- Links in markdown, comments, or docstrings
- Example commands (e.g. `cd`, `cat`, file arguments)
- References to scripts, config files, or assets
- Error messages or logging examples that show paths

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

## In Code and Docs

- **Imports and requires:** Use project-relative paths as the project already does (e.g. `from masu.external.foo`, `import '@/components/Bar'`).
- **Documentation links:** Link to files with repo-relative paths, e.g. `[api.ts](src/api/api.ts)` or `See scripts/run-pytest.sh`.
- **Examples:** Show commands as if run from project root: `./scripts/run-pytest.sh`, not `./Users/me/project/scripts/run-pytest.sh`.

## Quick Check

Before returning output, scan for:

- `/Users/`, `/home/`, `C:\Users\`
- Expanded `$HOME` or `~` with a specific path
- Any path that would change on another developer’s machine

If found, replace with a relative path or a generic placeholder.
