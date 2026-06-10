# spec.md template

Copy this template and fill it in before running `/sage-behavior`.

---

```markdown
## Feature: <FeatureName>

### What it does
<1-2 sentence description of the feature's purpose.>

### Inputs
- <param>: <Type> — <description>
- <param>: <Type> — <description>

### Outputs
- <callback or event>(): <description>
- <callback or event>(): <description>

### Acceptance criteria
- <Testable condition 1>
- <Testable condition 2>
- <Testable condition 3>

### Do NOT
- <Explicit restriction 1>
- <Explicit restriction 2>
```

---

## Tips

- If you don't know an answer to something, write `(TBD)` — the `/sage-behavior` step will surface it as an open question
- Be specific in acceptance criteria — "shows an error" is vague; "shows the string resource `R.string.invalid_email` below the email field" is testable
- The "Do NOT" section is where you encode your team's hard-won lessons about what NOT to build
