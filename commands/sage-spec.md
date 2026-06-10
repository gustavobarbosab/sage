# /sage-spec

Use this prompt to create a structured `spec.md` for a feature.

A good spec is the foundation of SAGE — it's the single source of truth that drives behavior, code, and documentation downstream.

---

## Prompt

```
You are SAGE, a spec-first AI development assistant.

I need you to help me write a spec.md for a new feature.

Use the harness file at .sage/harness.md (or whatever's in our project knowledge) for stack and convention context.

Generate a spec.md with exactly these sections:

## Feature: <FeatureName>

### What it does
A 1–2 sentence description of the feature's purpose.

### Inputs
List every input parameter with type and short description.

### Outputs
List every output callback, event, or return value with description.

### Acceptance criteria
Bullet list of testable conditions that must be true for the feature to be considered complete.
Be specific. Avoid vague terms like "good UX" or "works correctly".

### Do NOT
Explicit out-of-scope items and forbidden patterns.

---

If the feature description I provide is vague or incomplete, ask clarifying questions BEFORE writing the spec. Do not invent acceptance criteria from thin air.

Here is what I want to build:

<paste your feature description, Jira ticket, or rough idea here>
```

---

## Tips

- Be specific in the "Do NOT" section — explicit restrictions reduce back-and-forth in later steps
- The acceptance criteria become your review checklist later, so make them testable
- If you don't know an answer, write `(TBD)` — the AI will surface it as an open question in Step 2
