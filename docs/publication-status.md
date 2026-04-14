# Publication Status

Keypair, faucet, transfer, and basic contract lifecycle are available for experimentation on the public testnet. Staking, governance, and some advanced or operator paths are not yet production-complete.

This page explains what each public DytallixHQ repo is for and where public
source currently lives.

## Repository Roles

| Repository | Role | Current publication state |
| --- | --- | --- |
| `dytallix-sdk` | Public SDK and CLI source | Canonical public client source |
| `dytallix-node` | Public node and runtime source | Canonical public node/backend source with clean-checkout production provenance |
| `dytallix-website` | Public website frontend source | Canonical public website frontend source for `dytallix.com`, including explorer UI and faucet page |
| `dytallix-faucet` | Public faucet backend source | Canonical public faucet backend source with edge compatibility config |
| `dytallix-explorer` | Explorer surface description | Docs-only explorer surface repo that points to the canonical frontend source in `dytallix-website` |
| `dytallix-docs` | Canonical public documentation | Docs source only, not the live website frontend source |

## Important Boundaries

- The live website frontend source is now published in the public `dytallix-website` repo.
- The live explorer frontend remains documented in `dytallix-explorer`, but its canonical frontend source now lives in `dytallix-website` under `src/pages/build/blockchain.tsx`.
- The live faucet backend source is now published in the public `dytallix-faucet` repo.
- The public `GET /api/faucet/status` and `GET /api/faucet/check/:address` compatibility endpoints are currently provided at the nginx edge and documented in `dytallix-faucet/deploy/nginx/faucet-compat.conf`.
- Production node provenance is now evidenced from a clean public checkout rooted at `/opt/dytallix-node`.

## What Is Publicly Verifiable Today

- The public node serves `GET /api/capabilities`, which exposes a machine-readable contract for the supported public surface.
- The SDK and CLI consume that contract or an embedded fallback manifest.
- The docs, SDK, node, website, faucet, and explorer repos can be aligned against live endpoint behavior from public source.

## What Is Still Missing

- an explorer-specific source repo if the frontend is ever split out of `dytallix-website`
- edge and backend parity work whenever the public faucet compatibility routes change
- continued publication of live deployment evidence as the node moves to future commits

For the current public website, explorer UI, faucet backend, and node deployment path, the source-backed publication gap is closed.