# Contracts Overview

The Munja LST smart contract system provides liquid staking for MITO tokens through three main vaults. Users can deposit assets, earn rewards, and maintain liquidity while participating in validation.

## System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Munja LST Protocol                       │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐ │
│  │   mMITOc     │    │   mMITOs     │    │   gmMITO     │ │
│  │  Collateral  │    │   Staking    │    │  Governance  │ │
│  │    Vault     │    │    Vault     │    │    Vault     │ │
│  └──────┬───────┘    └──────┬───────┘    └──────┬───────┘ │
│         │                   │                    │          │
│         │         ┌─────────┴────────┐          │          │
│         │         │                  │          │          │
│         └────────▶│    Validators    │◀─────────┘          │
│                   │   & Rewards      │                      │
│                   └──────────────────┘                      │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

## Core Vaults

### mMITOc - Collateral Vault
**What it does**: Allows users to deposit WMITO as validator collateral and earn rewards.

**How it works**:
- Deposit WMITO tokens to receive mMITOc shares
- Your collateral is tracked and verified by the oracle system
- Earn rewards from validator operations
- Exchange rate changes based on validator performance
- Withdrawals require a time lock period

**Key characteristics**:
- Variable exchange rate (1 mMITOc ≠ 1 WMITO)
- Exposed to slashing risk (validator misbehavior)
- Rewards paid in gmMITO tokens
- 7-day withdrawal period

### mMITOs - Staking Vault
**What it does**: Provides liquid staking for tMITO with a simple 1:1 exchange.

**How it works**:
- Stake tMITO to receive equal amount of mMITOs tokens
- Your stake earns rewards from validators
- Exchange is always 1:1 (1 mMITOs = 1 tMITO)
- Use mMITOs in DeFi while earning staking rewards
- Withdrawals require a time lock period

**Key characteristics**:
- Fixed 1:1 exchange rate
- No slashing exposure on principal
- Rewards paid in gmMITO tokens
- 7-day withdrawal period

### gmMITO - Governance Vault
**What it does**: Converts staking rewards into governance tokens for protocol participation.

**How it works**:
- Claim your rewards from mMITOc or mMITOs vaults
- Rewards are automatically converted to gmMITO shares
- Exchange rate increases over time as more rewards compound
- Use gmMITO for governance voting
- Withdrawals require a time lock period

**Key characteristics**:
- Variable exchange rate (increases over time)
- Cannot deposit directly - only claim rewards
- Represents compounded governance power
- 7-day withdrawal period

## Withdrawal System

All three vaults use a **Withdrawal NFT** system:

1. **Request withdrawal**: Burn your vault tokens/shares
2. **Receive NFT**: Get an ERC721 NFT representing your pending withdrawal
3. **Wait for maturity**: Time lock period (typically 7 days)
4. **Claim assets**: Burn the NFT to receive your underlying assets

**Benefits**:
- NFTs are transferable (you can sell pending withdrawals)
- Clear visual representation of pending requests
- Protection against exchange rate manipulation
- Compatible with NFT marketplaces

## Oracle System

The protocol uses a **zero-knowledge oracle** to verify validator state:

**How it works**:
- Fetches validator data from the Cosmos chain
- Generates cryptographic proofs that data is correct
- Submits proofs to Ethereum for verification
- Contracts trust the verified data

**Why it matters**:
- Trustless verification (no need to trust oracle operators)
- Secure tracking of validator collateral
- Automatic detection of slashing events
- Accurate exchange rate calculations

## Reward Distribution

**Reward Flow**:
1. Validators generate rewards from operations
2. Protocol collects rewards periodically
3. Rewards distributed to vault participants
4. Users can claim rewards as gmMITO tokens

**Reward Types**:
- **Operator rewards**: For mMITOc collateral providers
- **Staking rewards**: For mMITOs stakers
- **Both paid in gmMITO governance tokens**

## User Journey

### Typical Flow:
1. **Start**: Deposit WMITO to mMITOc or tMITO to mMITOs
2. **Earn**: Accumulate rewards over time
3. **Claim**: Convert rewards to gmMITO
4. **Compound** (optional): Let gmMITO rewards compound automatically
5. **Withdraw**: Request withdrawal → receive NFT → wait → claim assets

### Example Scenarios:

**Collateral Provider**:
- Deposit 1000 WMITO → Receive ~950 mMITOc (depending on exchange rate)
- Earn rewards over time → Claim as gmMITO
- Request withdrawal → Receive NFT → Wait 7 days → Claim WMITO

**Liquid Staker**:
- Stake 1000 tMITO → Receive 1000 mMITOs (1:1)
- Use mMITOs in DeFi while earning rewards
- Earn rewards → Claim as gmMITO
- Unstake anytime → Receive NFT → Wait 7 days → Claim tMITO

## Security Features

- **Time-locked withdrawals**: Prevents rapid extraction during attacks
- **Oracle verification**: Ensures accurate validator state
- **Slashing detection**: Automatically adjusts for validator penalties
- **Upgradeable contracts**: Can be improved over time
- **Role-based access**: Different permissions for different operations

## Important Considerations

**Risks**:
- **mMITOc**: Exposed to validator slashing (lose collateral if validator misbehaves)
- **mMITOs**: Reduced rewards if validator is offline (no slashing of principal)
- **gmMITO**: Governance token value may fluctuate
- **All vaults**: 7-day withdrawal period (assets are locked)

**Benefits**:
- Maintain liquidity while staking (use vault tokens in DeFi)
- Earn rewards without running a validator
- Participate in protocol governance
- Transferable withdrawal NFTs

## Contract Addresses

Smart contract addresses are network-specific. See the deployment guide for current addresses on each network.
