# Dytallix Documentation

Official documentation for Dytallix, a PQC-native Layer 1 blockchain.

This repository now contains the first complete public docs set for the Dytallix
SDK, CLI, public RPC, explorer endpoints, node snapshot, token model, security
assumptions, FAQ, and whitepaper distribution.

The content in `docs/` was reconciled against:

- the local `dytallix-sdk-publish` snapshot
- the local `dytallix-node-publish` snapshot
- the local explorer and faucet READMEs
- the three Dytallix whitepapers
- live public endpoint checks performed on April 6, 2026

## Repository Layout

- `docs/index.md` — landing page and doc map
- `docs/implementation-status.md` — verified public behavior and known mismatches
- `docs/getting-started.md` — SDK and CLI quickstart
- `docs/core-concepts.md` — accounts, tokens, gas, transaction model
- `docs/cli-reference.md` — CLI command reference
- `docs/sdk-reference.md` — SDK crate and API reference
- `docs/rpc-reference.md` — public RPC, explorer API, and faucet API reference
- `docs/node-operators.md` — local node and operator notes
- `docs/tokenomics.md` — token roles and current public testnet behavior
- `docs/security-model.md` — cryptographic and protocol security model
- `docs/whitepapers.md` — whitepaper index with bundled PDFs
- `docs/faq.md` — common questions and answers
- `docs/assets/whitepapers/` — bundled PDF whitepapers

## Local Preview

If you want to preview the docs as a site, this repository includes
`mkdocs.yml`.

```bash
pip install mkdocs
mkdocs serve
```

## Links

- Website: https://dytallix.com
- SDK: https://github.com/DytallixHQ/dytallix-sdk
- Explorer: https://github.com/DytallixHQ/dytallix-explorer
- Faucet: https://github.com/DytallixHQ/dytallix-faucet
- Docs site: https://dytallix.com/docs
- Discord: https://discord.gg/eyVvu5kmPG
