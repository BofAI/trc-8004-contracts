# trc-8004-contracts

Smart contracts for **TRC-8004** (Trustless Agent) support on the **TRON** network.

## What is TRC-8004?

TRC-8004 is an open, neutral standard for trustless AI agent identity, reputation, and validation. It provides a standardized way for agents to be registered as unique identities (NFTs) and builds a decentralized trust layer around them.

- **Identity First**: Agents are represented as TRC-721 tokens, making them ownable, transferable, and easily discoverable.
- **On-Chain Reputation**: A transparent feedback system for agents to build verifiable track records.
- **Independent Validation**: A framework for agents to request and receive third-party validation (TEE, zkML, or human audits) of their work.
- **Trustless Integration**: Verified payment wallets linked to agent identities for secure financial interactions.

## Features

- **TRC-721 Identity Registry**: Agents are minted as NFTs with unique IDs and metadata storage.
- **Verified Agent Wallets**: Secure linking of payment wallets to agents using TRC-712 signatures.
- **Spam-Resistant Feedback**: Anyone can leave feedback, with on-chain aggregation and revocation support.
- **Validation Hooks**: Generic interface for requesting and recording independent validations.
- **Tron-Optimized**: Designed for the TRON network with high throughput and low fees.
- **Flexible Metadata**: On-chain key-value metadata storage for agent-specific configurations.

## Architecture

The project consists of three main registry contracts:

- **`IdentityRegistry.sol`**: The core contract that manages agent registration (as TRC-721), metadata, and payment wallet verification.
- **`ReputationRegistry.sol`**: Manages feedback and reputation scores, allowing clients to rate agents and agents to respond.
- **`ValidationRegistry.sol`**: Handles validation requests from agents to independent validators and records their responses.

### Flow
1. **Register**: An owner registers an agent in `IdentityRegistry`, receiving an NFT.
2. **Verify Wallet**: The agent's payment wallet signs a message to prove ownership, which is then recorded in `IdentityRegistry`.
3. **Validate**: The agent requests validation for a task in `ValidationRegistry`; a validator provider (e.g., a TEE) submits the result.
4. **Interact & Feedback**: Clients interact with the agent and provide feedback in `ReputationRegistry`.

## Deployed Addresses (TRON Mainnet)

- IdentityRegistry : [TFLvivMdKsk6v2GrwyD2apEr9dU1w7p7Fy](https://tronscan.org/#/contract/TFLvivMdKsk6v2GrwyD2apEr9dU1w7p7Fy/code)
- ReputationRegistry : [TFbvfLDa4eFqNR5vy24nTrhgZ74HmQ6yat](https://tronscan.org/#/contract/TFbvfLDa4eFqNR5vy24nTrhgZ74HmQ6yat/code)
- ValidationRegistry : [TLCWcW8Qmo7QMNoAKfBhGYfGpHkw1krUEm](https://tronscan.org/#/contract/TLCWcW8Qmo7QMNoAKfBhGYfGpHkw1krUEm/code)

## Deployed Addresses (Nile Testnet)

- IdentityRegistry : [TDDk4vc69nzBCbsY4kfu7gw2jmvbinirj5](https://nile.tronscan.org/#/contract/TDDk4vc69nzBCbsY4kfu7gw2jmvbinirj5/code)
- ReputationRegistry : [TBVaGd6mBuGuN5ebcvPvRaJo4rtEWqsW6Y](https://nile.tronscan.org/#/contract/TBVaGd6mBuGuN5ebcvPvRaJo4rtEWqsW6Y/code)
- ValidationRegistry : [TGGkHDHhBzhFcLNcEogAWJkvfFYy4jyrSw](https://nile.tronscan.org/#/contract/TGGkHDHhBzhFcLNcEogAWJkvfFYy4jyrSw/code)

## Deployed Addresses (Shasta Testnet)

- IdentityRegistry : [TH775ZzfJ5V25EZkFuX6SkbAP53ykXTcma](https://shasta.tronscan.io/#/contract/TH775ZzfJ5V25EZkFuX6SkbAP53ykXTcma/code)
- ReputationRegistry : [TTkds2ZZKBTChZHho4wcWAa7eWQTxh5TUT](https://shasta.tronscan.io/#/contract/TTkds2ZZKBTChZHho4wcWAa7eWQTxh5TUT/code)
- ValidationRegistry : [TQBFHtKRiaQjc1xp4LtmmXKYdA7JLN89w3](https://shasta.tronscan.io/#/contract/TQBFHtKRiaQjc1xp4LtmmXKYdA7JLN89w3/code)

## Requirements

- **Node.js**: `^22.23.4 || ^24.22.1` (default: `22.23.4`, see `.nvmrc`)
- **pnpm** or **npm**
- **Solidity**: 0.8.25
- **For TRON Deployment**: [@sun-protocol/sunhat](https://github.com/sun-protocol/sunhat) and a TRON RPC URL + deployer private key.

## Quick Start

### Install Dependencies

If you use nvm, run `nvm install` and `nvm use` to select the version in `.nvmrc`.

```bash
npm install
# or
pnpm install
```

### Build
```bash
npm run compile
```

### Test
This project supports both Hardhat and Foundry for testing.

**Run Hardhat tests:**
```bash
npm test
```

**Run Foundry tests:**
```bash
npm run test-foundry
```

### Deploy (TRON)
Ensure your `.env` is configured with `TRON_PRIVATE_KEY` and `TRON_RPC_URL`.

```bash
npm run deploy
```

## Project Layout

- `contracts/`: Core smart contract logic.
  - `interfaces/`: Solidity interfaces for TRC-8004.
- `test/`: Hardhat and Foundry test suites.
- `scripts/`: Deployment and utility scripts.
- `deploy/`: Deployment configurations for Sunhat.

## Security

The `IdentityRegistry` uses **TRC-712** for secure wallet verification. Agent wallets are automatically reset upon NFT transfer to ensure security of the new owner.

*Note: These contracts are reference implementations and should undergo a professional audit before mainnet deployment.*

