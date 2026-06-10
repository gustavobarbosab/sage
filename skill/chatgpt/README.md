# SAGE — ChatGPT (Custom GPT)

`/sage` commands via a dedicated Custom GPT with SAGE built in.

## Install

1. Go to [chat.openai.com/gpts/editor](https://chat.openai.com/gpts/editor)
2. Click **Configure**
3. Copy the full contents of `custom-gpt-instructions.md` into the **Instructions** field
4. Set the name to **SAGE**
5. Optionally upload `harness.template.md` to **Knowledge**
6. Click **Save**

Your SAGE GPT is ready.

## Harness

**Option A — Upload to Knowledge (persistent):**
1. Fill in `harness.template.md` with your project conventions
2. In the GPT Editor → **Knowledge** → upload the filled-in file
3. The GPT will load it automatically in every conversation

**Option B — Paste at session start:**
1. Fill in `harness.template.md`
2. Paste the contents at the beginning of each new conversation

Or run `/sage harness init` inside the GPT to generate one interactively.  
Or start from [`../../templates/harness/android-compose.md`](../../templates/harness/android-compose.md).

## Usage

Open your SAGE GPT and type:

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
| `custom-gpt-instructions.md` | Paste into GPT Editor → Instructions |
| `harness.template.md` | Fill in and upload to GPT Knowledge (or paste at session start) |
