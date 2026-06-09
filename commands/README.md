# SAGE — Commands

Copy-paste prompt templates for any AI tool.  
No installation required — paste the prompt, run the command.

---

## Usage

1. Open the command file for the step you want to run
2. Copy the prompt inside
3. Paste it into your AI assistant
4. Follow the instructions

---

## Commands

| File | Command | What it does |
|---|---|---|
| `sage-spec.md` | `/sage spec <description>` | Interviews you, then generates `spec.md` + `behavior.md` |
| `sage-behavior.md` | `/sage behavior` | Regenerates `behavior.md` from existing `spec.md` |
| `sage-code.md` | `/sage code` | Generates code from `spec.md` + `behavior.md` |
| `sage-update.md` | `/sage update <feedback>` | Applies spec-anchored changes to generated code |
| `sage-pull-request.md` | `/sage pr` | Generates `pr.md` with ADR-style decisions |
| `sage-doc.md` | `/sage doc` | Generates `doc.md` behavioral reference |
| `sage-harness-init.md` | `/sage harness init` | Interactive wizard to create `.sage/harness.md` |
| `sage-harness-generate.md` | `/sage harness generate` | AI infers harness from your codebase |
| `sage-harness-review.md` | `/sage harness review` | Audits harness for drift or gaps |

---

## The harness

Before running any command, set up your harness — the context block that tells the AI your stack and conventions.

```
/sage harness init       ← new project
/sage harness generate   ← existing codebase
```

Save the result as `.sage/harness.md` in your project root and paste it at the start of every session.

---

## Tip

For a better experience with persistent harness and native slash commands, see the packaged integrations in [`../skill/`](../skill/README.md).
