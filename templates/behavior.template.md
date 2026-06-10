# behavior.md template

This is what `/sage-behavior` will produce. Use this as a reference for the expected structure.

---

```markdown
## Open Questions

- [ ] <Ambiguity or missing detail from spec.md>
- [ ] <Another open question>

## Test Cases

> ⚠️ Pending resolution of open questions above. Do not finalize.

### Happy path

**Scenario: <Short title>**
Short → <one-line condensed form>
Full:
- Given <precondition>
- When <action>
- Then <expected outcome>

### Validation

**Scenario: <Short title>**
Short → <condensed form>
Full:
- Given ...
- When ...
- Then ...

### Edge cases

**Scenario: <Short title>**
Short → <condensed form>
Full:
- Given ...
- When ...
- Then ...

### Error handling

**Scenario: <Short title>**
Short → <condensed form>
Full:
- Given ...
- When ...
- Then ...
```

---

## Resolving open questions

Each `- [ ]` item must become `- [x]` with the answer inline, OR be removed entirely by updating `spec.md`.

Example of a resolved item:
```
- [x] Should timeout and wrong credentials show the same error?
      → Yes, generic error for both. Prevents account enumeration.
```

Once all questions are resolved, ask the AI to finalize the test cases section.
