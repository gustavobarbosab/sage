# /sage update

Applies precise, spec-anchored feedback to generated code.

## Inline argument

The user provides feedback inline:
```
/sage update "Scenario 'Double submit' is missing the assertion that no duplicate request is made"
/sage update "spec item 4 violated — navigation is inside the ViewModel, move it out"
/sage update "harness says Material3 only but the code imports Material2 Button"
```

If no argument is provided, ask: *"What needs changing? Tie your feedback to a specific spec item or scenario."*

---

## Instructions

Read the feedback argument. Apply the requested changes to the relevant files.

Rules:
- Do NOT introduce changes the user didn't request
- Do NOT deviate from the harness
- If a requested change would violate spec.md or behavior.md, flag it before applying:
  *"⚠️ This change conflicts with [spec item / scenario]. Do you want to update the spec first?"*
- Return only the modified files in the same `// FILE:` format

---

## What good feedback looks like

Guide the user toward precise feedback if theirs is vague:

✅ *"Scenario `Double submit during loading` is missing the assertion that no duplicate auth request is made"*
✅ *"Spec item 'Generic error on auth failure' is violated — raw exception message is surfaced. Replace with a generic string resource."*
✅ *"Harness says navigation via lambda callbacks but LoginViewModel calls NavController directly."*

❌ *"This doesn't look right"* → ask: *"Which spec item or scenario does it violate?"*
❌ *"Make it cleaner"* → ask: *"What specifically should change?"*

---

## After update

Tell the user:
*"Changes applied. Review the updated files. Run `/sage update <feedback>` again for further changes, or `/sage pr` and `/sage doc` when ready to export."*
