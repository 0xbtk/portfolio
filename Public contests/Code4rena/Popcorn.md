## [Popcorn Overview](https://code4rena.com/contests/2023-01-popcorn-contest#top)

| Protocol | Website     | Twitter     | Contest Pot | Length | Time spent |
|----------|-------------|-------------|-------------|--------|------------|
| Popcorn    | [Website](https://pop.network/) | [Twitter](https://twitter.com/Popcorn_DAO) | 90,500 USDC | 7 days | < 3 Hour  |

### About Popcorn

This protocols goal is to make vault creation easy, safe and all without compromising on flexibility. It allows anyone to spin up their own Yearn in minutes.

### Findings Summary

| Risk   | Title                                                                             |
|--------|-----------------------------------------------------------------------------------|
| [H-01] | Reentrancy on `MultiRewardStaking.claimRewards()` when the rewardToken is an ERC777 token       |
| [M-01] | ERC4626 does not work with fee-on-transfer tokens       |

## [H-01] Reentrancy on `MultiRewardStaking.claimRewards()` when the rewardToken is an ERC777 token

## Impact

[Reentrancy](https://hackernoon.com/hack-solidity-reentrancy-attack) attack allows to drain [`MultiRewardStaking.sol`](https://github.com/code-423n4/2023-01-popcorn//blob/main/src/utils/MultiRewardStaking.sol) funds due to non-adherence with CEI pattern.

## Proof of Concept

*Note: There is no re-entry risk on true ERC-20 tokens that work according to the spec, however ERC777 tokens can and they can maskerade as ERC20. So if a contract interacts with unknown ERC20 tokens it is better to be safe and consider that transfers can create reentrancy problems.*

When the attacker call [`claimRewards()`](https://github.com/code-423n4/2023-01-popcorn//blob/main/src/utils/MultiRewardStaking.sol#L170), the function will revert if any of the rewardTokens have zero rewards accrued, and a percentage of each reward can be locked in an escrow contract if this was previously configured.

```solidity
  function claimRewards(address user, IERC20[] memory _rewardTokens) external accrueRewards(msg.sender, user) {
    for (uint8 i; i < _rewardTokens.length; i++) {
      uint256 rewardAmount = accruedRewards[user][_rewardTokens[i]];

      if (rewardAmount == 0) revert ZeroRewards(_rewardTokens[i]);

      EscrowInfo memory escrowInfo = escrowInfos[_rewardTokens[i]];

      if (escrowInfo.escrowPercentage > 0) {
        _lockToken(user, _rewardTokens[i], rewardAmount, escrowInfo);
        emit RewardsClaimed(user, _rewardTokens[i], rewardAmount, true);
      } else {
        _rewardTokens[i].transfer(user, rewardAmount);
        emit RewardsClaimed(user, _rewardTokens[i], rewardAmount, false);
      }

      accruedRewards[user][_rewardTokens[i]] = 0;
    }
  }
```

What is interesting for us is this check `if (rewardAmount == 0) revert ZeroRewards(_rewardTokens[i]);`, this check is done in the top of function. Therefore, when the attacker [`escrowInfo.escrowPercentage > 0`](https://github.com/code-423n4/2023-01-popcorn//blob/main/src/utils/MultiRewardStaking.sol#L178), the [`_lockToken`](https://github.com/code-423n4/2023-01-popcorn//blob/main/src/utils/MultiRewardStaking.sol#L191) function will get executed:

```solidity
  function _lockToken(
    address user,
    IERC20 rewardToken,
    uint256 rewardAmount,
    EscrowInfo memory escrowInfo
  ) internal {
    uint256 escrowed = rewardAmount.mulDiv(uint256(escrowInfo.escrowPercentage), 1e18, Math.Rounding.Down);
    uint256 payout = rewardAmount - escrowed;

    rewardToken.safeTransfer(user, payout);
    escrow.lock(rewardToken, user, escrowed, escrowInfo.escrowDuration, escrowInfo.offset);
  }
```

Which will than transfer the `payout` to the attacker through [`SafeERC20.safeTransfer`](https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/blob/master/contracts/token/ERC20/utils/SafeERC20Upgradeable.sol#L22), thus the ERC777 hook get triggered which will allow the attacker to reenter and claim again because the [`claimRewards()`](https://github.com/code-423n4/2023-01-popcorn//blob/main/src/utils/MultiRewardStaking.sol#L170) didn't update its state before making an external call as you can see on line [186](https://github.com/code-423n4/2023-01-popcorn//blob/main/src/utils/MultiRewardStaking.sol#L186).

## Tools Used

Manual Review

## Recommended Mitigation Steps

***Follow the CEI pattern:***

```solidity
  function claimRewards(address user, IERC20[] memory _rewardTokens) external accrueRewards(msg.sender, user) {
    for (uint8 i; i < _rewardTokens.length; i++) {
      uint256 rewardAmount = accruedRewards[user][_rewardTokens[i]];

      if (rewardAmount == 0) revert ZeroRewards(_rewardTokens[i]);

      EscrowInfo memory escrowInfo = escrowInfos[_rewardTokens[i]];
      
      accruedRewards[user][_rewardTokens[i]] = 0;

      if (escrowInfo.escrowPercentage > 0) {
        _lockToken(user, _rewardTokens[i], rewardAmount, escrowInfo);
        emit RewardsClaimed(user, _rewardTokens[i], rewardAmount, true);
      } else {
        _rewardTokens[i].transfer(user, rewardAmount);
        emit RewardsClaimed(user, _rewardTokens[i], rewardAmount, false);
      }
    }
  }
```

***or use OpenZeppelin [`ReentrancyGuardUpgradeable.sol`](https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/blob/master/contracts/security/ReentrancyGuardUpgradeable.sol).***

## [M-01] ERC4626 does not work with fee-on-transfer tokens

## Impact

The fee on transfer can be abused to mint more shares than desired.

## Proof of Concept

The ERC4626 deposit/mint functions do not work well with fee-on-transfer tokens as the assets variable is the pre-fee amount, including the fee, whereas the totalAssets do not include the fee anymore.

This can be abused to mint more shares than desired.

## Tools Used

Manual review

## Recommended Mitigation Steps

Assets should be the amount excluding the fee (i.e the amount the contract actually received), therefore it's recommended to use the balance change before and after the transfer instead of the amount.
