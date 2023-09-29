## [Lybra Overview](https://code4rena.com/contests/2023-06-lybra-finance#top)

| Protocol   | Website     | Twitter     | Contest Pot | Length | Time spent |
|------------|-------------|-------------|-------------|--------|--------|
| Lybra      | [Website](https://lybra.finance/) | [Twitter](https://twitter.com/LybraFinance) | 60,500 USDC | 10 days | < 7 Hours |

### About Stakehouse

Lybra Finance is a groundbreaking DeFi protocol focused on bringing stability to the volatile cryptocurrency market through its innovative stablecoin, eUSD. Built on LSD/LST's, the protocol initially utilizes Lido Finance-issued stETH as its primary components and plans to support additional LST's in the upcoming V2.

### Findings Summary

| Risk   | Title                                                         |
|--------|---------------------------------------------------------------|
| [M-01] | Reentrancy attack may occur on withdraw ETH For Knot function |

## [M-01] `votingDelay()` and `votingPeriod()` will not work properly for Arbitrum due to block.number

## Impact

Note: The sponsor [message](https://discord.com/channels/810916927919620096/1121168405534343270/1121917925977235646) on which networks project will be deployed. 

Vote delay will not work correctly on Arbitrum due to the use of `block.number`, which may not give users enough time to buy voting power, or delegate it, before the voting of a proposal ends.

## Proof of Concept

This function represents the delay between the proposal is created and the vote starts:

```solidity
     function votingDelay() public pure override returns (uint256){
         return 1;
    }
```

And this function represents the delay between the vote start and vote end: 

```solidity
    function votingPeriod() public pure override returns (uint256){
         return 3;
    }
```

Both this function enforces a block delay. While this structure will work on mainnet, it is problematic for use on Arbitrum. According to Arbitrum [Docs](https://developer.arbitrum.io/time) `block.number` returns the most recently synced L1 `block.number`. Once per minute the `block.number` in the Sequencer is synced to the actual L1 `block.number` (This may introduce potential vulnerabilities in the governance system), and the fact that Arbitrum block time is 2-second. Thus users will not have enough time to buy voting power, or delegate it, before the voting of a proposal ends.

## Tools Used

Manual Review

## Recommended Mitigation Steps

We recommend using `block.timestamp` instead of `block.number` when deploying on L2s.
