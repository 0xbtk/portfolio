## [Stakehouse Overview](https://code4rena.com/contests/2022-11-lsd-network-stakehouse-contest#top)

| Protocol   | Website     | Twitter     | Contest Pot | Length | Time spent |
|------------|-------------|-------------|-------------|--------|--------|
| Stakehouse | [Website](https://docs.joinstakehouse.com/) | [Twitter](https://twitter.com/blockswap_team/) | 90,500 USDC | 7 days | < 8 Hours |

### About Stakehouse

Liquid Staking Derivative (LSD) Networks are permissionless networks deployed on top of the Stakehouse protocol that serves as an abstraction for consensus layer assets. LSD participants can enjoy fractionalized validator ownership with deposits as little as 0.001 ether.

### Findings Summary

| Risk   | Title                                                         |
|--------|---------------------------------------------------------------|
| [H-01] | Reentrancy attack may occur on withdraw ETH For Knot function |
| [M-01] | Reentrancy attack may occur on withdraw ETH For Knot function |

## [H-01] Reentrancy attack may occur on withdraw ETH For Knot function

## Impact
A reentrancy attack can occur when the contract fails to update its state before the interaction, the attacker can make a recursive call back to the original function in an attempt to drain funds.

## Proof of Concept

*The below scenario would be possible:*

Since the node runner could be a smart contract, the contract could have a malicious code so when withdrawETHForKnot get called, it goes in infinite loop in attempt to drain all the funds.

```solidity
    function withdrawETHForKnot(address _recipient, bytes calldata _blsPublicKeyOfKnot) external {
        require(_recipient != address(0), "Zero address");
        require(isBLSPublicKeyBanned(_blsPublicKeyOfKnot) == false, "BLS public key has already withdrawn or not a part of LSD network");

        address associatedSmartWallet = smartWalletOfKnot[_blsPublicKeyOfKnot];
        require(smartWalletOfNodeRunner[msg.sender] == associatedSmartWallet, "Not the node runner for the smart wallet ");
        require(isNodeRunnerBanned(nodeRunnerOfSmartWallet[associatedSmartWallet]) == false, "Node runner is banned from LSD network");
        require(associatedSmartWallet.balance >= 4 ether, "Insufficient balance");
        require(
            getAccountManager().blsPublicKeyToLifecycleStatus(_blsPublicKeyOfKnot) == IDataStructures.LifecycleStatus.INITIALS_REGISTERED,
            "Initials not registered"
        );

        // refund 4 ether from smart wallet to node runner's EOA
        IOwnableSmartWallet(associatedSmartWallet).rawExecute(
            _recipient,
            "",
            4 ether
        );

        // update the mapping
        bannedBLSPublicKeys[_blsPublicKeyOfKnot] = associatedSmartWallet;

        emit ETHWithdrawnFromSmartWallet(associatedSmartWallet, _blsPublicKeyOfKnot, msg.sender);
    }
```

## Tools Used

Manual Review

## Recommended Mitigation Steps

Use a reentrancy guard.

## [M-01] Due to incorrect require statements, the function always revert

## Impact
Since the function always revert Due to incorrect require statements, there is no way to add or remove a whitelisted node runner. Therefore, the functions ```registerBLSPublicKeys``` that require for a node runner to be whitelisted will also revert.

## Proof of Concept
```solidity
require(isNodeRunnerWhitelisted[_nodeRunner] != isNodeRunnerWhitelisted[_nodeRunner], "Unnecessary update to same status");
```
In this require statement you are basically saying that if a node runner is whitelisted than require that is not whitelisted and vice versa.

## Tools Used
Manual review

## Recommended Mitigation Steps
```solidity
Fix:

// Replace the incorrect require statement with this one.
require(isWhitelisted != isNodeRunnerWhitelisted[_nodeRunner], "Unnecessary update to same status");
```
