# Withdrawal NFT System

When you request a withdrawal from any Munja vault, you receive an ERC721 NFT that represents your pending withdrawal. This NFT can be claimed for your assets after a time lock period.

## What is a Withdrawal NFT?

A Withdrawal NFT is a digital certificate that proves you have a pending withdrawal. Think of it like a ticket you can redeem later for your assets.

**Key Properties**:
- Standard ERC721 NFT (compatible with wallets and marketplaces)
- Contains information about your withdrawal amount
- Has a maturity date (when you can claim)
- Transferable to other addresses
- Displays as a visual card in NFT viewers

## How It Works

### 1. Request Withdrawal

When you withdraw from a vault:
- Your vault tokens/shares are burned
- A Withdrawal NFT is minted to your address
- The NFT contains:
  - Amount of assets you'll receive
  - Timestamp of when you can claim
  - Which token you'll receive (WMITO, tMITO, or govMITO)

### 2. Wait for Maturity

- Each NFT has a **time lock period** (typically 7 days)
- You must wait until the maturity date
- During this time, you can:
  - View the NFT in your wallet
  - Transfer it to another address
  - List it on NFT marketplaces

### 3. Claim Your Assets

After the time lock expires:
- Call the claim function with your NFT ID(s)
- The NFT is burned
- You receive your underlying assets

## Example User Flow

### From mMITOc (Collateral Vault):
```
1. You request withdrawal of 1000 WMITO
2. Your mMITOc shares are burned
3. You receive NFT #123
4. NFT shows: "1000 WMITO claimable in 7 days"
5. Wait 7 days
6. Claim NFT #123
7. Receive 1000 WMITO
```

### From mMITOs (Staking Vault):
```
1. You unstake 500 tMITO
2. Your mMITOs tokens are burned
3. You receive NFT #456
4. NFT shows: "500 tMITO claimable in 7 days"
5. Wait 7 days
6. Claim NFT #456
7. Receive 500 tMITO
```

### From gmMITO (Governance Vault):
```
1. You withdraw 100 govMITO worth
2. Your gmMITO shares are burned
3. You receive NFT #789
4. NFT shows: "100 govMITO claimable in 7 days"
5. Wait 7 days
6. Claim NFT #789
7. Receive 100 govMITO
```

## NFT Features

### Visual Display

The NFT displays as a professional card showing:
- Token ID number
- Amount of assets you'll receive
- Asset type (WMITO, tMITO, govMITO)
- Creation timestamp

### OpenSea & Marketplace Support

The NFT works with all major NFT platforms:
- Displays on OpenSea, Rarible, LooksRare
- Shows metadata and properties
- Can be bought/sold/transferred
- Has on-chain SVG image

### Transferability

You can transfer your Withdrawal NFT:
```
Transfer NFT #123 → New owner can claim the assets
```

**Use cases**:
- Sell your pending withdrawal to get immediate liquidity
- Gift a withdrawal to another address
- Use as collateral (risky - depends on DeFi platform)

**Important**: Whoever owns the NFT at claim time receives the assets!

## Multiple Withdrawals

You can have multiple pending withdrawals:
- Each withdrawal = one NFT
- Track all your NFTs in your wallet
- Claim multiple NFTs at once for efficiency

**Example**:
```
NFT #100: 500 WMITO (matures in 2 days)
NFT #101: 300 WMITO (matures in 5 days)
NFT #102: 200 tMITO (matures in 1 day)

Claim all at once after they mature:
claimWithdraw([100, 101, 102])
```

## Time Lock Period

**Why have a time lock?**
- Protects against rapid extraction during market volatility
- Prevents exchange rate manipulation
- Gives protocol time to process withdrawals
- Standard security measure in DeFi

**Typical duration**: 7 days

**Cannot be bypassed**: You must wait the full period

## Checking Your NFTs

### In Your Wallet
- View NFTs in MetaMask, Rainbow, or any Web3 wallet
- See visual representation and metadata
- Check maturity status

### On NFT Marketplaces
- Browse to OpenSea or similar platform
- View your withdrawal NFTs
- Check properties: amount, timestamp, asset type

### In the DApp
- Protocol UI shows all your pending withdrawals
- Displays time remaining until maturity
- Shows claimable amount
- One-click claiming when ready

## Important Considerations

**Benefits**:
- Visual representation of pending withdrawals
- Transferable (can sell for immediate liquidity)
- Compatible with all NFT infrastructure
- Multiple withdrawals easily tracked
- Batch claiming supported

**Risks**:
- Must wait for time lock (no instant withdrawal)
- NFT can be transferred (don't send to wrong address!)
- Losing NFT = losing access to assets
- Exchange rate may change while waiting (mMITOc, gmMITO)

**Best Practices**:
- Keep NFTs in a secure wallet
- Don't transfer unless intentional
- Track maturity dates
- Claim promptly after maturity to receive assets

## Differences From Traditional Withdrawals

### Traditional Queue System:
- Position in queue (number)
- Cannot transfer your position
- Hard to visualize

### Munja NFT System:
- Visual NFT representation
- Fully transferable
- Compatible with NFT ecosystem
- Clear metadata and properties
- Can be traded on marketplaces

## Related Documentation

- [Vault Contracts](../vaults/README.md) - Learn about the three vault types
