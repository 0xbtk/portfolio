## [Caviar Overview](https://code4rena.com/contests/2023-04-caviar-private-pools#top)

| Protocol | Website     | Twitter     | Contest Pot | Length | Time spent |
|----------|-------------|-------------|-------------|--------|------------|
| Caviar   | [Website](https://www.caviar.sh/) | [Twitter](https://twitter.com/caviarAMM) | 47,000 USDC | 6 days | < 1 Hour  |

### About Caviar

A private pool is a an NFT AMM controlled by a single owner. Each private pool is highly customizable with concentrated liquidity, custom fee rates, stolen NFT filtering, custom NFT weightings, royalty support, and flash loans.

### Findings Summary

| Risk   | Title                                                                             |
|--------|-----------------------------------------------------------------------------------|
| [H-01] | Integer overflow by unsafe casting       |

## [H-01] Integer overflow by unsafe casting

## Impact

Possible interflow due to unsafe casting

## Proof of Concept

Keep in mind that the version of solidity used, despite being greater than 0.8, does not prevent integer overflows during casting, it only does so in mathematical operations.

It is necessary to safely convert between the different numeric types.

```solidity
        virtualBaseTokenReserves += uint128(netInputAmount - feeAmount - protocolFeeAmount); 
```

## Tools Used

Manual review

## Recommended Mitigation Steps

Use OpenZeppelin safeCast library.
