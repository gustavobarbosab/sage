# SAGE — Cursor

`@sage` commands via `.cursorrules` (simple) or `.cursor/rules/` (modular).

## Install

### Option A — Single file (simpler)

```bash
cp skill/cursor/.cursorrules /your/project/
cp -r skill/cursor/.sage /your/project/
```

### Option B — Modular rules (modern Cursor format)

```bash
cp -r skill/cursor/.cursor /your/project/
cp -r skill/cursor/.sage /your/project/
```

Both options work. Option A is simpler. Option B gives you per-command rule files you can enable/disable individually.

## Harness

Fill in `.sage/harness.md` (copied with either option above):

```bash
# Open and edit
code .sage/harness.md
```

Or run `@sage harness init` in Cursor Chat to generate it interactively.  
Or start from [`../../templates/harness/android-compose.md`](../../templates/harness/android-compose.md).

## Usage

In Cursor Chat:

```
@sage harness init
@sage spec "Login screen with email and password"
@sage behavior
@sage code
@sage update "spec item 3 violated — navigation inside ViewModel"
@sage pr
@sage doc
```

## Files

```
cursor/
├── .cursorrules                  ← Option A: copy to project root
├── .sage/
│   └── harness.md               ← harness placeholder — fill in your conventions
└── .cursor/
    └── rules/                   ← Option B: copy to project root
        ├── sage.mdc             ← entry point
        ├── sage-spec.mdc
        ├── sage-behavior.mdc
        ├── sage-code.mdc
        ├── sage-update.mdc
        ├── sage-pr.mdc
        ├── sage-doc.mdc
        ├── sage-harness-init.mdc
        ├── sage-harness-generate.mdc
        └── sage-harness-review.mdc
```
