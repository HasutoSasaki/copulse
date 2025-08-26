# Go Copilot Instructions

## Scope
These rules apply to all Go code in this repo, including CLI, services, and libraries.

## Language Conventions
- Follow Effective Go and Go Code Review Comments
- Package names are short, lower_case, no stutter (`p2p`, not `p2ppackage`)
- Keep exported API minimal; prefer unexported symbols when possible

## Project Structure
- One concern per package; avoid cyclic deps
- `cmd/<appname>/main.go` for binaries; keep `main` thin
- Use `internal/` for non-public packages

## Error Handling
- Return `error` as the last return value; wrap with `%w` using `fmt.Errorf`
- Prefer sentinel errors or `errors.Is/As` for classification
- Do not panic in library code; use panic only in `main` for truly unrecoverable states

## Concurrency
- Prefer context-aware functions: `func(ctx context.Context, ...)`
- Always respect `ctx.Done()` and propagate cancellations/timeouts
- Avoid goroutine leaks; document ownership of goroutines and channels

## Testing
- Use `testing` and table-driven tests; cover success and failure cases
- Use `t.Helper()`, `t.Parallel()` where safe
- Avoid time-based flakes; use fakes and deterministic inputs

## Tooling
- `go mod tidy` on changes; pin tools via `tools.go` if needed
- Lint with `golangci-lint` (vet, staticcheck, ineffassign, govet, revive)

## Performance & Reliability
- Prefer `[]byte` over `string` for I/O hot paths; reuse buffers with `sync.Pool` when justified
- Keep allocations low; benchmark with `testing.B`
- Add backpressure to networked components; set read/write deadlines

## Security & Privacy
- Zero sensitive memory when possible; avoid logging secrets
- Validate all inputs at boundaries (HTTP/IPC/P2P)

## Sample Checklist (PR-ready)
- [ ] Public API is minimal and documented
- [ ] Errors are wrapped and classified
- [ ] Context is passed and respected
- [ ] Tests added/updated and all pass (`go test ./...`)
- [ ] Lint passes with no warnings
