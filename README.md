# Dytallix Documentation

Official documentation for Dytallix, a PQC-native Layer 1 blockchain.

This repository now contains the first complete public docs set for the Dytallix
SDK, CLI, public RPC, explorer endpoints, node snapshot, token model, security
assumptions, FAQ, and whitepaper distribution.

The content in `docs/` was reconciled against:

- the public `dytallix-sdk` repository
- the public `dytallix-node` repository
- the local explorer and faucet READMEs
- the three Dytallix whitepapers
- live public endpoint checks performed on April 6, 2026
- [`public-surface.json`](public-surface.json), which is checked in CI

## Repository Layout

- [Home / Doc Map](docs/index.md) — landing page and navigation entrypoint
- [Implementation Status](docs/implementation-status.md) — verified public behavior and known mismatches
- [Getting Started](docs/getting-started.md) — SDK and CLI quickstart
- [Contract Quickstart](docs/contract-quickstart.md) — canonical public WASM deploy path
- [Core Concepts](docs/core-concepts.md) — accounts, tokens, gas, and transaction model
- [CLI Reference](docs/cli-reference.md) — command reference for `dytallix`
- [SDK Reference](docs/sdk-reference.md) — Rust SDK crate and API reference
- [RPC Reference](docs/rpc-reference.md) — public RPC, explorer API, and faucet API reference
- [Node Operators](docs/node-operators.md) — local node and operator notes
- [Tokenomics](docs/tokenomics.md) — token roles and current public testnet behavior
- [Security Model](docs/security-model.md) — cryptographic and protocol security model
- [Whitepapers Index](docs/whitepapers.md) — whitepaper index and bundled documents
- [FAQ](docs/faq.md) — common questions and answers
- [Foundational White Paper (PDF)](docs/assets/whitepapers/dytallix-foundational-white-paper.pdf)
- [Technical White Paper (PDF)](docs/assets/whitepapers/dytallix-technical-white-paper.pdf)
- [Tokenomics Paper (PDF)](docs/assets/whitepapers/dytallix-tokenomics-paper.pdf)

## Local Preview

If you want to preview the docs as a site, this repository includes
[mkdocs.yml](mkdocs.yml).

```bash
pip install mkdocs
mkdocs serve
```

## Public Surface Guard

The canonical public integration values live in
[`public-surface.json`](public-surface.json). CI runs
[`scripts/check_public_surface.py`](scripts/check_public_surface.py) to catch
retired hosts, stale local ports, and install-command drift in the Markdown
docs before those inconsistencies land on `main`.

## Links

- Website: https://dytallix.com
- SDK: https://github.com/DytallixHQ/dytallix-sdk
- Explorer: https://github.com/DytallixHQ/dytallix-explorer
- Faucet: https://github.com/DytallixHQ/dytallix-faucet
- Docs site: https://dytallix.com/docs
- Discord: https://discord.gg/eyVvu5kmPG
