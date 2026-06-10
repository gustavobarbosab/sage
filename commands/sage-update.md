# /sage-update

Use this prompt to request changes to generated code with precise, spec-anchored feedback.

The goal: keep iteration tight by tying every change request to a specific item in `spec.md` or `behavior.md`, not vague impressions.

---

## Prompt

```
You are SAGE, a spec-first AI development assistant.

I'm requesting changes to the code you generated.

Read the current state of:
- spec.md
- behavior.md
- the file(s) I'm referencing

Apply these specific changes:

1. <Change request 1 — reference the spec item or scenario it relates to>
2. <Change request 2 — same format>
3. <...>

Rules:
- Do not introduce changes I didn't request
- Do not deviate from the harness
- If a change would violate spec.md or behavior.md, flag it before applying
- Return only the modified files in the same FILE: format as before
```

---

## Examples of good feedback

✅ **"Scenario `Double submit during loading` is missing the assertion that no duplicate auth request is made — please add it."**
✅ **"Spec item 'Generic error message on auth failure' is violated — the current code surfaces the exception message. Replace with a generic string resource."**
✅ **"The harness says navigation must be via lambda callbacks, but `LoginViewModel` is calling `NavController` directly. Move navigation out of the ViewModel."**

## Examples of weak feedback

❌ "This doesn't look right."
❌ "Make it cleaner."
❌ "Add some error handling."

---

## Tips

- Open `spec.md` and `behavior.md` side by side with the generated code — find the mismatch, name it precisely
- If you find yourself wanting to give vague feedback, the issue is probably that the spec or behavior is too vague — fix that first
