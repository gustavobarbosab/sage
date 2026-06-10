# AI Coding Workflow: SDD, BDD, and Harness Engineering, Stitched Together

> A lightweight workflow built on SDD, BDD, and Harness Engineering — with the principles of TDD and ADR woven in.

---

## The problem I kept running into

For months, my workflow with AI looked like this: open Claude, paste a Jira ticket, ask for code, spend the next hour rewriting most of it.

The output compiled. Sometimes it even worked. But it never matched my project conventions. The ViewModels looked wrong, the navigation used patterns we'd abandoned, the tests were generic and missed edge cases that the AI couldn't have known about because I never told it.

Worse, the *behavior* was often wrong — not because the AI failed, but because I never clearly defined what I wanted in the first place. Vague tickets became vague prompts, which became vague code, which became a back-and-forth I should have avoided with 10 minutes of upfront thinking.

So I started experimenting with a more structured approach. What follows is what I landed on — a way of working with AI built on practices that have existed for years, applied to this new context.

---

## The practices I stitched together

The workflow combines a few practices that already existed, applied in a specific order:

**Spec-Driven Development (SDD)** — the specification is the single source of truth. Everything derives from it. This is a well-established practice with mature tools like GitHub Spec Kit, AWS Kiro, and BMAD-METHOD that I'll mention later.

**Behavior-Driven Development (BDD)** — express behaviors in human-readable Given/When/Then scenarios that both developers and non-technical stakeholders can understand.

**Harness Engineering** — give the AI structured context about your environment (stack, conventions, what to avoid) before any generation happens.

Two more practices show up as principles, not full implementations:

**Test-Driven Development (TDD)** — I don't follow the Red/Green/Refactor loop. But I do apply TDD's core principle: *define expected behavior before writing the implementation*. In my workflow, behavior scenarios are written before any code exists, and the code is generated to satisfy them. That's TDD's spirit applied to AI-assisted development, not classic TDD.

**Architecture Decision Records (ADR)** — I don't maintain a separate ADR log. But every behavioral decision resolved during the workflow gets captured automatically in the final documentation, with the reasoning preserved. That's ADR's spirit embedded in the artifact chain.

These practices come together under one principle: **front-load the thinking, back-load the generation.**

The four steps form a useful acronym: SAGE — *Spec, Assert, Generate, Export*.

```
spec.md  →  behavior.md  →  code       →  pr.md + doc.md
 (you)      (you + AI)      (you + AI)     (AI + you)
```

Most steps produce a concrete, committable Markdown file — the only exception is the code generation itself, which produces your actual implementation. Nothing lives only in the AI chat. Human involvement decreases as you move right — more *thinking* in the early steps, more *reviewing* in the later ones.

---

## Before any feature — the harness

Before working on any feature, my project has a harness: a reusable context block that tells the AI my stack, conventions, and what to avoid.

This isn't a step in the workflow. It's infrastructure — like a `.editorconfig` or `build.gradle`. I set it up once and share it with my team:

- **Claude Projects** — added as project knowledge so it's always in context
- **Cursor** — saved as `.cursorrules` at the repo root
- **Claude Code** — saved as `CLAUDE.md` for persistent loading
- **Any other tool** — pasted at the start of every session

Here's what mine looks like for an Android project:

```markdown
## Project Harness — NexAuth Android

### Stack
- Kotlin 2.0, Jetpack Compose (BOM 2024.06)
- Hilt for DI
- MVI: UiState sealed class + UiEvent channel in ViewModel
- Navigation: lambda callbacks (onLoginSuccess: () -> Unit)
- No LiveData, no XML views

### Conventions
- ViewModel exposes: uiState: StateFlow<ScreenUiState>
- UiState is a sealed interface with Loading, Idle, Error
- Composables receive state + callbacks only — no VM reference
- Previews required for each state variant

### Avoid
- viewModelScope.launch inside composables
- Hardcoded strings (use stringResource)
- Material2 imports (Material3 only)
- Exposing domain-level exceptions to the UI layer
```

Once the harness exists, every AI interaction speaks my dialect from line one. This is Harness Engineering in practice.

---

## Step 1 — Spec

The first thing I do for any feature is write a `spec.md`. This is SDD in action — the single source of truth that drives everything downstream.

A good spec has four parts: what the feature does, inputs and outputs, acceptance criteria, and explicit out-of-scope boundaries.

```markdown
## Feature: LoginScreen

### What it does
Allows the user to authenticate using email and password.
Displays validation errors inline and a loading state during
the auth request.

### Inputs
- email: String
- password: String

### Outputs
- onLoginSuccess(): navigates to HomeScreen
- onForgotPassword(): navigates to ForgotPasswordScreen

### Acceptance criteria
- Email field shows error if format is invalid
- Password field shows error if empty on submit
- Loading indicator shown while request is in progress
- Generic error message shown on auth failure (no details leaked)
- "Forgot password?" link visible below the password field

### Do NOT
- Perform any network call directly in the composable
- Store credentials in local state beyond the current session
- Navigate inside the ViewModel
```

It takes 5 minutes. But it eliminates 80% of the back-and-forth that used to happen mid-implementation. The act of writing it surfaces ambiguities before they become bugs.

---

## Step 2 — Assert behavior

This is the step that changed my workflow the most. Instead of going from spec to code, I ask the AI to produce a `behavior.md` first — with two mandatory sections: **Open Questions** and **Test Cases**.

```markdown
## Open Questions
- [ ] Should a network timeout and wrong credentials show
      the same error message, or different ones?
- [ ] Is email format validation triggered on-the-fly as
      the user types, or only on submit?
- [ ] If the user taps submit twice rapidly while loading,
      should the second tap be silently ignored or show feedback?

## Test Cases
> ⚠️ Pending resolution of open questions above.
```

**The AI stops here and waits.**

This is the part that made the biggest difference. Before a single line of code is written, the AI surfaces the exact questions that used to cause back-and-forth with my tech lead mid-PR — or worse, bugs in production.

This reframes how I think about AI. Most developers use it as a code generator. I started using it first as a **requirements reviewer** — something that stress-tests my understanding of the feature before any implementation decision is made. The AI isn't just writing tests; it's clarifying my ticket.

I resolve each question, update `spec.md` if needed, and give the AI the go-ahead. Only then does it finalize the test cases — using BDD Given/When/Then scenarios. Each one is presented in a short version for quick scanning and a full version for precise implementation guidance. This is also where TDD's *spirit* comes in — defining the expected behavior before writing any implementation, even though the loop itself isn't classic Red/Green/Refactor.

```markdown
## Test Cases

### Happy path

**Scenario: Successful login**
Short → Valid credentials + submit → Loading shown → Navigate to HomeScreen
Full:
- Given the user has entered a valid email and password
- When they tap the submit button
- Then the loading indicator is shown
- And they are navigated to HomeScreen

### Validation

**Scenario: Invalid email format**
Short → Invalid email + submit → Inline email error shown
Full:
- Given the user has entered an email with an invalid format
- When they tap the submit button
- Then an inline error is shown below the email field
- And no network request is made

### Edge cases

**Scenario: Double submit during loading**
Short → Loading state + second submit tap → Second tap ignored
Full:
- Given the screen is in the loading state
- When the user taps the submit button again
- Then the second tap is silently ignored
- And no duplicate auth request is made

### Error handling

**Scenario: Wrong credentials**
Short → Wrong credentials + submit → Generic error message shown
Full:
- Given the user has entered incorrect credentials
- When they tap the submit button
- Then a generic error message is displayed
- And no specific reason is given to avoid leaking account information
```

The behavioral contract is now explicit, human-readable, and committed to the repo — before implementation begins.

---

## Step 3 — Generate

Now the code generation starts. But unlike a blind prompt, the AI has full context: the harness, the spec, and a behavioral contract with explicit scenarios to satisfy. The code is written to make the behavior pass — that's the TDD spirit, applied at the AI prompting level.

When everything is resolved, the AI generates:

```
1. LoginUiState (sealed interface: Idle, Loading, Error)
2. LoginViewModel with submitLogin(email, password)
3. LoginScreen composable with all acceptance criteria implemented
4. Unit tests covering all scenarios in behavior.md
5. Previews for each state variant
```

I review the output against the spec — not my gut. The acceptance criteria become the checklist. If something's off, I give precise feedback tied to the spec, not vague impressions.

---

## Step 4 — Export

Once the code is commit-ready, the AI generates two final artifacts from the full context — spec, behavior decisions, resolved questions, and code:

**`pr.md`** — ready to paste into the PR, with a decisions section that captures every resolved open question with its reasoning (this is where the ADR spirit shows up):

```markdown
## Login screen implementation

Implements the LoginScreen feature per spec.md.

### Changes
- LoginUiState sealed interface (Idle, Loading, Error)
- LoginViewModel with email/password validation
- LoginScreen composable with all acceptance criteria
- Unit tests covering all scenarios in behavior.md

### Decisions (ADR-style)
- Timeout and wrong credentials show the same generic error
  → Avoids leaking information about account existence
- Email validation triggers only on submit, not on-the-fly
  → Reduces noise during input, aligns with mobile UX conventions
- Rapid double-submit during loading is silently ignored
  → Prevents duplicate auth requests
```

**`doc.md`** — behavioral reference for the team, with edge cases, decisions, and out-of-scope items explicitly documented:

```markdown
## LoginScreen — Behavior Reference

### Supported states
- Idle: initial state, form is editable
- Loading: triggered on submit, form is disabled
- Error: shown on auth failure, form re-enabled for retry

### Edge cases
- Double submit during loading: second tap ignored silently
- Network timeout: treated identically to wrong credentials
- Back navigation during loading: allowed, request is cancelled

### Decisions
- Generic error for all auth failures → prevents account enumeration
- Submit-only validation → better mobile UX, less interruption

### Out of scope
- Biometric authentication
- Remember me / persistent session
- Social login providers
```

Any engineer can open `doc.md` six months later and understand not just *what* the screen does, but *why* it works the way it does.

---

## Connecting it to existing tools

The artifact chain plugs naturally into the tools you already use — turning a local practice into a fully integrated pipeline:

A Jira ticket lands in the backlog. Instead of writing `spec.md` from scratch, the Jira MCP pulls the ticket context — title, description, acceptance criteria — and the AI generates a structured spec from it. The blank page problem disappears.

During code generation, Context7 gives the AI up-to-date documentation for the libraries in the harness, so the output uses current APIs instead of whatever was in the model's training data.

After the code is ready, the GitHub CLI takes the content from `pr.md` and opens the PR directly. After the feature ships, `doc.md` gets published to Confluence, Notion, or wherever the team's knowledge base lives, via the appropriate MCP.

```
Jira  →  spec.md  →  behavior.md  →  code  →  pr.md + doc.md  →  GitHub + Confluence
```

None of this is required. But it shows where the artifact chain naturally leads — AI participating in the entire feature lifecycle, not just the code generation moment.

---

## Why it works

**It front-loads the thinking.** The steps requiring the most judgment happen before any code exists, when changes cost nothing.

**It combines proven practices.** SDD, BDD, and Harness Engineering each solved a real problem. The TDD and ADR principles fill the gaps. Combining them with AI as connective tissue makes each one cheaper to apply than it used to be.

**It turns AI into a requirements reviewer.** The open questions step catches gaps that would have surfaced later as bugs or PR comments. The AI consistently surfaces things worth thinking about before the code exists.

**Everything is diffable.** All artifacts are Markdown files in the repo. Teams can review `behavior.md` in a PR, track how `spec.md` evolved, and read `doc.md` six months later without reconstructing intent from code.

---

## Where this fits in the SDD landscape

Spec-driven development took off in 2025-2026, and several mature tools now exist in this space:

- **GitHub Spec Kit** — the most adopted open-source SDD CLI, with a four-command workflow and a "constitution" file that's essentially the same idea as a harness
- **AWS Kiro** — a full IDE built around spec-driven workflows, with EARS notation for acceptance criteria and agent hooks for automation
- **BMAD-METHOD** — a multi-agent framework that orchestrates 12+ specialized AI agents across the full SDLC
- **Claude Code with CLAUDE.md** — Anthropic's approach to persistent project context, very close to the harness concept
- **OpenSpec** — focused on brownfield iteration with proposal-first workflows

What I've described is a lightweight approach that works for both personal projects and bigger ones, without committing to a heavier framework. It's just structured prompts and Markdown files — no CLI to install, no IDE to switch to, no multi-agent orchestration to configure. If you eventually need the rigor of a full framework, the practices you build here transfer naturally. But you don't need to start there.

---

## Trying it yourself

The prompts I use are in a [repository](https://github.com/your-username/sage) so anyone can apply the same workflow. They're tool-agnostic — Markdown files you can drop into Claude Projects, Cursor rules, Claude Code's command files, or paste manually into any AI assistant.

Start with just the spec and behavior steps. Write a `spec.md` for your next feature. Ask the AI to surface open questions before writing tests. Resolve them before any code gets generated.

That alone changes how the workflow feels. The rest compounds from there.

Whatever tool you reach for — these prompts, Spec Kit, Kiro, or Claude Code — the shift that matters is the same: stop treating AI as an autocomplete. Start treating it as a thinking partner that needs structure to think with you.

---

*Structure your context. Define your behavior. Generate with confidence.*

---

**Tags:** `Android Development` · `Artificial Intelligence` · `Software Engineering` · `Developer Productivity` · `Spec Driven Development`
