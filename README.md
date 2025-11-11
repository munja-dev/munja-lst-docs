# Munja LST Developer Documentation

Welcome to the Munja LST developer documentation. This comprehensive guide covers the architecture, implementation details, and development workflows for the Munja liquid staking protocol.

## What is Munja LST?

Munja LST is a decentralized liquid staking protocol that enables users to stake MITO and tMITO tokens while maintaining liquidity through liquid staking tokens (mMITO, gmMITO). The protocol features a sophisticated zero-knowledge proof system that trustlessly verifies Cosmos validator states on EVM chains.

## Key Features

- **Liquid Staking**: Stake MITO/tMITO and receive tradeable liquid tokens
- **Dual Vault Architecture**: Separate vaults for collateral (mMITOc) and staking (mMITOs)
- **Governance Tokens**: Stake mMITO to receive gmMITO for protocol governance
- **ZK Oracle System**: Trustlessly verify Cosmos validator states using SP1 zkVM
- **TWAB-Based Rewards**: Fair reward distribution based on time-weighted average balance
- **Slashing Protection**: Automatic handling of validator slashing events

## Architecture Overview

The protocol consists of three main layers:

### Smart Contracts Layer
- ERC4626 vault implementations (mMITOc, mMITOs, gmMITO)
- Zero-knowledge oracle contracts (ZkOracleFeed, ManagedOracleFeed)
- Validator management system (ValidatorController, RewardRouter)
- Withdrawal NFT system for time-locked withdrawals

### Oracle Layer (Rust)
- ABCI proof verification library (ICS23)
- SP1 zkVM program for trustless verification
- Proof generation service (prover)
- Contract feeding service (feeder)

### Supporting Services
- Event indexer (Ponder)
- Frontend application (Next.js)
- Operator service for automated operations

## Technology Stack

- **Smart Contracts**: Solidity 0.8.28, Foundry, UUPS proxy pattern
- **Oracle**: Rust, SP1 zkVM, ICS23 proofs, PostgreSQL/S3
- **Frontend**: Next.js, TypeScript, wagmi, RainbowKit
- **Indexer**: Ponder, PostgreSQL

## Documentation Structure

This documentation is organized into the following sections:

1. **Introduction**: Overview and getting started
2. **Contracts**: Smart contract architecture and implementation
3. **Oracle**: Zero-knowledge oracle system
4. **Development**: Development guides and workflows
5. **API Reference**: Detailed API documentation
6. **Deployment**: Deployment guides and best practices

## Quick Links

- [Getting Started](getting-started/prerequisites.md)
- [Contracts Overview](contracts/overview.md)
- [Oracle Overview](oracle/overview.md)
- [Development Guide](development/setup.md)

## Contributing

This is a security-critical financial protocol. All contributions should follow best practices for smart contract security and be thoroughly tested. See the [Contributing Guide](development/contributing.md) for details.

## License

See the LICENSE file in the project root for details.
