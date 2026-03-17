<div align="center">

# 🔱 Trident

**Soroban Event Indexer for Stellar**

[![Status: Pre-Alpha](https://img.shields.io/badge/Status-Pre--Alpha-orange?style=flat-square)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](./LICENSE)
[![Built with Rust](https://img.shields.io/badge/Built%20with-Rust-orange?style=flat-square&logo=rust)](https://www.rust-lang.org/)
[![Network: Stellar](https://img.shields.io/badge/Network-Stellar%20%2F%20Soroban-black?style=flat-square)](https://stellar.org)

*The indexing layer Stellar's developer ecosystem needs.*

> ⚠️ Trident is in active pre-development. The codebase is not yet public. Watch this repo for updates.

</div>

---

## The Problem

Soroban's RPC node is intentionally thin. No long-term storage, no historical queries, no filtering. That's a reasonable protocol decision — but it means every developer building on Stellar has to build their own event pipeline from scratch.

Every team. Same problem. Every time.

Every mature smart contract ecosystem has solved this exactly once:

| Ecosystem | Solution |
|-----------|----------|
| Ethereum  | The Graph |
| Solana    | Helius / Triton |
| Cosmos    | SubQuery |
| **Stellar** | **Trident** |

---

## What Trident Does

Trident streams every Soroban contract event off the network, stores it, and gives developers a clean API to query it — by contract, by topic, by ledger range, in real time or historically.

```
Soroban RPC  →  Event Streamer  →  Event Parser  →  PostgreSQL
                                                         ↓
                                              REST + GraphQL API
                                                         ↓
                                              TypeScript / Rust SDK
```

The indexer is written in **Rust** — chosen for a system that needs to run 24/7, process binary XDR data at volume, and scale without a rewrite as Stellar grows. The developer-facing SDK is TypeScript because that's what most Stellar dApp developers actually use.

---

## Planned Features

- Full historical Soroban event storage — no retention limits
- Query by contract address, topic, ledger range, or timestamp
- REST and GraphQL APIs
- Real-time WebSocket subscriptions per contract
- TypeScript SDK
- Self-hosted via Docker Compose
- Free hosted tier for the Stellar ecosystem

---

## Roadmap

| Phase | Focus | Status |
|-------|-------|--------|
| **1 — MVP** | Rust indexer, PostgreSQL, REST API, Testnet support | 🔄 In progress |
| **2 — Developer Ready** | GraphQL, TypeScript SDK, Mainnet, hosted free tier | 📋 Planned |
| **3 — Scale** | WebSocket subscriptions, analytics, developer dashboard | 📋 Planned |
| **4 — Ecosystem** | Public event explorer, Rust SDK, multi-RPC redundancy | 📋 Planned |

---

## Project Status

- [x] Architecture defined
- [x] Full specification written — [`docs/SPECIFICATION.md`](./docs/SPECIFICATION.md)
- [ ] Repository scaffolding
- [ ] Phase 1 development begins

---

## Contributing

The codebase isn't public yet. The most useful contributions right now:

- **Read the spec** at [`docs/SPECIFICATION.md`](./docs/SPECIFICATION.md) and open an issue if something is wrong, underspecified, or questionable
- **Share your use case** — what would you build on Trident? What queries do you need? Open a [Discussion](https://github.com/trident-build/trident/discussions)
- **Challenge the architecture** — if you've built something similar, your experience matters

Once development is underway, the full contribution guide is in [CONTRIBUTING.md](./CONTRIBUTING.md).

---

## License

MIT — see [LICENSE](./LICENSE).

---

<div align="center">

*Build on Stellar. Query everything.*

[Discussions](https://github.com/trident-build/trident/discussions) · [Specification](./docs/SPECIFICATION.md) · [Contributing](./CONTRIBUTING.md)

</div>
