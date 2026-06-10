---
mode: ask
description: SAGE /pr — spec-first AI development workflow step
---

# /sage pr

Generates `pr.md` — a ready-to-paste PR title and description with ADR-style decisions.

## Instructions

Read:
- `spec.md`
- `behavior.md`
- The generated code files
- `doc.md` if it exists

Generate `pr.md` with this structure:

```markdown
## <Short imperative title — under 72 chars>

<2–3 sentence summary of what this PR implements and why.>

### Changes
- <Concrete code change 1>
- <Concrete code change 2>
- <Concrete code change 3>

### Decisions (ADR-style)
- <Decision made during behavior step>
  → <The reasoning behind it>
- <Another decision>
  → <The reasoning>

### Acceptance criteria covered
- [x] <Item from spec.md>
- [x] <Item from spec.md>

### Out of scope
- <What this PR deliberately does NOT include>

### Testing
- <Scenarios from behavior.md that are covered>
- <What was tested manually>
```

---

## Rules

- Title must be imperative voice ("Implement login screen" not "Implemented")
- Title must be under 72 characters
- Every resolved open question from behavior.md becomes a "Decision" entry with its reasoning
- Do not include implementation details that belong in code review comments

---

## After generation

Tell the user:
*"pr.md is ready. To open the PR directly from terminal:*
```bash
gh pr create \
  --title \"$(head -n1 pr.md | sed 's/^## //')\" \
  --body \"$(tail -n +2 pr.md)\"
```
*Run `/sage doc` to also generate the behavioral reference documentation."*
