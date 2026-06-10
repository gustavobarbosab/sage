# SAGE — GitHub Copilot (VS Code)

`/sage` commands via Copilot Chat, using `copilot-instructions.md` and `.prompt.md` files.

## Install

```bash
# From the repo root
cp skill/copilot/.github/copilot-instructions.md /your/project/.github/
cp -r skill/copilot/.github/prompts /your/project/.github/
cp -r skill/copilot/.sage /your/project/
```

Make sure GitHub Copilot is enabled in VS Code and the `.github/` folder is at your project root.

## Harness

Fill in `.sage/harness.md` (copied above):

```bash
code .sage/harness.md
```

The harness is automatically referenced from `copilot-instructions.md` — Copilot will apply it to every interaction.

Or run `/sage harness init` in Copilot Chat to generate it interactively.  
Or start from [`../../templates/harness/android-compose.md`](../../templates/harness/android-compose.md).

## Usage

Open **Copilot Chat** in VS Code and type:

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
copilot/
├── .github/
│   ├── copilot-instructions.md  ← copy to your project .github/
│   └── prompts/                 ← copy to your project .github/prompts/
│       ├── sage-spec.prompt.md
│       ├── sage-behavior.prompt.md
│       ├── sage-code.prompt.md
│       ├── sage-update.prompt.md
│       ├── sage-pr.prompt.md
│       └── sage-doc.prompt.md
└── .sage/
    └── harness.md               ← harness placeholder — fill in your conventions
```
