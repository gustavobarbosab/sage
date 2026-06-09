# SAGE — Skill Integrations

Packaged integrations for each AI tool. Pick the one that fits your setup.

---

## Claude.ai

**What you get:** Native `/sage` slash commands + harness as project knowledge.

**Install:**
1. Download `sage.skill`
2. Go to **Claude.ai → Settings → Skills → Install skill**
3. Upload `sage.skill`

**Harness:** Add `.sage/harness.md` as project knowledge in your Claude Project.

**Use:**
```
/sage harness init
/sage spec "Login screen with email and password"
/sage behavior
/sage code
/sage pr
/sage doc
```

---

## Claude Code

**What you get:** `/sage` commands available in every Claude Code session for the project.

**Install:**
```bash
# From the repo root, copy into your project
cp -r skill/claude-code/.claude /your/project/
```

**Harness:** Save as `CLAUDE.md` or `.sage/harness.md` at your project root.

**Use:** Same `/sage` commands in any Claude Code session for that project.

---

## Cursor

**What you get:** `@sage` commands via `.cursorrules` or modular `.mdc` rules.

**Install — Option A (single file, simpler):**
```bash
cp skill/cursor/.cursorrules /your/project/
cp -r skill/cursor/.sage /your/project/
```

**Install — Option B (modular, modern Cursor format):**
```bash
cp -r skill/cursor/.cursor /your/project/
cp -r skill/cursor/.sage /your/project/
```

**Harness:** Fill in `.sage/harness.md` (copied above) with your project conventions.  
Or run `@sage harness init` to generate it interactively.

**Use:** `@sage spec "Login screen"`, `@sage behavior`, `@sage code`, etc.

---

## GitHub Copilot (VS Code)

**What you get:** `/sage` commands via Copilot Chat, with prompt files for each step.

**Install:**
```bash
cp skill/copilot/.github/copilot-instructions.md /your/project/.github/
cp -r skill/copilot/.github/prompts /your/project/.github/
cp -r skill/copilot/.sage /your/project/
```

**Harness:** Fill in `.sage/harness.md` with your project conventions.  
The harness is automatically referenced from `copilot-instructions.md`.

**Use:** Type `/sage spec "Login screen"` in Copilot Chat.

---

## ChatGPT (Custom GPT)

**What you get:** A dedicated SAGE GPT with all commands built in.

**Install:**
1. Go to [chat.openai.com/gpts/editor](https://chat.openai.com/gpts/editor)
2. Click **Configure**
3. Copy the contents of `skill/chatgpt/custom-gpt-instructions.md` into **Instructions**
4. Name it **SAGE** and save
5. Optionally upload `skill/chatgpt/harness.template.md` to **Knowledge**

**Harness:** Upload your filled-in `harness.md` to the GPT's Knowledge files,  
or paste it at the start of each session.

**Use:** `/sage spec "Login screen"` in your SAGE GPT.

---

## Any other AI (generic)

**What you get:** A single prompt file that works with Gemini, Mistral, Perplexity, or any AI that follows instructions.

**Install:**
```bash
cp skill/generic/sage-session-prompt.md ~/your-prompts/
cp skill/generic/harness.template.md ~/your-prompts/
```

**Harness:** Fill in `harness.template.md`, then paste its content into `sage-session-prompt.md` where indicated.

**Use:**
1. Paste `sage-session-prompt.md` at the start of every session
2. Run `/sage` commands normally

---

## Compatibility

| Feature | Claude.ai | Claude Code | Cursor | Copilot | ChatGPT | Generic |
|---|---|---|---|---|---|---|
| `/sage spec` interview | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `/sage behavior` ambiguity gate | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `/sage code` gate enforcement | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `/sage pr` + `/sage doc` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `/sage harness *` | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Native slash commands | ✅ | ✅ | ✅ | ✅ | ❌ | ❌ |
| Persistent harness | ✅ | ✅ | ✅ | ✅ | ⚠️ upload | ⚠️ paste |

---

## Harness location by tool

| Tool | Harness location |
|---|---|
| Claude.ai | Project knowledge |
| Claude Code | `CLAUDE.md` or `.sage/harness.md` |
| Cursor | `.sage/harness.md` |
| Copilot | `.sage/harness.md` |
| ChatGPT | GPT Knowledge file or pasted at session start |
| Generic | Pasted at session start |

---

## File reference

```
skill/
├── README.md                          ← this file
├── sage.skill                         ← Claude.ai install file
├── SKILL.md                           ← skill entry point (Claude format)
├── references/                        ← shared prompt logic for all tools
│   ├── spec.md
│   ├── behavior.md
│   ├── code.md
│   ├── update.md
│   ├── pr.md
│   ├── doc.md
│   ├── harness-init.md
│   ├── harness-generate.md
│   └── harness-review.md
├── claude-code/
│   └── .claude/commands/              ← copy to your project root
│       ├── sage.md
│       └── sage/
├── cursor/
│   ├── .cursorrules                   ← Option A: single file
│   ├── .cursor/rules/                 ← Option B: modular .mdc files
│   └── .sage/harness.md              ← harness placeholder
├── copilot/
│   ├── .github/copilot-instructions.md
│   ├── .github/prompts/              ← prompt files per command
│   └── .sage/harness.md
├── chatgpt/
│   ├── custom-gpt-instructions.md    ← paste into GPT Editor
│   └── harness.template.md
└── generic/
    ├── sage-session-prompt.md        ← paste at session start
    └── harness.template.md
```
