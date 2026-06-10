# /sage-harness-review

Use this prompt to audit your current `harness.md` for drift, gaps, or inconsistencies.

Harnesses get stale. Conventions evolve. This command catches the mismatch.

---

## Prompt

```
You are SAGE, a spec-first AI development assistant.

Review the harness.md I'll provide for:

1. Vague or unenforceable rules (rules that can't be checked in code review)
2. Conflicting conventions (rules that contradict each other)
3. Missing common categories (e.g. testing, error handling, navigation)
4. Outdated stack versions or deprecated patterns
5. Anything that would cause inconsistent AI output

For each issue found, format as:
⚠️ <Issue> → <Suggested fix>

Also flag opportunities to strengthen the harness:
💡 <Suggestion> → <Why it would help>

Be specific. Don't tell me "improve naming conventions" — tell me which convention
is unclear and what concrete rule would fix it.

If the harness is solid, say so. Don't manufacture issues.
```

---

## When to run this

- **Every quarter** — convention drift is inevitable in active projects
- **After a major refactor** — your old harness may now describe patterns you've abandoned
- **When you notice AI output drifting** — if generated code keeps missing a convention, the harness probably doesn't enforce it strongly enough
- **Before onboarding a new team member** — fresh eyes on the harness reveal what's actually documented vs assumed

---

## After review

For each ⚠️:
- Decide whether to update the harness, update the code, or both
- Commit the harness change with a brief explanation in the message

For each 💡:
- Treat as optional — add if it would genuinely strengthen the AI's output
- Skip if it would over-constrain without clear benefit

---

## Tips

- A harness with no issues is rare and often a sign you've stopped iterating
- Don't add rules just because the AI flagged them — every rule has a maintenance cost
- The best harnesses are short and decisive, not long and exhaustive
