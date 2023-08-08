## [GoGoPool Overview](https://audits.sherlock.xyz/contests/51)

| Protocol | Website     | Twitter     | Contest Pot  | Length  | Time spent |
|----------|-------------|-------------|--------------|---------|------------|
| GoGoPool | [Website]() | [Twitter]() | 128,000 USDC | 19 days | < 15 Hours |

### About GoGoPool

This is a contest to evaluate the entirety of the GoGoPool Protocol, a decentralized liquid staking protocol on Avalanche. Our mission is to be the easiest way to stake AVAX. GoGoPool allows users with hardware and 1000 AVAX to create a validator node in conjunction with funds deposited by liquid staking users.
### Findings Summary

| Risk   | Title                                                                             |
|--------|-----------------------------------------------------------------------------------|
| [M-01] | feeRecipient can be set to address(0) even if feeMantissa is more than zero       |
