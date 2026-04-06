# CLI Reference

The `dytallix` CLI is the main developer entrypoint for wallet management,
funding, balance checks, transfers, and selected advanced workflows.

## Install

```bash
cargo install --git https://github.com/DytallixHQ/dytallix-sdk.git dytallix-cli --bin dytallix
```

Top-level help:

```bash
dytallix --help
```

## Global Notes

- default network profile: `testnet`
- keystore path: `~/.dytallix/keystore.json`
- active config path: `~/.dytallix/config.json`
- current public explorer page: `https://dytallix.com/build/blockchain`

The CLI currently exposes more surface area than the public gateway routes in a
few places. Those cases are called out below.

## `init`

```bash
dytallix init
```

What it does:

- generates an ML-DSA-65 keypair
- derives a D-Addr
- stores the key in the local keystore
- requests faucet funding for the active wallet
- polls until both `DGT` and `DRT` are visible

This is the fastest first-run path for most users.

## `wallet`

```bash
dytallix wallet <subcommand>
```

Subcommands:

- `create [--name NAME]`
- `import --key-file PATH [--name NAME]`
- `export --output PATH`
- `list`
- `switch NAME`
- `rotate`
- `info`

Behavior notes:

- imported keys may be raw bytes or hex-encoded bytes
- `rotate` intentionally refuses in-place rotation because the D-Addr is derived
  from the ML-DSA-65 public key and would change

## `balance`

```bash
dytallix balance
dytallix balance <D-ADDR>
```

Shows `DGT` and `DRT` balances for the active wallet or a provided address.

## `send`

```bash
dytallix send [--token dgt|drt] <D-ADDR> <AMOUNT>
```

What the command does:

- validates the destination address locally first
- reads the sender account nonce
- estimates fees from the network gas schedule
- signs the transaction
- submits it to the public node

Current public behavior:

- fees are currently charged in `DGT`
- you can transfer either `DGT` or `DRT`
- even a `DRT` transfer needs enough `DGT` to cover gas

## `faucet`

```bash
dytallix faucet
dytallix faucet <D-ADDR>
dytallix faucet status
```

Behavior:

- no argument funds the active wallet
- an address argument funds that address
- `status` checks whether the active wallet may request funds again

## `chain`

```bash
dytallix chain <subcommand>
```

Subcommands:

- `status`
- `block <NUMBER|HASH|latest|finalized>`
- `epoch`
- `params`

Notes:

- `status`, `block`, and `epoch` map cleanly to the public node reads
- `params` currently expects `/v1/chain/params`, which is not publicly routed
  on `https://dytallix.com`

## `crypto`

```bash
dytallix crypto <subcommand>
```

Subcommands:

- `keygen [--scheme ml-dsa-65|slh-dsa]`
- `sign <MESSAGE>`
- `verify <MESSAGE> <SIGNATURE_HEX> <PUBKEY_HEX>`
- `address <PUBKEY_HEX>`
- `inspect <KEYSTORE_FILE>`

Notes:

- ML-DSA-65 is the default account scheme
- `SLH-DSA` is exposed as an explicit option for cold-storage-style workflows
- `address` derivation is only meaningful for ML-DSA-65 public keys

## `config`

```bash
dytallix config <subcommand>
```

Subcommands:

- `show`
- `set <KEY> <VALUE>`
- `network <testnet|mainnet|local>`
- `reset`

Current caveat:

- the CLI local profile still points at `http://localhost:8545`
- the published local node snapshot and published SDK client use
  `http://localhost:3030`

## `dev`

```bash
dytallix dev <subcommand>
```

Subcommands:

- `faucet-server`
- `explorer`
- `docs`
- `discord`
- `github`
- `decode <HEX>`
- `encode <TEXT>`
- `simulate-tx <D-ADDR> <AMOUNT>`
- `benchmark`

Current caveat:

- `dev explorer` still opens `https://explorer.dytallix.com`
- the supported public explorer page currently lives at
  `https://dytallix.com/build/blockchain`

## `stake`

```bash
dytallix stake <subcommand>
```

Subcommands:

- `delegate <VALIDATOR> <AMOUNT>`
- `undelegate <VALIDATOR> <AMOUNT>`
- `claim`
- `status`

The CLI surface is present, but public module exposure may vary depending on the
gateway routes and node configuration.

## `governance`

```bash
dytallix governance <subcommand>
```

Subcommands:

- `proposals`
- `vote <ID> <yes|no|abstain>`
- `propose`
- `status <ID>`

The command surface exists, but several of the read routes it expects are under
`/v1/*` and are not currently public JSON routes on the website gateway.

## `contract`

```bash
dytallix contract <subcommand>
```

Subcommands:

- `deploy <WASM_FILE>`
- `call <ADDRESS> <METHOD> [ARGS...]`
- `query <ADDRESS> <METHOD> [ARGS...]`
- `info <ADDRESS>`
- `events <ADDRESS>`

The deploy and call commands build data-bearing transactions; query and metadata
commands depend on contract routes being exposed on the connected node.

## `node`

```bash
dytallix node <subcommand>
```

Subcommands:

- `start`
- `stop`
- `status`
- `peers`
- `logs`

This command family is primarily a repo-local developer convenience layer. It
expects helper scripts such as `start-local.sh` and `stop-local.sh` and is not a
full production node supervisor.
