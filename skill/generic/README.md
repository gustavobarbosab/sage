# SAGE — Generic (Any AI)

Works with any AI assistant — Gemini, Mistral, Perplexity, LLaMA, or anything else that follows instructions.

## Install

No installation needed. Just copy the files somewhere accessible:

```bash
cp skill/generic/sage-session-prompt.md ~/prompts/
cp skill/generic/harness.template.md ~/prompts/
```

## Harness

1. Fill in `harness.template.md` with your project conventions
2. Open `sage-session-prompt.md`
3. Replace the `[PASTE YOUR .sage/harness.md CONTENT HERE]` placeholder with your harness content
4. Save the combined file

Or run `/sage harness init` at the start of a session to generate one interactively.  
Or start from [`../../templates/harness/android-compose.md`](../../templates/harness/android-compose.md).

## Usage

At the start of every session:

1. Paste the full contents of `sage-session-prompt.md` (with harness filled in)
2. Run `/sage` commands normally:

```
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
| `sage-session-prompt.md` | Paste at the start of every session |
| `harness.template.md` | Fill in and embed into `sage-session-prompt.md` |

## Tip

If your AI tool supports saved system prompts or persistent instructions, paste `sage-session-prompt.md` there so you don't have to repeat it every session.
