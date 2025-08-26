# TypeScript Copilot Instructions

## Scope
These rules apply to any TypeScript/JavaScript, Node.js, and VS Code Extension code in this repo.

## Language Conventions
- Follow standard TypeScript conventions and strict typing
  - Enable `strict`, `noImplicitAny`, `noUnusedLocals`, `noUnusedParameters`
  - Prefer `unknown` over `any`; narrow types explicitly
- Use modern ES modules, `async/await`, and `for..of` over callbacks and `forEach` where appropriate
- Prefer composition over inheritance; keep classes small

## Project Structure
- Keep `src/` for source, `tests/` for unit tests; co-locate test files with the unit under test when practical (`*.test.ts`)
- Public APIs go through an index barrel; avoid deep imports across packages

## Error Handling
- Never swallow errors; wrap with context using `Error` or libraries like `errcause`
- For async functions, prefer `Result`-like patterns or typed error objects where appropriate
- Surface user-facing errors with actionable messages

## Testing (vitest)
- Use `vitest` for unit tests; cover happy path and at least one edge case
- Mock I/O and network boundaries; avoid real timers and sleeps
- Keep tests deterministic; avoid relying on system time or env unless injected

## Tooling
- Lint with ESLint + `@typescript-eslint` and Prettier; ensure zero lint errors
- Use `tsup`/`tsc` for builds; generate declaration files where needed

## Performance & UX
- Optimize hot paths and extension activation time; use lazy imports
- Avoid blocking the event loop; offload heavy work to workers or subprocesses

## Security & Privacy
- Do not log secrets or PII; redact sensitive fields
- Validate all inputs at boundaries (IPC/HTTP); use zod or similar for schemas

## Sample Checklist (PR-ready)
- [ ] Types are precise and `any` is avoided
- [ ] Errors carry context and are handled
- [ ] Tests added/updated and pass locally with vitest
- [ ] Lint/type-check pass with no warnings
- [ ] Public API documented (JSDoc) and stable
