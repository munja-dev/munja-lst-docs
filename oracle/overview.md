# Oracle System Overview

The Munja LST Oracle brings validator data from the Cosmos blockchain to Ethereum in a trustless way. It uses zero-knowledge proofs to verify that the data is correct without requiring you to trust the oracle operators.

## What is the Oracle?

The oracle is a bridge that:
- Fetches validator information from the Cosmos chain
- Proves the data is legitimate using cryptographic proofs
- Submits verified data to Ethereum smart contracts
- Enables accurate tracking of validator collateral and performance

## Why Do We Need It?

The Munja protocol needs to know:
- How much collateral each validator has
- Whether validators have been slashed
- Who owns collateral for each validator
- Current validator states and balances

This information exists on the Cosmos chain but is needed on Ethereum. The oracle system bridges this gap **trustlessly**.

## How It Works (Simplified)

```
┌──────────────────────────────────────────────────────────┐
│  Step 1: Fetch Data from Cosmos Chain                    │
│  - Query validator state                                 │
│  - Request cryptographic proofs (ICS23)                  │
│  - Get consensus data (block hash, app hash)            │
└──────────────────────────────────────────────────────────┘
                         ↓
┌──────────────────────────────────────────────────────────┐
│  Step 2: Generate Zero-Knowledge Proof                   │
│  - Verify data matches consensus state                   │
│  - Create cryptographic proof of correctness             │
│  - Output: Proof + Verified Data                        │
└──────────────────────────────────────────────────────────┘
                         ↓
┌──────────────────────────────────────────────────────────┐
│  Step 3: Submit to Ethereum                              │
│  - Send proof + data to smart contract                   │
│  - Contract verifies proof on-chain                      │
│  - If valid, store verified data                         │
└──────────────────────────────────────────────────────────┘
                         ↓
┌──────────────────────────────────────────────────────────┐
│  Step 4: Contracts Use Data                              │
│  - Calculate exchange rates                              │
│  - Detect slashing events                                │
│  - Distribute rewards fairly                             │
└──────────────────────────────────────────────────────────┘
```

## Key Features

### 1. Trustless Verification

**Traditional oracles**: You must trust the operator
- Operator says "Validator has 1000 MITO collateral"
- You have to believe them
- Risk of manipulation

**Zero-knowledge oracle**: You can verify the proof
- Operator provides cryptographic proof
- Smart contract verifies the proof on-chain
- Mathematically impossible to fake
- No need to trust anyone

### 2. Cryptographic Proofs

The oracle uses two types of proofs:

**ICS23 Proofs** (from Cosmos):
- Prove data exists in the Cosmos blockchain
- Show data is part of consensus state
- Verified against block hash

**Zero-Knowledge Proofs** (SP1):
- Prove the ICS23 proofs are valid
- Generate on-chain verifiable proof
- Efficient verification on Ethereum

### 3. Freshness Guarantee

- Proofs must be recent (within 12 hours)
- Uses Ethereum's beacon chain (EIP-4788)
- Prevents using stale data
- Ensures accurate validator state

## What Data Is Tracked?

### Validator Collateral
- Total collateral amount deposited
- Current collateral after any slashing
- Collateral changes over time

### Collateral Ownership
- Who owns how much collateral
- Multiple owners per validator
- Ownership shares for reward distribution

### Validator State
- Voting power
- Active status
- Commission rates

## Benefits for Users

### Accurate Exchange Rates
- Exchange rates reflect real validator collateral
- Slashing automatically detected
- Fair share calculations

### Automatic Slashing Detection
- Oracle detects when validator is slashed
- Exchange rate adjusts automatically
- Protects remaining collateral

### Fair Reward Distribution
- Rewards distributed based on verified collateral
- Time-weighted calculations
- No manipulation possible

### Security
- No need to trust oracle operators
- All data cryptographically verified
- On-chain proof verification

## Oracle Components (High-Level)

### Prover Service
**What it does**: Generates zero-knowledge proofs

**How it works**:
1. Fetches validator data from Cosmos RPC
2. Verifies data is correct
3. Generates cryptographic proof
4. Stores proof for submission

### Feeder Service
**What it does**: Submits proofs to Ethereum

**How it works**:
1. Monitors for new proofs
2. Checks proofs are fresh (< 12 hours)
3. Submits transactions to Ethereum
4. Updates oracle contract with verified data

### Oracle Contract
**What it does**: Verifies and stores data on Ethereum

**How it works**:
1. Receives proof + data from feeder
2. Verifies proof is valid
3. Checks data is fresh
4. Stores verified data for vault contracts

## Security Properties

### Trustlessness
- Don't need to trust oracle operators
- Cryptographic proofs ensure correctness
- Anyone can verify proofs

### Soundness
- Invalid proofs cannot be verified
- Fake data is rejected
- Mathematically guaranteed

### Freshness
- Data must be recent (< 12 hours)
- Stale proofs are rejected
- Real-time validator state

### Integrity
- Data tied to consensus state
- Cannot be modified in transit
- Verified against blockchain

## Common Questions

### Why use zero-knowledge proofs?

**Benefits**:
- Trustless verification (no need to trust operators)
- Efficient on-chain verification
- Strong cryptographic guarantees
- Industry-standard technology

### How often is data updated?

- Typically every few hours
- Can be updated more frequently if needed
- Must be within 12-hour window for EIP-4788

### What happens if the oracle stops?

- Contracts use last known valid data
- Can switch to backup oracle systems
- Time-locked withdrawals protect users
- Protocol has fallback mechanisms

### Can the oracle be manipulated?

**No, because**:
- Proofs are cryptographically verified
- Data is tied to Cosmos consensus
- On-chain verification prevents tampering
- Multiple layers of verification

### What if validator is slashed?

1. Slashing occurs on Cosmos chain
2. Oracle fetches updated collateral amount
3. Generates proof of new state
4. Submits to Ethereum
5. Contracts detect slashing
6. Exchange rate adjusts automatically
7. Users see accurate collateral amounts

## Real-World Example

### Normal Operation:
```
Day 1: Validator has 1000 MITO collateral
       → Oracle submits proof
       → Contract stores: 1000 MITO
       → Exchange rate: Normal

Day 2: No changes
       → Oracle submits updated proof
       → Contract stores: 1000 MITO
       → Exchange rate: Unchanged
```

### Slashing Event:
```
Day 1: Validator has 1000 MITO collateral
       → Contract stores: 1000 MITO
       → Exchange rate: 1.0

Day 2: Validator misbehaves, slashed 10%
       → Cosmos chain reduces collateral to 900 MITO
       → Oracle detects change
       → Generates proof of 900 MITO
       → Submits to Ethereum
       → Contract updates: 900 MITO
       → Exchange rate: 0.9 (reflects slashing)

Day 3: Users see accurate collateral
       → Withdrawals adjusted for slashing
       → Fair distribution to remaining stakers
```

## Technical Details (Optional)

For developers and advanced users who want to understand the implementation:

- **Zero-Knowledge System**: SP1 zkVM with Groth16 proofs
- **Proof Standard**: ICS23 for Cosmos state verification
- **Ethereum Integration**: EIP-4788 for beacon root access
- **Storage**: Verified data stored on-chain for vault contracts

## Related Documentation

- [Contracts Overview](../contracts/overview.md) - How contracts use oracle data
- [Vault Contracts](../contracts/vaults/README.md) - Understanding the vaults
