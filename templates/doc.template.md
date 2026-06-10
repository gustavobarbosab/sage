# doc.md template

This is what `/sage-doc` will produce — the behavioral reference for the feature.

---

```markdown
## <FeatureName> — Behavior Reference

### Supported states
- <State 1>: <When it occurs>
- <State 2>: <When it occurs>
- <State 3>: <When it occurs>

### Validation rules
- <Field>: <Validation rule and trigger condition>
- <Field>: <Validation rule and trigger condition>

### Edge cases
- <Edge case>: <Expected behavior>
- <Edge case>: <Expected behavior>

### Decisions
- <Decision made during the SAGE workflow>
  → <The reasoning behind it>
- <Another decision>
  → <The reasoning>

### Out of scope
- <What this feature deliberately does NOT handle>
- <Another out-of-scope item>

### Known limitations
- <Current limitation>
- <Future improvement>
```

---

## Where to publish

- Commit alongside the code in your repo
- Confluence via Atlassian MCP
- Notion via Notion MCP
- Obsidian vault (drop the file in)
- GitBook space via integration
- GitHub Wiki via `gh api`
