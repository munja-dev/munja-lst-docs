# Vault Contracts

The Munja LST protocol has three vault contracts that allow you to deposit assets, earn rewards, and maintain liquidity.

## Overview

```
User Assets                     Liquid Tokens
─────────────────────────────────────────────────────────────

WMITO ──────▶ mMITOc ──────▶ mMITOc shares
(Collateral)   Vault         (Earn rewards, risk of slashing)
                 │
                 │ Claim rewards as gmMITO
                 ▼

tMITO ──────▶ mMITOs ──────▶ mMITOs tokens
(Staking)      Vault         (1:1 exchange, liquid staking)
                 │
                 │ Claim rewards as gmMITO
                 ▼

Rewards ─────▶ gmMITO ─────▶ gmMITO shares
               Vault         (Governance + compounding)
```

## The Three Vaults

### [mMITOc - Collateral Vault](mmitoc.md)

**Purpose**: Deposit WMITO as validator collateral and earn rewards.

**How it works**:
- Deposit WMITO → Receive mMITOc shares
- Exchange rate varies based on validator performance
- Exposed to slashing if validators misbehave
- Earn operator rewards in gmMITO

**Best for**: Users willing to accept slashing risk for validator collateral rewards

**Key details**:
- Variable exchange rate
- 7-day withdrawal period
- Slashing exposure
- Higher potential rewards

---

### mMITOs - Staking Vault

**Purpose**: Liquid staking for tMITO with a simple 1:1 exchange.

**How it works**:
- Stake tMITO → Receive equal amount of mMITOs
- Always 1:1 ratio (1 tMITO = 1 mMITOs)
- Use mMITOs in DeFi while earning staking rewards
- Earn staking rewards in gmMITO

**Best for**: Users who want simple liquid staking without slashing exposure

**Key details**:
- Fixed 1:1 exchange rate
- 7-day withdrawal period
- No slashing risk on principal
- Standard staking rewards

---

### gmMITO - Governance Vault

**Purpose**: Convert staking rewards into governance tokens.

**How it works**:
- Claim rewards from mMITOc or mMITOs
- Rewards automatically convert to gmMITO shares
- Exchange rate increases over time (compounding)
- Use for protocol governance voting

**Best for**: Users who want governance participation and automatic reward compounding

**Key details**:
- Cannot deposit directly (claim rewards only)
- Variable exchange rate (increases over time)
- 7-day withdrawal period
- Represents governance power

---

## Comparison Table

| Feature | mMITOc | mMITOs | gmMITO |
|---------|--------|--------|--------|
| **Deposit Asset** | WMITO | tMITO | N/A (claim only) |
| **Exchange Rate** | Variable | 1:1 Fixed | Variable (increasing) |
| **Slashing Risk** | Yes | No | No |
| **Withdrawal Period** | 7 days | 7 days | 7 days |
| **Rewards** | gmMITO | gmMITO | None (is the reward) |
| **Use Case** | Collateral provider | Liquid staking | Governance |

## How to Use the Vaults

### Getting Started

**Option 1: Provide Collateral**
1. Have WMITO tokens
2. Deposit to mMITOc vault
3. Receive mMITOc shares
4. Earn operator rewards over time

**Option 2: Liquid Staking**
1. Have tMITO tokens
2. Stake to mMITOs vault
3. Receive equal mMITOs tokens
4. Earn staking rewards over time

### Earning and Claiming Rewards

1. **Accumulate rewards** in mMITOc or mMITOs
2. **Claim rewards** through gmMITO vault
3. **Receive gmMITO** shares automatically
4. **Compound or withdraw** as needed

### Withdrawing

All vaults use the same withdrawal process:

1. **Request withdrawal** → Burn your vault tokens
2. **Receive NFT** → Get a withdrawal NFT
3. **Wait 7 days** → Time lock period
4. **Claim assets** → Burn NFT to receive assets

[Learn more about Withdrawal NFTs →](../withdrawal/withdrawal-nft.md)

## Common Questions

### Which vault should I use?

**Use mMITOc if:**
- You want to provide validator collateral
- You're comfortable with slashing risk
- You want potentially higher rewards

**Use mMITOs if:**
- You want simple liquid staking
- You want to avoid slashing risk on principal
- You want to use your staked tokens in DeFi

**Use gmMITO if:**
- You want to convert rewards to governance tokens
- You want automatic compounding
- You want to participate in governance

### Can I use multiple vaults?

Yes! You can:
- Deposit to both mMITOc and mMITOs
- Earn rewards from both
- Claim all rewards to gmMITO
- Participate in governance

### What are the risks?

**mMITOc**:
- Slashing risk (validator misbehavior)
- Exchange rate can decrease

**mMITOs**:
- Validator downtime (lower rewards)
- No slashing on principal

**gmMITO**:
- Governance token value fluctuation

**All vaults**:
- 7-day withdrawal lock
- Smart contract risk

### How do rewards work?

1. Validators generate rewards from operations
2. Protocol distributes rewards to vault participants
3. You accumulate rewards over time
4. Claim rewards as gmMITO tokens
5. Optionally compound in gmMITO vault

## Security Features

- **Time-locked withdrawals**: 7-day period prevents rapid extraction
- **Oracle verification**: Tracks validator state accurately
- **Slashing detection**: Automatically adjusts for penalties
- **Upgradeable contracts**: Can be improved over time
- **Role-based permissions**: Different access levels for different operations

## Example Scenarios

### Scenario 1: Collateral Provider
```
Day 1:  Deposit 1000 WMITO to mMITOc
        → Receive ~950 mMITOc shares (varies by exchange rate)

Day 30: Earned 10 gmMITO worth of rewards
        → Claim to gmMITO vault

Day 60: Want to withdraw
        → Request withdrawal of all mMITOc
        → Receive Withdrawal NFT

Day 67: NFT matures (7 days later)
        → Claim NFT
        → Receive WMITO back (amount based on exchange rate)
```

### Scenario 2: Liquid Staker
```
Day 1:  Stake 500 tMITO to mMITOs
        → Receive exactly 500 mMITOs tokens

Day 1:  Use 500 mMITOs in DeFi protocol
        → Still earning staking rewards

Day 30: Earned 5 gmMITO worth of rewards
        → Claim to gmMITO vault

Day 60: Return 500 mMITOs from DeFi
        → Request unstake
        → Receive Withdrawal NFT

Day 67: Claim NFT
        → Receive exactly 500 tMITO (1:1)
```

### Scenario 3: Governance Participant
```
Day 1:  Have rewards in mMITOc and mMITOs

Day 1:  Claim all rewards
        → Automatically mint gmMITO shares

Day 30: gmMITO exchange rate increased (compounding)
        → Your share value increased

Day 30: Participate in governance vote
        → Use gmMITO voting power

Day 60: Want to withdraw governance tokens
        → Request withdrawal
        → Receive Withdrawal NFT

Day 67: Claim NFT
        → Receive govMITO tokens
```

## Related Documentation

- [Withdrawal NFT System](../withdrawal/withdrawal-nft.md)
- [Contracts Overview](../overview.md)
