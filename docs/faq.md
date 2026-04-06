# FAQ

## What is Dytallix?

Dytallix is a PQC-native Layer 1 blockchain with ML-DSA-65 accounts, Bech32m
D-Addrs, a public testnet, and developer tooling centered on a Rust SDK and
CLI.

## Is there a live public testnet?

Yes. Public read endpoints, the faucet, and signed transaction submission were
all verified against `https://dytallix.com` on April 6, 2026.

## How do I get testnet funds?

Use the public faucet:

- `dytallix init`
- `dytallix faucet`
- `POST https://dytallix.com/api/faucet/request`

## Which signature scheme should I use?

Use `ML-DSA-65` for normal Dytallix accounts and D-Addr derivation.

## What does a Dytallix address look like?

A canonical address starts with `dytallix1` and is a Bech32m-encoded hash of an
ML-DSA-65 public key.

## Which token pays gas right now?

On the current public testnet, gas is charged in `DGT` according to the live
`/status` endpoint and the published node source.

## Then what is DRT for?

`DRT` remains a first-class token in balances, transfers, and reward-token
language across the SDK and explorer metadata. It is part of the dual-token
model even though the current public fee denom is `udgt`.

## Where do I view blocks and transactions?

Use the site-hosted explorer:

```text
https://dytallix.com/build/blockchain
```

## Can I call the public node directly?

Yes. The most useful public routes today are:

- `/status`
- `/account/:address`
- `/balance/:address`
- `/block/:id`
- `/blocks`
- `/tx/:hash`
- `/api/blockchain/submit`

## Are all CLI commands fully live on the public gateway?

Not yet. Wallet, balance, faucet, and core transfer flows are the most
straightforward today. Some governance, contract, and `/v1/*`-backed read
surfaces are still ahead of the public gateway routing.

## What port does the local node use?

The published local node snapshot uses `3030`. The CLI local-profile constant is
still catching up in one place, so direct local integrations should treat `3030`
as the observable node port.

## Where are the whitepapers?

They are bundled in this repository and indexed on
[`whitepapers.md`](whitepapers.md).
