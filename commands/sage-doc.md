# /sage-doc

Use this prompt to generate `doc.md` — a behavioral reference document for the feature, with edge cases and decisions captured as embedded ADRs.

This is the documentation your team will read six months from now to understand not just *what* the feature does, but *why* it works the way it does.

---

## Prompt

```
You are SAGE, a spec-first AI development assistant.

Read:
- The harness file (.sage/harness.md or in project knowledge)
- spec.md
- behavior.md
- The final generated code

Generate a doc.md with this structure:

## <FeatureName> — Behavior Reference

### Supported states
List every state the feature can be in, with a 1-line description of when it occurs.

### Validation rules
List every validation rule with the exact condition that triggers it.

### Edge cases
List every edge case explicitly documented in behavior.md, with the expected behavior.

### Decisions
For each open question that was resolved during the SAGE workflow, document:
- The decision that was made
- The reasoning behind it (the WHY, not just the WHAT)
This is the ADR-style record embedded in the feature documentation.

### Out of scope
List explicit non-goals from spec.md — what this feature deliberately does NOT handle.

### Known limitations
Anything the implementation can't currently do, even if it should eventually.

---

Be concise. Each item should be 1-2 lines. The goal is a document a teammate can scan in 60 seconds and understand the feature's behavior contract.
```

---

## Where to publish

Once you have `doc.md`, you can:

- Commit it alongside the code in your repo
- Publish to Confluence via the Atlassian MCP
- Publish to Notion via the Notion MCP
- Drop it into an Obsidian vault (it's already in Markdown)
- Add it to a GitBook space via the GitBook integration
- Wiki page on GitHub via `gh api`

---

## Tips

- The "Decisions" section is the most valuable part long-term — it captures the reasoning that would otherwise be lost
- Keep it focused on behavior, not implementation details (those live in code comments)
- If a section would be empty (e.g. no edge cases), omit it rather than padding
