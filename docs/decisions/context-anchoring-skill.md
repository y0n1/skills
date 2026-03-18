# Context anchoring skill (session anchor)

## Decisions
| Decision | Reason | Rejected alternative |
|----------|--------|----------------------|
| Personal skill at ~/.cursor/skills/context-anchoring/ | Single place for behavior; tessl 100% | Project-level only |
| Description includes decision logs, open questions, rationale | Tessl specificity; clearer triggers | Vague "persist decisions" |
| Feature doc primary; priming doc updates secondary | Avoid over-focus on project doc; feature state is the main anchor | Priming doc equal to feature doc |
| sessionEnd hook deferred | Reminder usefulness unclear; bloat/duplication risk | Implement hook now |

## Constraints
- Skill is personal (not project).
- No hook automation until design is clear (single rolling file / conditional / metadata-only).

## Open questions
- [ ] Whether/when to add a sessionEnd hook.
- [ ] How to make a close-time reminder useful without duplicating the real feature doc.

## State
- [x] Skill created and tessl-reviewed (100%).
- [x] Hooks discussed; decision deferred.
- [ ] Optional: implement hook later with anti-bloat rules.
