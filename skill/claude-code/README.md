# SAGE — Claude Code

Native `/sage` commands available in every Claude Code session for the project.

## Install

Copy the `.claude/` folder into your project root:

```bash
cp -r skill/claude-code/.claude /your/project/
```

That's it. Open Claude Code in your project and `/sage` is ready.

## Harness

Save your harness as `CLAUDE.md` at your project root (Claude Code loads it automatically):

```bash
cp ../../templates/harness/android-compose.md /your/project/CLAUDE.md
# Fill in your project-specific conventions
```

Or run `/sage harness init` inside a Claude Code session to generate it interactively.

## Usage

```
/sage harness init
/sage spec "Login screen with email and password"
/sage behavior
/sage code
/sage update "spec item 3 violated — navigation inside ViewModel"
/sage pr
/sage doc
```

## Files

```
claude-code/
└── .claude/
    └── commands/
        ├── sage.md          ← entry point — copy to your project
        └── sage/            ← per-command reference files
            ├── spec.md
            ├── behavior.md
            ├── code.md
            ├── update.md
            ├── pr.md
            ├── doc.md
            ├── harness-init.md
            ├── harness-generate.md
            └── harness-review.md
```
