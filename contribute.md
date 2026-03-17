<div align="center">

# 🔱 Contributing to Trident

**Trident is pre-launch open-source infrastructure for the Stellar ecosystem.**
**Your involvement at this stage shapes the project from the ground up.**

</div>

---

## Table of Contents

- [Where We Are Right Now](#where-we-are-right-now)
- [How to Contribute Before the Codebase Exists](#how-to-contribute-before-the-codebase-exists)
- [How to Contribute Once Development Begins](#how-to-contribute-once-development-begins)
  - [Reporting Bugs](#reporting-bugs)
  - [Suggesting Features](#suggesting-features)
  - [Submitting Code](#submitting-code)
  - [Improving Documentation](#improving-documentation)
- [Development Setup](#development-setup)
- [Development Workflow](#development-workflow)
  - [Branching Strategy](#branching-strategy)
  - [Commit Messages](#commit-messages)
  - [Pull Request Process](#pull-request-process)
- [Testing](#testing)
- [Style Guide](#style-guide)
- [Code of Conduct](#code-of-conduct)
- [Getting Help](#getting-help)

---

## Where We Are Right Now

Trident does not yet have a public codebase. We are in the **architecture and specification phase** — defining exactly what we are building before we write the first line of code.

This is actually the best time to get involved. Decisions made now about architecture, API design, data models, and developer experience will define the project for years. Your voice matters most before those decisions are locked in.

---

## How to Contribute Before the Codebase Exists

There is meaningful work to do right now:

**Review the specification**

The full project specification lives in [`./docs/SPECIFICATION.md`](./docs/SPECIFICATION.md). Read it. If something is unclear, underspecified, architecturally questionable, or missing entirely — open an issue. These are the highest-leverage contributions you can make today.

**Share your use case**

Open a [GitHub Discussion](https://github.com/trident-build/trident/discussions) and tell us what you are building on Stellar. What events do you need to query? What does your current workaround look like? What would make Trident indispensable to your project? This directly informs our priorities.

**Challenge the architecture**

Have experience building indexers, event-driven systems, or Stellar infrastructure? We want your critique. Open a Discussion under the `architecture` category. If you think we have made the wrong choice — on the database, the streaming strategy, the API design — say so now while we can still change it.

**Spread the word**

If you believe this infrastructure needs to exist, tell other Stellar developers. Community demand is what justifies grant funding and sustained development. Star the repository. Share it in the Stellar Discord and developer forums.

---

## How to Contribute Once Development Begins

When Phase 1 development kicks off, this section becomes the primary guide. All active work will be tracked via GitHub Issues and a public project board linked from the repository homepage.

### Reporting Bugs

Before filing a bug report:

1. Search [existing issues](https://github.com/trident-build/trident/issues) to check if it has been reported already.
2. Confirm you can reproduce it on the latest version of `main`.

A good bug report can be acted on without back-and-forth. Use the **Bug Report** issue template and include:

- The Trident version you are running
- Network: Mainnet / Testnet / Futurenet
- Deployment mode: Hosted API / Self-hosted Docker / Local dev
- Exact steps to reproduce, as minimal as possible
- What you expected to happen
- What actually happened — full error messages and stack traces
- Relevant logs from the `indexer` or `api` service

> **Security vulnerabilities must not be filed as public GitHub issues.** Send them to `security@trident.build`. We respond within 48 hours and follow responsible disclosure.

---

### Suggesting Features

Use the **Feature Request** issue template. The most useful feature requests describe:

- The concrete problem you are trying to solve (not just the solution you have in mind)
- How you would use this in a real project
- Any alternatives you have already considered

Requests that clearly articulate the underlying developer pain are far more likely to be prioritised over requests that only describe a desired implementation.

Check the [roadmap](./README.md#roadmap) before submitting — your idea may already be planned.

---

### Submitting Code

**Before writing code for anything non-trivial, open an issue first.**

This is the most important rule in the project. It prevents wasted effort on work that duplicates something in progress, conflicts with a planned approach, or solves a problem differently than maintainers intend. Comment on the issue to claim it before you start.

For good starting points, look for issues labelled:

- [`good first issue`](https://github.com/trident-build/trident/labels/good%20first%20issue) — well-scoped, low-risk, no deep system knowledge required
- [`help wanted`](https://github.com/trident-build/trident/labels/help%20wanted) — higher-impact work where we actively want community involvement

---

### Improving Documentation

Documentation contributions are always welcome and never need a prior issue. This includes fixing typos, clarifying confusing explanations, adding missing examples, and writing guides for common use cases.

Documentation source lives in `./docs/`. The public site at [docs.trident.build](https://docs.trident.build) is built from this directory.

---

## Development Setup

> This section will be fully filled out when the repository goes public. The below reflects the planned setup.

**Prerequisites:**

| Tool | Minimum Version |
|------|----------------|
| Node.js | 20 LTS |
| pnpm | 8+ |
| Docker | 24+ |
| Docker Compose | v2 |
| Git | 2.40+ |

**Setup:**

```bash
git clone https://github.com/trident-build/trident.git
cd trident
pnpm install
cp .env.example .env
# Configure .env with your RPC URL and database credentials
docker compose -f docker/docker-compose.dev.yml up -d
pnpm db:migrate
pnpm dev
```

The API will be available at `http://localhost:3000`. Full setup details will be added to [`./docs/development.md`](./docs/development.md) before the first public commit.

---

## Development Workflow

### Branching Strategy

| Branch | Purpose |
|--------|---------|
| `main` | Stable, production-ready code. All releases tagged here. |
| `dev` | Integration branch. PRs target `dev`. |
| `feature/<issue-number>-short-description` | New features |
| `fix/<issue-number>-short-description` | Bug fixes |
| `docs/<short-description>` | Documentation only |
| `chore/<short-description>` | Tooling, CI, dependencies |

Always branch from the latest `dev`:

```bash
git fetch upstream
git checkout -b feature/42-graphql-subscriptions upstream/dev
```

---

### Commit Messages

Trident uses [Conventional Commits](https://www.conventionalcommits.org). Every commit message must follow this format:

```
<type>(<scope>): <short description>

[optional body]

[optional footer — e.g. Fixes #42]
```

**Types:**

| Type | When to use |
|------|-------------|
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation only |
| `test` | Adding or fixing tests |
| `refactor` | Neither a bug fix nor a new feature |
| `perf` | A performance improvement |
| `chore` | Tooling, CI, dependency updates |

**Scopes:** `indexer`, `api`, `sdk`, `sdk-rust`, `db`, `docs`, `docker`

**Rules:**
- Imperative mood: "add feature" not "added feature"
- No capital letter on the first word
- No period at the end
- Subject line under 72 characters
- Reference the issue in the footer: `Fixes #42`

Commits that don't follow this format will be flagged by CI.

---

### Pull Request Process

1. **One PR, one concern.** A PR that mixes a bug fix with a new feature will be asked to split.
2. **Fill out the PR template.** Every field exists for a reason.
3. **Link the issue.** Every PR must reference its issue with `Closes #NNN`.
4. **Pass CI.** Linting, type checking, tests, and build must all be green before review begins.
5. **Include tests.** Bug fixes need a regression test. New features need unit tests and integration tests where appropriate.
6. **Update documentation** if your change affects any developer-facing behaviour.

**Review SLA:** Maintainers aim to review PRs within 3 business days. Complex PRs may take longer and will be acknowledged explicitly.

---

## Testing

Trident will use [Vitest](https://vitest.dev) for unit and integration tests. The testing strategy across the project:

| Layer | Test Type | What's Verified |
|-------|-----------|----------------|
| Parser | Unit | XDR decoding correctness, type normalisation, error handling |
| Streamer | Unit | Cursor management, retry logic, backoff behaviour |
| API routes | Integration | Request/response shapes, filter logic, pagination |
| Full pipeline | Integration | Streamer → parser → DB → API end-to-end |
| Testnet | E2E (nightly) | Real events, real network, full correctness verification |

**Coverage targets** (to be enforced in CI):
- Parser: 95%+
- Streamer: 90%+
- API routes: 85%+
- SDK: 90%+

All PRs adding new behaviour must include tests. PRs that reduce coverage will be asked to add them before merging.

---

## Style Guide

A formal linting and formatting configuration will be committed with the initial codebase. The principles that will govern it:

**TypeScript**
- No `any`. Use `unknown` and narrow with type guards.
- Prefer `const`. Never use `var`.
- Explicit return types on all exported functions.
- Typed errors — throw instances of `TridentError` subclasses, never raw strings.
- `async/await` over `.then()` chains.
- Named exports over default exports everywhere except entry-point files.

**SQL**
- Migrations are numbered sequentially and append-only — never modify a committed migration.
- Index names follow the pattern: `idx_<table>_<columns>`.
- Explicit column lists in all `SELECT` statements. No `SELECT *` in production query code.

**Naming**

| Context | Convention |
|---------|-----------|
| TS variables & functions | `camelCase` |
| TS types & interfaces | `PascalCase` |
| TS filenames | `kebab-case` |
| DB tables & columns | `snake_case` |
| Environment variables | `SCREAMING_SNAKE_CASE` |
| API endpoints | `kebab-case` |
| Git branches | `kebab-case` |

---

## Code of Conduct

Trident follows the [Contributor Covenant Code of Conduct](./CODE_OF_CONDUCT.md). By participating, you agree to uphold it.

The short version: be kind, be constructive, assume good intent. We are building public infrastructure together.

---

## Getting Help

- **[GitHub Discussions](https://github.com/trident-build/trident/discussions)** — questions, ideas, use cases, architecture discussion
- **[GitHub Issues](https://github.com/trident-build/trident/issues)** — confirmed bugs and concrete feature requests
- **Email** — `contributors@trident.build` — for anything that shouldn't be public

If you are unsure whether something is a bug or a usage question, start in Discussions. It is always the right place.

---

<div align="center">

**Trident is foundational infrastructure for Stellar's developer ecosystem.**
**Getting involved now means you help shape it from day one.**

🔱

</div>
