# /sage doc

Generates `doc.md` — a behavioral reference document for the feature with ADR-style decisions embedded.

## Instructions

Read:
- `spec.md`
- `behavior.md`
- The generated code files
- `pr.md` if it exists

Generate `doc.md` with this structure:

```markdown
## <FeatureName> — Behavior Reference

### Supported states
- <State>: <When it occurs — 1 line>

### Validation rules
- <Field>: <Rule and exact trigger condition>

### Edge cases
- <Edge case>: <Expected behavior>

### Decisions
- <Decision made during SAGE workflow>
  → <The reasoning — the WHY, not just the WHAT>

### Out of scope
- <What this feature deliberately does NOT handle>

### Known limitations
- <Current limitation or future improvement>
```

---

## Rules

- Each item should be 1–2 lines — the goal is a document a teammate scans in 60 seconds
- The "Decisions" section is the most valuable long-term — it captures reasoning that would otherwise be lost
- Every resolved open question from behavior.md must appear as a Decision entry
- Omit empty sections rather than padding with placeholders
- Focus on behavior, not implementation details (those belong in code comments)

---

## After generation

Tell the user:
*"doc.md is ready. You can publish it to:*
- *Commit alongside the code in your repo*
- *Confluence via Atlassian MCP*
- *Notion via Notion MCP*
- *Obsidian vault — drop the file in directly*
- *GitHub Wiki via `gh api`"*
