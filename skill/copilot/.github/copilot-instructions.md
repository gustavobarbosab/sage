# SAGE — GitHub Copilot Instructions
# Save this file as .github/copilot-instructions.md in your project root.
# Copilot will use these instructions for all chat interactions in this repo.

## Project Harness

<!-- Fill in your project conventions below, or run @sage harness init to generate. -->
<!-- See .sage/harness.md for the full harness. -->

Stack: <!-- e.g. Kotlin 2.0, Jetpack Compose, Hilt, MVI, StateFlow -->
Conventions: <!-- e.g. ViewModel + StateFlow, Composables receive state + callbacks only -->
Avoid: <!-- e.g. LiveData, XML views, Material2, hardcoded strings -->

---

## SAGE Workflow

SAGE is a spec-first, AI-assisted development workflow built on SDD, BDD, and Harness Engineering.

When I reference a SAGE command, follow the instructions below exactly.

### /sage spec <description>

Two-phase command — do NOT generate files immediately.

**Phase 1 — Interview:**
Analyze the description and prepare questions. Show ALL questions at once:
```
I have X questions before writing your spec and behavior files. Answer them all and I'll generate both at once.

Question 1 of X
[Category: Purpose & scope]
<question>

Question 2 of X
[Category: Inputs & outputs]
<question>
...
```
Minimum 3, maximum 10 questions. Wait for answers before proceeding.

**Phase 2 — Generation (after answers received):**
Generate `spec.md`:
```
## Feature / ### What it does / ### Inputs / ### Outputs / ### Acceptance criteria / ### Do NOT
```
Then immediately generate `behavior.md` in the same response:
- Open Questions first (`- [ ]` items or `- No open questions.`)
- Test Cases (placeholder if questions remain, full BDD scenarios if none)

### /sage behavior

Read `spec.md`. Generate `behavior.md` with:

**Open Questions section (ALWAYS first):**
- List every ambiguity as `- [ ] <question>`
- If no ambiguities: `- No open questions.`

**Test Cases section:**
- Output `> ⚠️ Pending resolution of open questions above.`
- STOP. Wait for user to resolve questions.

After resolution: generate BDD Given/When/Then scenarios. Each scenario needs:
```
**Scenario: <title>**
Short → <condition + action + outcome>
Full:
- Given <precondition>
- When <action>
- Then <outcome>
```

### /sage code

**Before generating:** Check `behavior.md` for `- [ ]` items.
If any remain: list them and stop. Do not generate code.

When clear: generate code following harness conventions exactly.
Format: `// FILE: <relative/path>` before each file.

### /sage update <feedback>

Apply precise spec-anchored changes only.
If change conflicts with `spec.md` or `behavior.md`, flag it first.

### /sage pr

Generate `pr.md`:
- Imperative title under 72 chars
- 2-3 sentence summary
- Changes list
- Decisions (ADR-style): every resolved open question + reasoning
- Acceptance criteria checklist
- Out of scope
- Testing notes

### /sage doc

Generate `doc.md`:
- Supported states
- Validation rules
- Edge cases
- Decisions with reasoning (ADR-style)
- Out of scope
- Known limitations

### /sage harness init

Run interactive wizard — ask stack questions one at a time.
Save result to `.sage/harness.md`.

### /sage harness generate

Ask user to share codebase files. Infer conventions.
Flag low-confidence items with ❓, inconsistencies with ⚠️.
Save result to `.sage/harness.md`.

### /sage harness review

Read `.sage/harness.md`. Report:
- Issues: `⚠️ <issue> → <fix>`
- Suggestions: `💡 <suggestion> → <why>`
