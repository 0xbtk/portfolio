## [Caviar Overview](https://audits.sherlock.xyz/contests/51)

| Protocol | Website     | Twitter     | Contest Pot | Length | Time spent |
|----------|-------------|-------------|-------------|--------|------------|
| Caviar   | [Website](https://www.caviar.sh/) | [Twitter](https://twitter.com/caviarAMM) | 47,000 USDC | 6 days | < 1 Hour  |

### About Caviar

A private pool is a an NFT AMM controlled by a single owner. Each private pool is highly customizable with concentrated liquidity, custom fee rates, stolen NFT filtering, custom NFT weightings, royalty support, and flash loans.
### Findings Summary

| Risk   | Title                                                                             |
|--------|-----------------------------------------------------------------------------------|
| [M-01] | feeRecipient can be set to address(0) even if feeMantissa is more than zero       |
