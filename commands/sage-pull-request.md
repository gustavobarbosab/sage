# /sage-pull-request

Use this prompt to generate `pr.md` — a ready-to-paste PR title and description with embedded ADR-style decisions.

---

## Prompt

```
You are SAGE, a spec-first AI development assistant.

Read:
- spec.md
- behavior.md
- The final generated code
- doc.md (if it exists)

Generate a pr.md with this structure:

## <Short PR title — one line, imperative voice>

<2-3 sentence summary of what this PR implements and why>

### Changes
Bullet list of the concrete code changes (new classes, modified files, key behaviors implemented).

### Decisions (ADR-style)
For each open question resolved during the SAGE workflow:
- <The decision made>
  → <The reasoning behind it>

### Acceptance criteria covered
Reference the items from spec.md that this PR satisfies (use a checklist).

### Out of scope
Briefly mention what this PR deliberately does NOT include and why
(e.g. follow-up tickets, deferred decisions).

### Testing
Brief description of test coverage — which scenarios from behavior.md are covered, what was tested manually, what's left for QA.

---

The title should be imperative voice ("Implement login screen" not "Implemented login screen") and under 72 characters.

Do not include implementation details that belong in code review comments — keep this focused on intent, scope, and decisions.
```

---

## How to open the PR

After `pr.md` is generated, you can open the PR directly with the GitHub CLI:

```bash
gh pr create \
  --title "$(head -n1 pr.md | sed 's/^## //')" \
  --body "$(tail -n +2 pr.md)"
```

Or just copy-paste into the GitHub web UI.

---

## Tips

- The "Decisions" section is gold for reviewers — they see WHY you made the choices you made without having to ask
- Keep the title imperative and concise — `git log` becomes much more useful
- If the PR is large, consider splitting it before opening — `pr.md` will tell you if too many decisions are bundled
