---
name: sage
description: SAGE — spec-first, AI-assisted development workflow using SDD, BDD, and Harness Engineering. Use this skill whenever the user types /sage, wants to write a spec, generate behavior scenarios, generate code from a spec, export a PR description or documentation, manage a project harness, or mentions spec.md, behavior.md, harness.md, pr.md, or doc.md. Also triggers when the user asks to start a feature using AI, define acceptance criteria before coding, or generate BDD test scenarios. Always use this skill for any /sage command, even if the request seems simple.
---

# SAGE

**S**pec · **A**ssert · **G**enerate · **E**xport

A spec-first workflow that combines SDD, BDD, and Harness Engineering to front-load thinking and back-load generation.

```
spec.md  →  behavior.md  →  code       →  pr.md + doc.md
 (you)      (you + AI)      (you + AI)     (AI + you)
```

---

## Commands

The user interacts with SAGE using `/sage <command> [argument]`.

| Command | Argument | Reference file |
|---|---|---|
| `/sage spec <description>` | Feature description, ticket text, or idea | `references/spec.md` |
| `/sage behavior` | *(none — reads spec.md)* | `references/behavior.md` |
| `/sage code` | *(none — reads spec.md + behavior.md)* | `references/code.md` |
| `/sage update <feedback>` | Precise feedback tied to spec or behavior | `references/update.md` |
| `/sage pr` | *(none — reads full context)* | `references/pr.md` |
| `/sage doc` | *(none — reads full context)* | `references/doc.md` |
| `/sage harness init` | *(none — interactive wizard)* | `references/harness-init.md` |
| `/sage harness generate` | *(none — reads codebase files)* | `references/harness-generate.md` |
| `/sage harness review` | *(none — reads harness.md)* | `references/harness-review.md` |

---

## How to handle each command

When the user types a `/sage` command:

1. **Identify the sub-command** from the table above
2. **Read the corresponding reference file** — it contains the full prompt and instructions for that step
3. **Extract the inline argument** if provided (e.g. `/sage spec "Login screen with email and password"` → argument is `"Login screen with email and password"`)
4. **Execute the step** following the reference file instructions

If the user types `/sage` with no sub-command, show the command table above and ask which step they want to run.

---

## Prerequisite — the harness

Before running any SAGE step, check if `.sage/harness.md` (or `CLAUDE.md`, `.cursorrules`, or project knowledge) exists.

- **If it exists** — load it as context for all steps
- **If it doesn't exist** — remind the user once: *"No harness found. Run `/sage harness init` or `/sage harness generate` to set one up. I'll proceed without it for now."* Then continue.

---

## The ambiguity gate

`/sage behavior` is the most important step. It MUST:

1. Output `## Open Questions` first — every ambiguity found in spec.md
2. Output `## Test Cases` as a placeholder with a ⚠️ warning
3. **Stop and wait** for the user to resolve questions before finalizing test cases

Never skip open questions. Never generate test cases before questions are resolved.

---

## Reference files

Load the reference file for the active command. Each file contains the full prompt template and step-specific instructions.

- `references/spec.md` — how to generate spec.md from a description
- `references/behavior.md` — how to generate behavior.md with the ambiguity gate
- `references/code.md` — how to generate code from spec + behavior
- `references/update.md` — how to apply precise spec-anchored feedback
- `references/pr.md` — how to generate pr.md with ADR-style decisions
- `references/doc.md` — how to generate doc.md behavioral reference
- `references/harness-init.md` — interactive wizard to create harness.md
- `references/harness-generate.md` — AI-inferred harness from codebase
- `references/harness-review.md` — audit harness for drift or gaps
