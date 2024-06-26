# Fee Collector Solana
Timelock governed OLAS and SOL Fee Collector on Solana.

## Pre-requisites
A successful program CPI with Lockbox and Orca Whirlpool programs requires that the following environment is satisfied:
```
anchor --version
anchor-cli 0.26.0
solana --version
solana-cli 1.14.29 (src:36af529e; feat:139196142)
rustc --version
rustc 1.62.0 (a8314ef7d 2022-06-27)
```

Advise the script `setup-env.sh` to correctly install the required environment.

## Development
Install the dependencies:
```
yarn
```

If you need to remove / check dependencies, run:
```
cargo clean
cargo tree
```

You might also want to completely remove the `Cargo.lock` file.

Build the code with:
```
anchor build
```

Run the validator in a separate window:
```
./validator.sh
```

Export environment variables:
```
export ANCHOR_PROVIDER_URL=http://127.0.0.1:8899
export ANCHOR_WALLET=artifacts/id.json
```

To run the initial script that would just initialize the lockbox program along with having Orca Whirlpool program
and required user accounts setup, run:
```
solana airdrop 10000 9fit3w7t6FHATDaZWotpWqN7NpqgL3Lm1hqUop4hAy8h --url localhost && npx ts-node tests/fee_collector_init.ts
```

To run integration test, make sure to stop and start the `validator.sh` in a separate window. Then run:
```
solana airdrop 10000 9fit3w7t6FHATDaZWotpWqN7NpqgL3Lm1hqUop4hAy8h --url localhost && npx ts-node tests/fee_collector.ts
```

The deployed program ID must be `DWDGo2UkBUFZ3VitBfWRBMvRnHr7E2DSh57NK27xMYaB` and corresponds to the `declare_id`
in the `programs/fee_collector/src/lib.rs` and `Anchor.toml` file.

For debugging a program address, after the launch of local validator, run:
```
solana logs -v --url localhost DWDGo2UkBUFZ3VitBfWRBMvRnHr7E2DSh57NK27xMYaB
```
