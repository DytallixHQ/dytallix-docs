# Contract Quickstart

This is the canonical public path from zero to a first contract deployment on
Dytallix.

It uses:

- the public `dytallix` CLI
- the live testnet faucet and submit path
- the minimal deployable WASM example published in `dytallix-sdk`

## What You Need

- Rust and Cargo
- network access to `https://dytallix.com`
- the `wasm32-unknown-unknown` Rust target

## 1. Install The CLI

```bash
cargo install --git https://github.com/DytallixHQ/dytallix-sdk.git dytallix-cli --bin dytallix
```

## 2. Create And Fund A Wallet

```bash
dytallix init
```

This creates an ML-DSA-65 keypair, writes `~/.dytallix/keystore.json`, and
requests faucet funds for the active address.

Confirm the wallet state:

```bash
dytallix wallet info
dytallix balance
```

## 3. Clone The SDK Example Contract

```bash
git clone https://github.com/DytallixHQ/dytallix-sdk.git
cd dytallix-sdk
rustup target add wasm32-unknown-unknown
```

The canonical quickstart contract lives at:

```text
examples/contracts/minimal_contract
```

## 4. Build A Deployable WASM Artifact

```bash
cargo build \
  --manifest-path examples/contracts/minimal_contract/Cargo.toml \
  --target wasm32-unknown-unknown \
  --release
```

The resulting artifact is:

```text
examples/contracts/minimal_contract/target/wasm32-unknown-unknown/release/minimal_contract.wasm
```

## 5. Deploy It

```bash
dytallix contract deploy \
  examples/contracts/minimal_contract/target/wasm32-unknown-unknown/release/minimal_contract.wasm
```

Expected result:

- a transaction hash
- a predicted contract address
- a success message indicating the deployment transaction was submitted

## 6. Inspect The Contract Lifecycle

Useful follow-up commands:

```bash
dytallix contract info <CONTRACT_ADDRESS>
dytallix contract query <CONTRACT_ADDRESS> ping
dytallix contract call <CONTRACT_ADDRESS> ping
dytallix contract events <CONTRACT_ADDRESS>
```

If you want the full lifecycle against a current node build or a direct node
endpoint, point the CLI at that base URL first:

```bash
dytallix config set endpoint http://localhost:3030
```

Or for a one-off shell session:

```bash
export DYTALLIX_ENDPOINT=http://localhost:3030
```

That override applies to `contract info`, `query`, `call`, and `events` without
changing your faucet profile.

Useful public pages:

- Explorer page: `https://dytallix.com/build/blockchain`
- Docs: `https://dytallix.com/docs`

## Public Rollout Status

The current node and CLI support contract lifecycle reads at:

- `GET /api/contracts/<address>`
- `GET /api/contracts/<address>/query/<method>`
- `GET /api/contracts/<address>/events`

The public website gateway still needs to roll out those reads. Until that
happens, use a direct node endpoint or a local node for the full post-deploy
loop.

## Related Repositories

- SDK and CLI: https://github.com/DytallixHQ/dytallix-sdk
- Reference contracts: https://github.com/DytallixHQ/dytallix-contracts
