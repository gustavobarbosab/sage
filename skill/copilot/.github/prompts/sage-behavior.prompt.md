---
mode: ask
description: SAGE /behavior — spec-first AI development workflow step
---

# /sage behavior

Generates `behavior.md` from `spec.md` — with the ambiguity gate that surfaces open questions BEFORE writing test cases.

> **Note:** When triggered via `/sage spec`, this step runs automatically after spec.md is generated. Use `/sage behavior` directly only when you already have a `spec.md` and want to regenerate behavior.md independently.

## Instructions

Read `spec.md` and the harness. Then generate `behavior.md` in exactly this structure:

---

### Section 1 — Open Questions (REQUIRED, always first)

Analyze spec.md and list every ambiguity, missing detail, or behavioral decision not explicitly covered. Format:

```markdown
## Open Questions
- [ ] <Question about an ambiguous behavior>
- [ ] <Question about a missing edge case>
- [ ] <Question about a conflicting constraint>
```

Surface anything where:
- The spec is silent on expected behavior
- Two interpretations are equally valid
- An edge case isn't explicitly covered
- A constraint conflicts with another

If there are genuinely no ambiguities: `- No open questions.`

**DO NOT skip this section under any circumstances.**

---

### Section 2 — Test Cases (BLOCKED until questions resolved)

If open questions exist:
```markdown
## Test Cases
> ⚠️ Pending resolution of open questions above. Do not finalize.
```
**STOP HERE. Wait for the user to resolve questions.**

If NO open questions: generate full test cases immediately (see below).

---

### Resolving open questions

The user will either:
- Answer questions inline in chat
- Mark each `[ ]` as `[x]` with the answer in behavior.md
- Update spec.md to remove the ambiguity

When all questions are resolved, finalize test cases.

---

### Finalizing test cases

Group scenarios under: Happy path, Validation, Edge cases, Error handling.

For each scenario provide TWO versions:

```markdown
**Scenario: <Short descriptive title>**
Short → <one-line condensed form: condition + action + outcome>
Full:
- Given <precondition>
- When <action>
- Then <expected outcome>
- And <additional assertion if needed>
```

---

## Rules

- Never generate test cases before open questions are resolved
- Never skip the Open Questions section
- Short form is for quick scanning; Full form is for precise implementation guidance
- Every acceptance criterion in spec.md must have at least one corresponding scenario

---

## Output

If open questions remain:
*"behavior.md generated. Resolve the open questions above, then confirm and I'll finalize the test cases. After that, run `/sage code`."*

If no open questions:
*"behavior.md generated — no open questions. Run `/sage code` to generate the implementation."*
