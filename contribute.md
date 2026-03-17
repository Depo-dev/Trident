# Contributing to Trident

Trident is pre-launch infrastructure. The codebase isn't public yet, but contributors who get involved now shape the project from the ground up — architecture, API design, developer experience, all of it.

---

### Getting Set Up

Prerequisites:
- Rust (stable toolchain via [rustup](https://rustup.rs))
- Node.js 20 LTS (for the TypeScript SDK)
- Docker + Docker Compose v2
- PostgreSQL 15+ (or just use the Docker setup)

```bash
git clone https://github.com/trident-build/trident.git
cd trident
cp .env.example .env
docker compose -f docker/docker-compose.dev.yml up -d
cargo build
```

Full setup instructions will live in [`docs/development.md`](./docs/development.md) once the repo is scaffolded.

---

### How the Repo Is Structured

```
trident/
├── crates/
│   ├── indexer/        # Core Rust indexer — streamer + parser
│   ├── api/            # REST + GraphQL API server (Axum)
│   └── common/         # Shared types, error handling, config
├── sdk/
│   └── typescript/     # TypeScript SDK (@trident-indexer/sdk)
├── database/
│   ├── schema.sql      # Canonical PostgreSQL schema
│   └── migrations/     # Versioned migration files
├── docker/             # Compose files for dev and production
└── docs/               # Specification and technical documentation
```

The indexer and API are separate Rust crates. They share types through `common` but are independently deployable. The TypeScript SDK is a pure client — it talks to the API, it doesn't touch the database or the Rust code directly.

---

### Workflow

**Before writing code for anything non-trivial, open an issue first.** This prevents duplicate work and makes sure your approach aligns with where the project is heading. Comment on the issue to claim it.

**Branches:**

```
main          → stable, tagged releases only
dev           → integration branch, PRs target this
feature/NNN-short-description
fix/NNN-short-description
docs/short-description
```

**Commits follow [Conventional Commits](https://www.conventionalcommits.org):**

```
feat(indexer): add cursor recovery on restart
fix(api): return 404 when event id not found
docs(sdk): add subscribeToContract example
chore(deps): update tokio to 1.35
```

Types: `feat`, `fix`, `docs`, `test`, `refactor`, `perf`, `chore`
Scopes: `indexer`, `api`, `sdk`, `db`, `docker`, `docs`

---

### Pull Requests

A PR that will be reviewed quickly:
- Has a linked issue (`Closes #NNN` in the description)
- Is focused — one concern per PR
- Passes CI (tests, clippy, fmt)
- Includes tests for any new behaviour
- Updates relevant docs if the change is user-facing

A PR that will be asked to revise:
- Mixes unrelated changes
- Has no tests for new logic
- Breaks the CI checks
- Changes public API without a prior discussion

---

### Code Standards

**Rust:**
- `cargo clippy` must pass with no warnings
- `cargo fmt` must be clean
- Errors use the project's typed error types — no `.unwrap()` in non-test code
- Public functions get doc comments

**TypeScript (SDK):**
- Strict mode on
- No `any`
- Named exports only
- ESLint + Prettier must be clean

**SQL:**
- Migrations are numbered and append-only — never edit a committed migration
- Index names follow `idx_<table>_<column(s)>`

---

### Good First Issues

These are the kinds of issues we'll tag `good first issue` once development starts:

- Adding a missing filter parameter to a REST endpoint
- Writing tests for an existing parser function
- Improving an error message with more context
- Documenting an undocumented function
- Adding a fixture event type to the test suite

---

### Harder Contributions

If you want to work on something more substantial:

- **Indexer core** (streamer, cursor logic, XDR parsing) — read the architecture section of the spec first, then open a discussion before touching it
- **Query performance** — bring benchmarks, not just intuition
- **New API capabilities** — propose in a Discussion with a concrete use case before implementing

---

### Security

Don't file security vulnerabilities as public issues. Email `security@trident.build` — we'll respond within 48 hours.

---

## Getting Help

- [GitHub Discussions](https://github.com/trident-build/trident/discussions) — questions, ideas, use cases
- [GitHub Issues](https://github.com/trident-build/trident/issues) — bugs and concrete feature requests
- `contributors@trident.build` — anything that shouldn't be public

---

*Trident is infrastructure for the whole Stellar ecosystem. Getting it right matters. Thanks for helping.*
