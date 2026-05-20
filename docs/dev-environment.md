# Developer Environment

This guide describes the local setup expected for BalotaChain contributors. The
project is in early scaffold form, so install the toolchains now and expect more
package-specific commands to appear as implementation work lands.

## Version Policy

- Rust: use stable Rust. The MSRV is declared in `Cargo.toml` or
  `rust-toolchain.toml`.
- Go: use the version declared by `packages/tala-bulletin/go.mod`.
- Node.js: use the version declared in `.nvmrc`.
- pnpm: use the `packageManager` field in `package.json` through Corepack.
- Docker: use a current Docker Desktop or Docker Engine release capable of
  running Hyperledger Fabric containers.

## macOS

Install system tools:

```sh
xcode-select --install
brew install git gh node rustup go docker
rustup toolchain install stable
corepack enable
```

Docker Desktop is the simplest path for local Fabric work. Start Docker before
running any Fabric scripts.

## Linux

Install common prerequisites with your distribution package manager:

```sh
sudo apt-get update
sudo apt-get install -y build-essential curl git pkg-config libssl-dev
```

Install Rust with rustup, Node.js with your preferred version manager, and Go
from your package manager or the official tarball. Enable pnpm through Corepack:

```sh
rustup toolchain install stable
corepack enable
```

For Docker:

```sh
sudo usermod -aG docker "$USER"
```

Log out and back in after changing Docker group membership.

## Windows

Use WSL2 for development unless a future Windows-specific client task requires
native Windows tooling.

1. Install WSL2 with Ubuntu.
2. Install Docker Desktop and enable WSL integration.
3. Install Rust, Go, Node.js, pnpm through Corepack, Git, and GitHub CLI inside
   the WSL distribution.
4. Clone the repository inside the Linux filesystem, not under `/mnt/c`, for
   better file watching and build performance.

## Bootstrap Check

After cloning:

```sh
corepack enable
pnpm install
pnpm typecheck
cargo test --workspace
cd packages/tala-bulletin && go test ./...
```

If a toolchain is missing, run the bootstrap helper for a checklist:

```sh
./tools/bootstrap.sh
```

On Windows PowerShell:

```powershell
.\tools\bootstrap.ps1
```

## Tauri Prerequisites

The desktop client is not implemented yet. When Tauri work starts, install the
platform prerequisites before building the app.

- macOS: Xcode command line tools and WebKit dependencies provided by Tauri.
- Linux: WebKitGTK, OpenSSL, appindicator, librsvg, and build-essential
  packages required by Tauri.
- Windows: Microsoft C++ Build Tools and WebView2.

Keep Tauri-specific setup in this document as the desktop client design becomes
concrete.

## Hyperledger Fabric Local Network

The bulletin board package will target Hyperledger Fabric. Until the local
network scripts exist, prepare:

- Docker and Docker Compose.
- Fabric binaries and images matching the chosen Fabric release.
- A local workspace for chaincode package, install, approve, and commit flows.

Expected future workflow:

```sh
cd packages/tala-bulletin
go test ./...
# future: ./scripts/fabric-up.sh
# future: ./scripts/deploy-chaincode.sh
```

## Editor Configuration

Recommended editor support:

- EditorConfig support for whitespace rules.
- rust-analyzer for Rust.
- Go extension or gopls for Go.
- ESLint, Prettier, and TypeScript language service for TypeScript.
- Markdown linting for docs and ADRs.

Prefer repository settings over personal defaults when they differ.

