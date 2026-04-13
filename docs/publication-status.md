# Publication Status

Keypair, faucet, transfer, and basic contract lifecycle are available for experimentation on the public testnet. Staking, governance, and some advanced or operator paths are not yet production-complete.

This page explains what each public DytallixHQ repo is for and where public
source is still missing.

## Repository Roles

| Repository | Role | Current publication state |
| --- | --- | --- |
| `dytallix-sdk` | Public SDK and CLI source | Canonical public client source |
| `dytallix-node` | Public node and runtime source | Published node snapshot plus reproducible deployment templates |
| `dytallix-faucet` | Faucet surface description | Docs-only service-surface repo |
| `dytallix-explorer` | Explorer surface description | Docs-only service-surface repo |
| `dytallix-docs` | Canonical public documentation | Docs source only, not the live website frontend source |

## Important Boundaries

- The explorer and faucet repos are docs-only service-surface repos. They do not publish the deployed explorer frontend or faucet backend code.
- The live website frontend source is not yet represented by a dedicated public repository in the DytallixHQ org.
- The current production website frontend checkout lives at `/opt/quantumvault/main-frontend`.
- The live explorer frontend currently lives inside that unpublished website source tree, not in the public `dytallix-explorer` repo.
- The live faucet backend source currently lives in a separate unpublished host checkout at `/root/faucet`, not in the public `dytallix-faucet` repo.
- The node repo currently provides a published node snapshot plus reproducible deployment templates. Until production provenance is independently evidenced from a clean checkout deployment, it should not be described as a fully proven canonical deployment repo.

## What Is Publicly Verifiable Today

- The public node serves `GET /api/capabilities`, which exposes a machine-readable contract for the supported public surface.
- The SDK and CLI consume that contract or an embedded fallback manifest.
- The docs, SDK, node, faucet, and explorer repos can be aligned against live endpoint behavior from public source.

## What Is Still Missing

- public repo for the live website frontend source
- public repo for the live explorer frontend source, or a public website repo that clearly owns `build/blockchain`
- public repo for the live faucet backend source
- independent public proof that production now runs only from a clean `dytallix-node` checkout

If a surface is not yet source-available, the public documentation should say that plainly rather than implying otherwise.