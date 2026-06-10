# SAGE — Claude.ai

Native `/sage` slash commands installed as a Claude Skill.

## Install

1. Download `sage.skill`
2. Go to **Claude.ai → Settings → Skills → Install skill**
3. Upload `sage.skill`

Done. `/sage` commands are now available in any conversation.

## Harness

Add your harness as **project knowledge** in a Claude Project:

1. Go to **Claude.ai → Projects → Your Project → Project Knowledge**
2. Upload or paste your `.sage/harness.md`
3. Claude loads it automatically in every conversation in that project

Use `/sage harness init` to generate a harness interactively, or start from [`../../templates/harness/android-compose.md`](../../templates/harness/android-compose.md).

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

| File | Purpose |
|---|---|
| `sage.skill` | Upload this to Claude.ai Settings → Skills |
| `SKILL.md` | Skill entry point — dispatches to reference files |
| `references/` | Per-command prompt logic, loaded on demand |
