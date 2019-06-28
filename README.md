# XTH Client

A Dothereum testnet node implementation written in Rust built with Parity Substrate.

What is Dothereum? [Medium: The Dothereum Parachain](https://medium.com/@dothereum/the-dothereum-parachain-7fd056c1107d).

### Building the client from source

1. Install Rust:
  ```bash
  curl https://sh.rustup.rs -sSf | sh
  ```
2. Install required tools:
  ```bash
  ./scripts/init.sh
  ```
3. Ensure Cargo is in your `$PATH`:
  ```bash
  export PATH=$PATH:$HOME/.cargo/bin
  ```
4. Build the WebAssembly binary:
  ```bash
  ./scripts/build.sh
  ```
5. Build all native code:
  ```bash
  cargo build --release
  ```

### Run a development chain

You can start a development chain with:

```bash
./xth --dev
```

Detailed logs may be shown by running the node with the following environment variables set: `RUST_LOG=debug RUST_BACKTRACE=1 ./xth --dev`.

### Run local XTH testnet

If you want to see the multi-node consensus algorithm in action locally, then you can create a local testnet with two validator nodes for Alice and Bob, who are the initial authorities of the genesis chain that have been endowed with testnet units. Give each node a name and expose them so they are listed on the Polkadot [telemetry site](https://telemetry.polkadot.io/#/Local%20Testnet). You'll need two terminal windows open.

We'll start Alice's dothereum node first on default TCP port 30333 with her chain database stored locally at `/tmp/alice`. The bootnode ID of her node is `QmZGoiBiYFYSGL7XjSTmoY2yoqaraody7V8X8ccXB1vmMv`, which is generated from the `--node-key` value that we specify below:

```bash
./xth \
  --base-path /tmp/alice \
  --chain=local \
  --alice \
  --node-key 00000000000000000000000000000000000000000000000000000000000a11c3 \
  --telemetry-url ws://telemetry.polkadot.io:1024 \
  --validator
```

In the second terminal, we'll start Bob's dothereum node on a different TCP port of 30334, and with his chain database stored locally at `/tmp/bob`. We'll specify a value for the `--bootnodes` option that will connect his node to Alice's bootnode ID on TCP port 30333:

```bash
./xth \
  --base-path /tmp/bob \
  --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/QmZGoiBiYFYSGL7XjSTmoY2yoqaraody7V8X8ccXB1vmMv \
  --chain=local \
  --bob \
  --node-key 0000000000000000000000000000000000000000000000000000000000000b0b \
  --port 30334 \
  --telemetry-url ws://telemetry.polkadot.io:1024 \
  --validator
```

### Connect with the XTH testnet

_Soon(tm)._

```bash
./xth
```

### Get help

Additional CLI usage options are available and may be shown by running `./xth --help`.

For questions and bug reports, please use the [Github issue tracker](https://github.com/dothereum/client/issues).
