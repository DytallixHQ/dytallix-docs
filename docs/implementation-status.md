# Implementation Status

This page records the public behavior that was verified on April 6, 2026 and
the mismatches that still exist across the local source snapshots.

## Treat These As Canonical Today

For developers building against the public testnet, the following should be
treated as canonical:

- root RPC reads under `https://dytallix.com`
- explorer reads under `https://dytallix.com/api/blockchain`
- faucet endpoints under `https://dytallix.com/api/faucet`
- signed transaction submission through
  `POST https://dytallix.com/api/blockchain/submit`
- ML-DSA-65 addresses and signatures for public Dytallix accounts

## Verified Public Behavior

The following were checked directly against the live gateway.

### Root RPC

- `GET /status` returns chain health, height, gas schedule, and timestamp
- `GET /account/:address` returns address, raw balances, and nonce
- `GET /balance/:address` returns formatted per-denom balances
- `GET /block/:id` returns block details
- `GET /blocks?limit=n` returns recent blocks
- `GET /tx/:hash` returns a transaction receipt including gas fields

### Submit Path

`POST /api/blockchain/submit` is live and expects a JSON body containing a
`signed_tx` object. A malformed body returns HTTP `422`, which confirms the
route is active and validating request shape.

### Faucet

- `GET /api/faucet/status`
- `GET /api/faucet/check/:address`
- `POST /api/faucet/request`

The faucet reported these limits on April 6, 2026:

- `10 DGT` per request
- `100 DRT` per request
- `60` minute cooldown
- `3` requests per hour

### End-To-End SDK Check

The published SDK example `first-transaction` was run successfully against the
public testnet on April 6, 2026. The flow:

- generated an ML-DSA-65 keypair
- derived a D-Addr
- funded the address through the faucet
- estimated fees
- submitted a signed transaction
- received a confirmed receipt

## Known Mismatches

### Fee Token Language

Several older docs and adjacent notes describe `DRT` as the fee token. The
current public node and live `/status` endpoint report:

- `fee_denom: "udgt"`
- `min_gas_price: 1000`

The published SDK snapshot also formats fee estimates in `DGT`.

Practical guidance:

- use `DGT` as the current public testnet fee token
- keep `DRT` documented as the reward token and as part of the long-range
  dual-token design language

### SDK Dev Tree vs Publish Tree

The local `dytallix-sdk` working tree still points transaction simulation and
submission at `/v1/transactions` and `/v1/transactions/simulate`.

The local `dytallix-sdk-publish` tree is closer to the public gateway:

- it submits transactions through `/api/blockchain/submit`
- it derives fees from `/status`
- it uses `http://localhost:3030` for the local node client

This documentation uses the publish-tree behavior whenever the two diverge.

### Public `GET /v1/*` JSON Routes

The public site gateway does not currently expose `GET /v1/*` JSON responses as
developer-facing read APIs. Requests such as `GET /v1/transactions` currently
fall through to the website HTML shell.

Practical guidance:

- use root RPC paths and `/api/blockchain/*` read paths today
- do not depend on public `GET /v1/*` routes unless the gateway is updated

### Local Node Port

There is still a local-profile inconsistency:

- published node source and published SDK client use `3030`
- the current CLI config helper still uses `8545` for the `local` profile

If you are operating the published local node snapshot, `3030` is the
observable node port in source and docs.

### Explorer URL

The supported public explorer page is:

- `https://dytallix.com/build/blockchain`

The current CLI `dev explorer` command still points to:

- `https://explorer.dytallix.com`

Treat the site-hosted explorer path as canonical for now.

### Block Interval Default

The older RPC README says `DYT_BLOCK_INTERVAL_MS` defaults to `2000`. The
published node `main.rs` currently defaults it to `15000`.

If you are starting from source, trust `main.rs`.

## Recommendation

For future doc maintenance, use this priority order:

1. live public gateway behavior
2. `dytallix-sdk-publish`
3. `dytallix-node-publish`
4. older working-tree or placeholder docs
