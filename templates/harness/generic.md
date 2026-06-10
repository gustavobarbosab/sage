## Project Harness — Generic Template

> Copy this file and replace each section with your project's specifics.
> Delete sections that don't apply, add ones that do.

### Stack
- Language: <e.g. TypeScript 5.4>
- Framework/Runtime: <e.g. Node.js 22, React 18>
- Dependency injection: <e.g. Inversify, manual, none>
- State management: <e.g. Zustand, Redux Toolkit>
- Async: <e.g. async/await, RxJS>
- Networking: <e.g. fetch, axios>
- Persistence: <e.g. Prisma + PostgreSQL>
- Other key libraries: <list>

### Conventions

**Architecture**
- <e.g. Layered: routes → services → repositories>
- <Folder structure rules>

**Naming**
- Files: <e.g. kebab-case, .ts extension>
- Classes/types: <e.g. PascalCase>
- Functions: <e.g. camelCase>
- Test files: <e.g. *.test.ts colocated with source>
- Test naming: <e.g. it('should X when Y given Z')>

**Patterns**
- <e.g. Error handling via Result<T, E> types, no thrown exceptions in domain>
- <e.g. All API endpoints return discriminated unions>
- <e.g. Dependencies passed as constructor args, not imported>

### Test framework
- <e.g. Vitest + Testing Library + MSW>
- <Assertion style preferences>

### Avoid
- <Anti-pattern 1>
- <Deprecated API or library>
- <Pattern the team has explicitly moved away from>
- <Anything that has caused bugs in the past>

### Project-specific rules
- <Rules unique to this codebase>
- <Constraints from external systems>
