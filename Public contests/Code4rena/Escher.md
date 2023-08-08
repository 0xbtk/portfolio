## [Escher Overview](https://code4rena.com/contests/2022-12-escher-contest#top)

| Protocol | Website     | Twitter     | Contest Pot | Length |
|----------|-------------|-------------|-------------|--------|
| Escher   | [404]() | [404](L) | 36,500 USDC | 3 days |

### About Escher

Escher is a decentralized curated marketplace for editioned artwork.

### Findings Summary

| Risk   | Title                                                                             |
|--------|-----------------------------------------------------------------------------------|
| [M-01] | call() should be used instead of transfer() M-2 Use safeMint instead of mint for ERC721       |

## call() should be used instead of transfer() M-2 Use safeMint instead of mint for ERC721

## Impact
If saleReceiver and feeReceiver where smart contracts and one of the scenarios described in the POC occurred, neither of them will be able to withdraw their funds, and they (funds) will be frozen in the contract, resulting in a loss of funds for both users and the protocol.

## Proof of Concept
Provide direct links to all referenced code in GitHub. Add screenshots, logs, or any other relevant proof that illustrates the concept.

## Tools Used

## Recommended Mitigation Steps
