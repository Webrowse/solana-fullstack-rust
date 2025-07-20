# Solana Fullstack Rust

This is a fullstack Solana project in Rust:  
A raw on-chain smart contract (`solana-raw`) and its CLI client (`solana-vault-client`), combined via Git submodules.

## Structure

```
solana-fullstack-rust/
├── client/             # CLI client repo (submodule)
│   └── src/main.rs     # Interacts with the deployed program
├── on-chain/           # On-chain Solana program (submodule)
│   └── program/        # Rust-based Solana smart contract
├── .gitmodules         # Git submodule tracking
└── README.md
```

## Included Repos (Submodules)

- [`solana-raw`](https://github.com/Webrowse/solana-raw) → On-chain program
- [`solana-vault-client`](https://github.com/Webrowse/solana-vault-client) → CLI for sending transactions

## Setup Instructions

### 1. Clone with Submodules

```bash
git clone --recurse-submodules https://github.com/Webrowse/solana-fullstack-rust.git
cd solana-fullstack-rust
```

If already cloned without submodules:

```bash
git submodule update --init --recursive
```

### 2. Build the On-Chain Program

```bash
cd on-chain/program
cargo build-bpf
```

### 3. Deploy to Devnet

```bash
solana config set --url devnet
solana program deploy <path_to_solana_raw.so>
```

Note the program ID from this output.

### 4. Configure Client

In `client/src/main.rs`, update:

```rust
let program_id = Pubkey::from_str("YourProgramIDHere").unwrap();
```

Or load from a `.json` file if structured that way.

### 5. Run the Client

```bash
cd client
cargo run
```

## Requirements

- Rust + Cargo
- Solana CLI
- Git 2.11+ (for submodules)
- BPF SDK (for on-chain build)

## 📄 License

MIT

