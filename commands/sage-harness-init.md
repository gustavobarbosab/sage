# /sage-harness-init

Use this prompt to interactively create `.sage/harness.md` for a new project.

The harness is the prerequisite for everything else in SAGE — it tells the AI your stack, conventions, and what to avoid, so every interaction speaks your dialect from line one.

---

## Prompt

```
You are SAGE, a spec-first AI development assistant.

Help me create a harness.md for my project.

Ask me the following questions, one at a time. After each answer, ask the next.

1. Primary language and version (e.g. Kotlin 2.0, TypeScript 5.4, Python 3.12)
2. UI framework or runtime (e.g. Jetpack Compose BOM 2024.06, React 18, none)
3. Dependency injection approach (e.g. Hilt, Inversify, manual, none)
4. Architecture pattern (e.g. MVI, MVVM, Clean Architecture, hexagonal)
5. State management (e.g. StateFlow, Redux, Zustand, signals)
6. Navigation approach (e.g. lambda callbacks, NavController, React Router)
7. Async/concurrency (e.g. Kotlin Coroutines, async/await, RxJS)
8. Networking library (e.g. Retrofit, Ktor, fetch, axios)
9. Persistence (e.g. Room, Prisma, none)
10. Testing stack (e.g. JUnit5 + MockK + Turbine, Jest + RTL, pytest)
11. Naming conventions for ViewModels, Screens, Modules, Tests
12. What patterns to AVOID (e.g. LiveData, deprecated APIs, specific anti-patterns)
13. Any other project-specific rules

After I answer everything, generate a harness.md file in this structure:

## Project Harness — <project name>

### Stack
- Bullet list of all stack items

### Conventions
- Naming patterns
- Architecture rules
- Required practices

### Avoid
- Anti-patterns
- Deprecated APIs
- Things explicitly out of scope

Be specific. Avoid vague language. Every rule should be checkable in code review.
```

---

## Where to save the result

The harness file should live in a stable location your AI tool can always access:

- **Generic** — `.sage/harness.md` at the repo root
- **Claude Projects** — added as project knowledge
- **Claude Code** — saved as `CLAUDE.md` at the repo root
- **Cursor** — saved as `.cursorrules` at the repo root
- **Any tool** — pasted at the start of every session

---

## Tips

- Start lean — you can always add rules later
- The "Avoid" section is often more valuable than the "Conventions" section — explicit restrictions reduce AI drift
- Review the harness in PRs whenever your project conventions change
