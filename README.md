# SAGE

> **S**pec · **A**ssert · **G**enerate · **E**xport

A lightweight, tool-agnostic workflow for AI-assisted development.  
Built on SDD, BDD, and Harness Engineering — with the principles of TDD and ADR woven in.

<img width="3780" height="1890" alt="SAGE-COVER" src="https://github.com/user-attachments/assets/6f3c714c-b7af-41c6-b7bc-645e5263be1c" />

---

## The principle

**Front-load the thinking, back-load the generation.**

<img width="2816" height="1536" alt="Gemini_Generated_Image_udhcloudhcloudhc" src="https://github.com/user-attachments/assets/662931a4-acdb-43b5-b4f3-f89199d5a10d" />


Most steps produce a concrete, committable Markdown file. Nothing lives only in the AI chat.

---

## Repository layout

```
sage/
├── commands/       # Prompt templates — copy-paste into any AI tool
├── skill/          # Packaged integrations per AI tool
│   ├── claude/     # Claude.ai .skill file
│   ├── claude-code/# Claude Code .claude/commands/
│   ├── cursor/     # .cursorrules + .cursor/rules/
│   ├── copilot/    # .github/copilot-instructions.md
│   ├── chatgpt/    # Custom GPT instructions
│   └── generic/    # Plain Markdown — works with any AI
├── templates/      # spec, behavior, pr, doc, and harness templates
└── docs/
    └── article.md  # The Medium post
```

---

## Quick start

### Option A — Any AI tool (copy-paste)

1. Grab a prompt from `commands/` and paste it into your AI assistant
2. See [`commands/README.md`](commands/README.md) for the full list

### Option B — Packaged integration per tool

Go to [`skill/README.md`](skill/README.md) and follow the install instructions for your tool:

| Tool | Folder | Install time |
|---|---|---|
| Claude Desktop | `skill/` (`.skill` file) | ~1 min |
| Claude Code | `skill/claude-code/` | ~1 min |
| Cursor | `skill/cursor/` | ~1 min |
| GitHub Copilot | `skill/copilot/` | ~2 min |
| ChatGPT | `skill/chatgpt/` | ~2 min |
| Any other AI | `skill/generic/` | ~1 min |

---

## How SAGE works

### Before any feature — the harness

A `.sage/harness.md` file that tells the AI your stack, conventions, and what to avoid.  
Set it up once, commit it, share it with your team.

```bash
/sage harness init       # new projects — interactive wizard
/sage harness generate   # existing projects — AI infers from codebase
```

### Step 1 — Spec

`/sage spec "Login screen with email and password"`

SAGE interviews you first — shows all questions upfront, waits for your answers, then generates `spec.md` and `behavior.md` together.

It also produces `behavior.md` with two mandatory sections:
- **Open Questions** — every ambiguity surfaced before any code is written
- **Test Cases** — BDD Given/When/Then scenarios (only after questions resolved)

This is the ambiguity gate: AI as requirements reviewer, not code generator.

### Step 2 — Generate

`/sage code`

Blocked until all open questions are resolved. Generates code that satisfies the behavioral contract.

### Step 3 — Export

`/sage pr` → `pr.md` with ADR-style decisions  
`/sage doc` → `doc.md` behavioral reference

---

## Roadmap

| Version | Contents | Status |
|---|---|---|
| v0.1 | `commands/` — copy-paste prompt templates | ✅ |
| v0.2 | `skill/` — packaged for Claude, Cursor, Copilot, ChatGPT | ✅ |
| v0.3 | `cli/` — Kotlin CLI with enforced gate logic | 🔜 |

---

## Contributing

Most valuable right now:
- Harness templates for other stacks (`templates/harness/`) — iOS/SwiftUI, Node, React, Python, Go
- Tool adaptations — Gemini, Windsurf, Zed, JetBrains AI
- Integration prompts — Jira MCP, Linear, Confluence, Notion, Obsidian

Open an issue first for bigger changes.

---

## License

MIT
