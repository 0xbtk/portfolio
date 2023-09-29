## [Maia Overview](https://code4rena.com/contests/2023-05-maia-dao-ecosystem#top)

| Protocol   | Website     | Twitter     | Contest Pot | Length | Time spent |
|------------|-------------|-------------|-------------|--------|--------|
| Maia | [Website](https://maiadao.io) | [Twitter](https://twitter.com/MaiaDAOEco) | 300,500 USDC | 1 motnh | < 8 Hours |

### About Stakehouse

Maia DAO V2 Ecossytem docs that explains the business logic and technical references, can be found [here](https://v2-docs.maiadao.io/). Docs are split into 4 protocols, in which you will find relevant information about how each of these protocols work in the system.

### Findings Summary

| Risk   | Title                                                         |
|--------|---------------------------------------------------------------|
| [M-01] | Reentrancy attack may occur on withdraw ETH For Knot function |

## [M-01] holders will not have enough time to delegate or cast their votes

## Impact

Note: The sponsor [message](https://discord.com/channels/810916927919620096/1110626768223739924/1116673692588589106) on which networks project will be deployed. 

Vote period/delay will not work correctly on L2s due to the use of `block.number`, which may not give holders enough time to delegate or cast before the voting delay or period ends.

## Proof of Concept

```solidity
    uint256 public constant MIN_VOTING_PERIOD = 80640; // About 2 weeks

    /// @notice The max setable voting period
    uint256 public constant MAX_VOTING_PERIOD = 161280; // About 4 weeks

    /// @notice The min setable voting delay
    uint256 public constant MIN_VOTING_DELAY = 40320; // About 1 weeks

    /// @notice The max setable voting delay
    uint256 public constant MAX_VOTING_DELAY = 80640; // About 2 weeks
```

Each of these values represent a specific period in ethereum blocks (.i.e 12s), but all of this values will not give the holders enough time when deploying on L2s.

Here is a simple comparison of block times across different networks:

| Network               | Block time |
|-----------------------|------------|
| Ethereum mainnet      | 12 s       |
| Arbitrum              | 2 s        |
| Optimism              | 2 s        |
| Polygon               | 2 s        |
| Binance               | 3 s        |
| Metis                 | 2 s        |
| Fantom                | 1 s        |
| Avalanche             | 3 s        |

## Tools Used

Manual Review

## Recommended Mitigation Steps

We recommend using `block.timestamp` instead of `block.number`.
