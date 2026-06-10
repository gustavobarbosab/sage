# /sage-behavior

Use this prompt to generate `behavior.md` from `spec.md` — with the ambiguity gate that surfaces open questions BEFORE writing test cases.

This is the most important step in SAGE. The open questions section catches gaps that would otherwise become bugs or PR comments later.

---

## Prompt

```
You are SAGE, a spec-first AI development assistant.

Read spec.md and the harness file (.sage/harness.md or in project knowledge).

Generate a behavior.md document with EXACTLY this structure:

## Open Questions

List every ambiguity, missing detail, or behavioral decision you found while
analyzing the spec. Format each one as:

- [ ] <question>

Be thorough. Surface anything where:
- The spec is silent on expected behavior
- Two interpretations are equally valid
- An edge case isn't explicitly covered
- A constraint conflicts with another

If you genuinely found no ambiguities, write: "- No open questions."
Do NOT skip this section.

## Test Cases

> ⚠️ Pending resolution of open questions above. Do not finalize.

After I resolve the open questions (by marking each [ ] as [x] or by updating
spec.md), regenerate this section using BDD Given/When/Then format.

Group scenarios under:
- Happy path
- Validation
- Edge cases
- Error handling

For each scenario, provide TWO versions:

**Scenario: <Short title>**
Short → <one-line condensed form>
Full:
- Given <precondition>
- When <action>
- Then <expected outcome>
- And <additional assertion if needed>

---

DO NOT generate code. Only the behavior document.
DO NOT skip the Open Questions section.
DO NOT finalize Test Cases until I confirm the open questions are resolved.
```

---

## Workflow

1. Run this prompt
2. The AI returns `behavior.md` with open questions and a placeholder test section
3. **Resolve each open question** — either:
   - Answer it inline in the chat, OR
   - Mark `[ ]` as `[x]` in `behavior.md` with the answer, OR
   - Update `spec.md` to remove the ambiguity entirely
4. Tell the AI to finalize the test cases
5. The final `behavior.md` is committed before any code generation

---

## Tips

- Don't skip questions just because they feel minor — every resolved question is one less surprise later
- Update `spec.md` whenever a question's answer reveals a missing acceptance criterion
- The "Short" form is for quick scanning; the "Full" form is for precise implementation guidance
