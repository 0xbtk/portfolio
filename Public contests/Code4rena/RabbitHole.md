## [RabbitHole Overview](https://code4rena.com/contests/2023-01-rabbithole-quest-protocol-contest#top)

| Protocol | Website     | Twitter     | Contest Pot | Length | Time spent |
|----------|-------------|-------------|-------------|--------|------------|
| RabbitHole | [Website](https://rabbithole.gg/) | [Twitter](https://twitter.com/rabbithole_gg) | 36,500 USDC | 5 days | < 1 Hour  |

### About RabbitHole

Quests Protocol is a protocol to distribute token rewards for completing on-chain tasks.

### Findings Summary

| Risk   | Title                                                                             |
|--------|-----------------------------------------------------------------------------------|
| [H-01] | onlyMinter() modifier is not working as expected       |


## [H-01] onlyMinter() modifier is not working as expected

## Impact

onlyMinter() can be bypasssed by anyone due to an invalid check.

## Proof of Concept

***`onlyMinter()` can be bypasssed by anyone due to an invalid check:***

```solidity
modifier onlyMinter() {
    msg.sender == minterAddress;
    _;
}
```

***Thus, everyone can mint tokens:***

```solidity
function mint(address to_, string memory questId_) public onlyMinter {
    _tokenIds.increment();
    uint newTokenID = _tokenIds.current();
    questIdForTokenId[newTokenID] = questId_;
    timestampForTokenId[newTokenID] = block.timestamp;
    _safeMint(to_, newTokenID);
}
```

## Tools Used

Manual review

## Recommended Mitigation Steps

***Replace the affected modifier by this one:***

```solidity
modifier onlyMinter() {
    require(msg.sender == minterAddress, "Only minter can mint tokens");
    _;
}
```
