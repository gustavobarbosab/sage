# pr.md template

This is what `/sage-pull-request` will produce.

---

```markdown
## <Short imperative title — under 72 chars>

<2-3 sentence summary of what this PR implements and why.>

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
- [x] <Item from spec.md>

### Out of scope
- <What this PR deliberately does NOT include>
- <Follow-up tickets if any>

### Testing
- <Scenarios from behavior.md that are covered>
- <Manual testing done>
- <What's left for QA>
```

---

## Opening the PR

After `pr.md` is generated, open the PR directly:

```bash
gh pr create \
  --title "$(head -n1 pr.md | sed 's/^## //')" \
  --body "$(tail -n +2 pr.md)"
```

Or paste into the GitHub web UI.
