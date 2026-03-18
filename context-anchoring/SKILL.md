---
name: context-anchoring
description: >-
  Persist feature-level decisions and reasoning in a living document: create
  decision logs, track open questions, and summarize rationale for future
  reference so new chats and other devs can resume without re-explaining. Use
  when starting or continuing multi-session feature work, when the user
  mentions losing context, multiple sessions, or anxiety about closing the
  chat; when work spans days or multiple developers; or when the user asks to
  "anchor context," "save decisions," or "document what we decided."
---

# Context Anchoring

Persist decision context in a **feature document** outside the chat so new sessions and other developers can resume without re-explaining. The conversation stays the medium for making decisions; the document is the record.

## When to suggest anchoring

- Work will span or has spanned **multiple sessions**.
- User mentions **losing context**, **re-explaining**, or not wanting to **close the chat**.
- **Multiple people** (or multiple AI sessions) work on the same feature.
- User explicitly asks to **anchor context**, **save decisions**, or **document what we decided**.

## When not to push it

- One-off question, quick fix, or single short session with no plan to return.

## Two layers of context

1. **Feature document (primary)** — Feature-level decisions, reasoning, constraints, open questions, and state. Evolves every session. This is the main anchor; create or update it when anchoring is warranted.

2. **Project-level priming (secondary)** — Tech stack, architecture, conventions. More stable. When a project already has a priming document (e.g. in rules, docs, or AGENTS.md), **still recommend considering updates to it** when feature work reveals new patterns, conventions, or stack choices that belong in project-level context. Treat priming doc updates as secondary to the feature doc: the feature doc is the living record for the current work; priming doc changes are optional follow-ups so future sessions benefit.

## Feature document template

Offer to create or update a feature doc using this structure:

```markdown
# Feature: [Name and version]

## Decisions
| Decision | Reason | Rejected alternative |
|----------|--------|----------------------|
| ...      | ...    | ...                  |

## Constraints
- ...

## Open questions
- [ ] ...

## State
- [ ] Design / implementation items...
```

Keep it short (e.g. under 50 lines). Update at natural pause points: end of a design step, after a significant decision, or when resolving an open question.

## Calibration

| Scenario | Anchoring | Why |
|----------|-----------|-----|
| Quick question, single utility | No | Context decay irrelevant |
| Single-session feature (&lt; ~1 hr) | Optional, lightweight | A few bullets enough to restart if needed |
| Multi-session / multi-day | Yes — full feature doc | Cost of lost context is high |
| Multiple developers on feature | Yes — shared feature doc | Aligns independent sessions |

## Litmus test

If the user (or the situation) implies **"I'm worried about closing this chat"** — treat that as a signal to suggest anchoring and offer to draft or update the feature doc.

## What the agent should do

- When anchoring is warranted: **offer** to create or update a feature doc (and suggest a path, e.g. `docs/decisions/` or next to the code). Do not assume a path; ask or use project conventions if visible.
- When the user agrees: populate the template from the conversation (decisions, reasons, rejected alternatives, constraints, open questions, state). If the user prefers to write it, offer a short summary they can paste.
- When a project has a priming doc: after updating the feature doc, **recommend considering** whether the priming doc should be updated (e.g. new pattern, new convention). Frame priming doc updates as secondary to the feature doc.
