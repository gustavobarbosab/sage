# /sage harness review

Audits the current `.sage/harness.md` for drift, gaps, or inconsistencies.

## Instructions

Read `.sage/harness.md` (or `CLAUDE.md`, `.cursorrules`, or project knowledge).

Analyze for:
1. **Vague or unenforceable rules** — rules that can't be checked in code review
2. **Conflicting conventions** — rules that contradict each other
3. **Missing categories** — common gaps: error handling, navigation, testing, string resources
4. **Outdated stack versions** — deprecated patterns or libraries
5. **Anything that would cause inconsistent AI output** — ambiguous rules

Format issues as:
```
⚠️ <Issue> → <Suggested fix>
```

Format improvement suggestions as:
```
💡 <Suggestion> → <Why it would help AI output quality>
```

If the harness is solid, say so explicitly. Don't manufacture issues.

---

## Rules

- Be specific — "improve naming conventions" is not useful; "the ViewModel naming rule doesn't specify whether test files use `Test` or `Spec` suffix" is
- Don't suggest rules just because they're common — every rule has a maintenance cost
- The best harnesses are short and decisive, not long and exhaustive

---

## After review

Tell the user:
*"Review complete. For each ⚠️ — decide whether to update the harness, update the code, or both, and commit the change with a brief message. 💡 suggestions are optional — add only what genuinely improves AI output."*
