# Contributing to BalotaChain

Thanks for helping with BalotaChain and the underlying Tala framework. This
project is still early research-grade software, so contributions should make the
codebase clearer, safer, and easier to review.

## Goals

- Build an end-to-end verifiable voting application for BalotaChain.
- Grow Tala as reusable open-source cryptographic infrastructure.
- Keep protocol, implementation, and operational decisions reviewable.
- Favor correctness, auditability, and explicit tradeoffs over speed.

## Non-Goals

- Do not treat the current codebase as production-ready election software.
- Do not add deployment automation before the deployment model is designed.
- Do not merge cryptographic changes without clear references, tests, and
  review context.

## Prerequisites

Use stable toolchains unless a file in the repository pins a narrower version.

- Rust stable, with the repository minimum supported Rust version documented in
  `Cargo.toml` or `rust-toolchain.toml`.
- Go matching the `go` directive in `packages/tala-bulletin/go.mod`.
- Node.js matching `.nvmrc`, with pnpm managed through Corepack.
- Docker Desktop or Docker Engine for future Hyperledger Fabric development.
- Git and GitHub CLI for the branch and pull request workflow.

Platform-specific setup notes are in [docs/dev-environment.md](docs/dev-environment.md).

## Bootstrap

From a fresh clone:

```sh
git clone https://github.com/tala-blockchain/balotachain.git
cd balotachain
corepack enable
pnpm install
cargo test --workspace
cd packages/tala-bulletin && go test ./...
```

The repository is scaffolded before most packages have real implementations, so
some commands may initially exercise placeholder packages only.

## Test Commands

TypeScript:

```sh
pnpm lint
pnpm typecheck
pnpm test
pnpm build
```

Rust:

```sh
cargo fmt --check
cargo clippy --workspace --all-targets -- -D warnings
cargo test --workspace
cargo build --workspace
```

Go:

```sh
cd packages/tala-bulletin
gofmt -w .
go vet ./...
go test ./...
go build ./...
```

## Style

- Follow `.editorconfig` for whitespace and line endings.
- Use `cargo fmt` for Rust formatting.
- Use `gofmt` for Go formatting.
- Use Prettier and ESLint for TypeScript and Markdown where configured.
- Keep public cryptographic APIs small, documented, and testable.

## Commits

Use Conventional Commits:

```text
feat(scope): add trustee key share model
fix(ci): run cargo clippy on all targets
docs(adr): record workspace layout decision
```

Common scopes include `repo`, `ci`, `docs`, `crypto`, `credentials`,
`bulletin`, `protocol`, and `app`.

## Branch and Pull Request Workflow

1. Create a topic branch from `main`.
2. Keep each pull request focused on one issue or one coherent change.
3. Link related issues and ADRs in the pull request description.
4. Run the relevant checks before requesting review.
5. Include cryptographic or security notes when the change touches protocols,
   primitives, credentials, trustees, bulletin board behavior, or threat models.
6. Wait for review and required status checks before merge.

## Architectural Changes

Architectural decisions are captured as ADRs in `docs/adr/`. Write or update an
ADR when a change affects long-term structure, protocol choices, security
assumptions, major dependencies, or operational behavior. Start from
`docs/adr/template.md` and follow the process in `docs/adr/README.md`.

## Security Reports

Do not open public issues for vulnerabilities. Follow the private disclosure
process in [SECURITY.md](SECURITY.md).

