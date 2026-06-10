# /sage-harness-generate

Use this prompt to let AI infer a `harness.md` from your existing codebase.

This is the fastest way to onboard SAGE into an existing project — point the AI at your code and let it extract the conventions you've already established.

---

## Prompt

```
You are SAGE, a spec-first AI development assistant.

I'll share several files from my codebase. Analyze them and generate a harness.md
that captures:

- Tech stack and versions (from build files, package manifests, lockfiles)
- Architecture patterns in use (MVI, MVVM, Clean Architecture, etc.)
- Naming conventions (ViewModel suffixes, file organization, package structure)
- Dependency injection approach
- State management patterns
- Navigation approach
- Test framework and naming patterns
- Patterns that appear to be deliberately avoided

Format the output as:

## Project Harness — <inferred project name>

### Stack
- Bullet list

### Conventions
- Naming patterns with examples from the code
- Architecture rules

### Avoid
- Anti-patterns NOT found in the code (i.e. things the team has avoided)
- Deprecated APIs not used

Flag anything that seems inconsistent across files with:
⚠️ Inconsistency: <description>

Where you're inferring something with low confidence, mark it:
❓ Possibly: <inferred rule> — confirm before adopting

I will paste the files now. After you've analyzed them, generate the harness.
```

---

## Files to share

The most useful files to feed the AI:

- `build.gradle.kts` / `build.gradle` / `package.json` / `pyproject.toml` (stack and versions)
- 2-3 `ViewModel` or equivalent state-holding classes (architecture patterns)
- 2-3 UI files / screens / components (UI conventions)
- 1-2 DI modules (injection approach)
- 1-2 test files (test conventions)
- Any existing `.editorconfig`, `.cursorrules`, `CLAUDE.md`, or style guide

Don't include secrets, generated code, or massive files — the AI just needs enough context to infer patterns.

---

## After generation

1. **Review the inferred harness carefully** — AI is good at pattern recognition but can miss intent
2. **Resolve every ⚠️ inconsistency** — decide which version is the actual convention
3. **Confirm every ❓ possibly** — these are guesses
4. **Save to your tool's expected location** (see [sage-harness-init.md](sage-harness-init.md) for paths)
5. **Run [`/sage-harness-review`](sage-harness-review.md) periodically** to catch drift over time

---

## Tips

- The "Avoid" section will likely be sparse on first generation — add to it as you notice the AI defaulting to patterns you don't want
- Inferred harnesses are starting points, not final answers — expect to spend 15-30 minutes refining the first one
