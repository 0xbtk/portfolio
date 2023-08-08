## [RabbitHole Overview](https://audits.sherlock.xyz/contests/51)

| Protocol | Website     | Twitter     | Contest Pot | Length | Time spent |
|----------|-------------|-------------|-------------|--------|------------|
| RabbitHole | [Website](https://rabbithole.gg/) | [Twitter](https://twitter.com/rabbithole_gg) | 36,500 USDC | 5 days | < 1 Hour  |

### About RabbitHole

Quests Protocol is a protocol to distribute token rewards for completing on-chain tasks.

### Findings Summary

| Risk   | Title                                                                             |
|--------|-----------------------------------------------------------------------------------|
| [H-01] | feeRecipient can be set to address(0) even if feeMantissa is more than zero       |
