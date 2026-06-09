# /sage harness init

Creates `.sage/harness.md` via an interactive wizard.

## Instructions

Ask the user the following questions one at a time. Wait for each answer before asking the next.

1. *"What's your primary language and version? (e.g. Kotlin 2.0, TypeScript 5.4)"*
2. *"What UI framework or runtime are you using? (e.g. Jetpack Compose BOM 2024.06, React 18, none)"*
3. *"How do you handle dependency injection? (e.g. Hilt, Inversify, manual, none)"*
4. *"What architecture pattern do you follow? (e.g. MVI, MVVM, Clean Architecture)"*
5. *"How do you manage state? (e.g. StateFlow, Redux, Zustand, signals)"*
6. *"How does navigation work? (e.g. lambda callbacks, NavController, React Router)"*
7. *"What's your async/concurrency approach? (e.g. Kotlin Coroutines + Flow, async/await)"*
8. *"What test framework do you use? (e.g. JUnit5 + MockK + Turbine, Jest + RTL)"*
9. *"What naming conventions do you follow for key files? (e.g. ViewModels, Screens, Tests)"*
10. *"What should I avoid? (e.g. LiveData, XML views, Material2, hardcoded strings)"*
11. *"Anything else I should always know about this project?"*

After collecting all answers, generate `.sage/harness.md`:

```markdown
## Project Harness — <project name>

### Stack
- <bullet list of stack items>

### Conventions
- <naming patterns>
- <architecture rules>
- <required practices>

### Avoid
- <anti-patterns>
- <deprecated APIs>
- <things explicitly out of scope>
```

---

## Rules

- Every rule must be checkable in code review — no vague guidance
- The "Avoid" section is often more valuable than "Conventions"
- Start lean — the harness can always be extended later
- Save to `.sage/harness.md` at the project root

---

## After generation

Tell the user:
*"Harness saved to `.sage/harness.md`. Commit it to version control so your whole team shares the same conventions. Run `/sage harness review` periodically to catch drift. Now run `/sage spec <feature description>` to start your first feature."*
