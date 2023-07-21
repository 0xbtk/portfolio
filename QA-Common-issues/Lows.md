| Total Low issues |
|------------------|

| Risk   | Issues Details                                                                      | Number        |
|--------|-------------------------------------------------------------------------------------|---------------|
| [L-**] | Low level calls with solidity version 0.8.14 and lower can result in optimiser bug  |               |
| [L-**] | Critical changes should use-two step procedure                                      |               |
| [L-**] | Avoid using `tx.origin`                                                             |               |
| [L-**] | Avoid shadowing inherited state variables                                           |               |
| [L-**] | No Storage Gap for Upgradeable contracts                                            |               |
| [L-**] | Loss of precision due to rounding                                                   |               |
| [L-**] | Use `safeMint` instead of mint for ERC721                                           |               |
| [L-**] | ERC4626 does not work with fee-on-transfer tokens                                   |               |
| [L-**] | ERC4626Cloned 's implmentation is not fully up to EIP-4626's specification          |               |
| [L-**] | Lack of `nonReentrant` modifier                                                     |               |
| [L-**] | Take warnings seriously                                                             |               |
| [L-**] | Solmate's SafeTransferLib doesn't check whether the ERC20 contract exists           |               |
| [L-**] | `call()` should be used instead of `transfer()`                                     |               |
| [L-**] | Payout may be too soon                                                              |               |
| [L-**] | Integer overflow by unsafe casting                                                  |               |
| [L-**] | Allows malleable `SECP256K1` signatures                                             |               |
| [L-**] | Add `address(0)` check for the critical changes                                     |               |
| [L-**] | Multiple Pragma used                                                                |               |
| [L-**] | Array lengths not checked                                                           |               |
| [L-**] | The protocol is using `draft-****.sol` which is deprecated                          |               |
| [L-**] | Missing Event for initialize                                                        |               |
| [L-**] | `admin` can renounce while system is paused                                         |               |
| [L-**] | Using `>/>=` without specifying an upper bound is unsafe                            |               |
| [L-**] | Not all tokens support approve-max                                                  |               |

## [L-**] Low level calls with solidity version 0.8.14 and lower can result in optimiser bug

#### Description

The protocol is using low level calls with solidity version 0.8.12 which can result in optimizer bug.

> Ref: https://medium.com/certora/overly-optimistic-optimizer-certora-bug-disclosure-2101e3f7994d

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Consider upgrading to solidity 0.8.17

## [L-**] Critical changes should use-two step procedure

#### Description

The following contract have a function that allows them an owner to change it to a different address. If the owner accidentally uses an invalid address for which they do not have the private key, then the system will gets locked.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Consider adding two step procedure on the critical functions where the first is announcing a pending new owner and the new address should then claim its ownership.

A similar issue was reported in a previous contest and was assigned a severity of medium: code-423n4/2021-06-realitycards-findings#105

## [L-**] Avoid using `tx.origin`

#### Description

`tx.origin` is a global variable in Solidity that returns the address of the account that sent the transaction.

Using the variable could make a contract vulnerable if an authorized account calls a malicious contract. You can impersonate a user using a third party contract.

#### Lines of code 

- []()

## [L-**] Avoid shadowing inherited state variables

#### Description

In `****.sol` there is a local variables named `****` `****`, but there is functions and state variables in the inherited contracts ( `****.sol` `****.sol` ) with the same name. This use causes compilers to issue warnings, negatively affecting checking and code readability.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Avoid using variables with the same name.

## [L-**] No Storage Gap for Upgradeable contracts

#### Description

For upgradeable contracts, inheriting contracts may introduce new variables. In order to be able to add new variables to the upgradeable contract without causing storage collisions, a storage gap should be added to the upgradeable contract.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Consider adding a storage gap at the end of the upgradeable contract:
```solidity
  /**
   * @dev This empty reserved space is put in place to allow future versions to add new
   * variables without shifting down storage in the inheritance chain.
   * See https://docs.openzeppelin.com/contracts/4.x/upgradeable#storage_gaps
   */
  uint256[50] private __gap;
```

## [L-**] Loss of precision due to rounding

#### Description

Loss of precision due to the nature of arithmetics and rounding errors.

#### Lines of code 

- []()

## [L-**] Use `safeMint` instead of mint for ERC721

## Impact

Users could lost their NFTs if `msg.sender` is a contract address that does not support `ERC721`, the NFT can be frozen in the contract forever.

As per the documentation of EIP-721:

> A wallet/broker/auction application MUST implement the wallet interface if it will accept safe transfers.

> Ref: https://eips.ethereum.org/EIPS/eip-721

As per the documentation of ERC721.sol by Openzeppelin:

> Ref: https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC721/ERC721.sol#L274-L285

### Lines of code

- []()

### Recommended Mitigation Steps 

Use [`_safeMint`](https://github.com/transmissions11/solmate/blob/main/src/tokens/ERC721.sol#L193-L202) instead of [`mint`](https://github.com/transmissions11/solmate/blob/main/src/tokens/ERC721.sol#L157-L170) to check received address support for ERC721 implementation.

## [L-**] ERC4626 does not work with fee-on-transfer tokens

#### Description

The ERC4626 deposit/mint functions do not work well with fee-on-transfer tokens as the `assets` variable is the pre-fee amount, including the fee, whereas the `totalAssets` do not include the fee anymore.

This can be abused to mint more shares than desired.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

`assets` should be the amount excluding the fee (i.e the amount the contract actually received), therefore it's recommended to use the balance change before and after the transfer instead of the amount.

## [L-**] ERC4626Cloned 's implmentation is not fully up to EIP-4626's specification

#### Description

Must return the maximum amount of shares mint would allow to be deposited to receiver and not cause a revert, which must not be higher than the actual maximum that would be accepted (it should underestimate if necessary).

This assumes that the user has infinite assets, i.e. must not rely on balanceOf of asset. Could cause unexpected behavior in the future due to non-compliance with EIP-4626 standard.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

`maxMint()` and `maxDeposit()` should reflect the limitation of maxSupply.

## [L-**] Lack of `nonReentrant` modifier

#### Description

It is a best practice to use the `nonReentrant` modifier when you make external calls to untrustable entities because even if an auditor did not think of a way to exploit it, an attacker just might.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Add reentrancy guard to the functions mentioned above.

## [L-**] Take warnings seriously

#### Description

If the compiler warns you about something, you should change it. Even if you do not think that this particular warning has security implications, there might be another issue buried beneath it. Any compiler warning we issue can be silenced by slight changes to the code.

> Ref: https://docs.soliditylang.org/en/v0.8.17/security-considerations.html#take-warnings-seriously

#### Lines of code 

- []()

## [L-**] Solmate's SafeTransferLib doesn't check whether the ERC20 contract exists

#### Description

Solmate's `SafeTransferLib.sol`, which is often used to interact with non-compliant/unsafe ERC20 tokens, does not check whether the ERC20 contract exists. The following code will not revert in case the token doesn't exist.

> Ref: https://github.com/transmissions11/solmate/blob/main/src/utils/SafeTransferLib.sol#L9

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Add a contract exist check in functions or use Openzeppelin `safeERC20` instead.

## [L-**] `call()` should be used instead of `transfer()`

#### Description

The use of the deprecated ```transfer()``` function for a payable address will certainly make the transaction fail when:

1. The claimer smart contract does not implement a payable fallback function.

2. The claimer smart contract does implement a payable fallback which uses more than 2300 gas unit.

3. The claimer smart contract implements a payable fallback function that needs less than 2300 gas units but is called through proxy, raising the call's gas usage above 2300.

4. Some multisig wallets might also require higher gas than 2300.

A more detailed explanation can be found [here](https://consensys.net/diligence/blog/2019/09/stop-using-soliditys-transfer-now/).

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Consider using `call()` instead with the CEI pattern implemented correctly.

## [L-**] Payout may be too soon

#### Description

The first timestamp should be based on when rewards are first payed, so that an appropriate duration of the cycle occurs, rather than during deployment.

#### Lines of code 

- []()

## [L-**] Integer overflow by unsafe casting

#### Description

Keep in mind that the version of solidity used, despite being greater than 0.8, does not prevent integer overflows during casting, it only does so in mathematical operations.

It is necessary to safely convert between the different numeric types.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use OpenZeppelin [safeCast](https://docs.openzeppelin.com/contracts/3.x/api/utils#SafeCast) library.

## [L-**] Allows malleable `SECP256K1` signatures

#### Description

Here, the `ecrecover()` method doesn't check the `bytes32 s` range.

Homestead [`EIP-2`](https://eips.ethereum.org/EIPS/eip-2) added this limitation, however the precompile remained unaltered. The majority of libraries, including OpenZeppelin, do this check.

> Ref: https://github.com/OpenZeppelin/openzeppelin-contracts/blob/7201e6707f6631d9499a569f492870ebdd4133cf/contracts/utils/cryptography/ECDSA.sol#L138-L149

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use OpenZeppelin's [`ECDSA`](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/cryptography/ECDSA.sol) library for signature verification.

## [L-**] Add `address(0)` check for the critical changes

#### Description

Check of `address(0)` to protect the code from `(0x0000000000000000000000000000000000000000)` address problem just in case. This is best practice or instead of suggesting that they verify `_address != address(0)`, you could add some good NatSpec comments explaining what is valid and what is invalid and what are the implications of accidentally using an invalid address.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Add checks for `address(0)` when assigning values to address state variables.	

## [L-**] Multiple Pragma used 

#### Description

Solidity pragma versions should be exactly same in all contracts. Currently some contracts use `^0.8.**` and others use `^0.8.**`

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use one version for all contracts.

## [L-**] Array lengths not checked

#### Description

If the length of the arrays are not required to be of the same length, user operations may not be fully executed.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

 Check that the arrays length are the same.
 
 ## [L-**] The protocol is using `draft-****.sol` which is deprecated

#### Description

While OpenZeppelin draft contracts are safe to use and have been audited, their 'draft' status means that the EIPs they're based on are not finalized, and thus there may be breaking changes in even [minor releases](https://docs.openzeppelin.com/contracts/3.x/api/drafts). If a bug is found in this version of OpenZeppelin, and the version that you're forced to upgrade to has breaking changes in the new version, you'll encounter unnecessary delays in porting and testing replacement contracts. Ensure that you have extensive test coverage of this area so that differences can be automatically detected, and have a plan in place for how you would fully test a new version of these contracts if they do indeed change unexpectedly.

> [Refrence]()

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Consider creating a forked version of the file rather than importing it from the package, and manually patch your fork as changes are made.

## [L-**] Missing Event for initialize

#### Description

Events help non-contract tools to track changes, and events prevent users from being surprised by changes Issuing event-emit during initialization is a detail that many projects skip.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Add Event-Emit

## [L-**] `admin` can renounce while system is paused

#### Description

The contract `admin` is not prevented from renouncing the role/ownership while the contract is paused, which would cause any user assets stored in the protocol, to be locked indefinitely.

#### Lines of code 

- []()

## [L-**] Using `</<=` without specifying an upper bound is unsafe

#### Description

There will be breaking changes in future versions of solidity, and at that point your code will no longer be compatable. While you may have the specific version to use in a configuration file, others that include your source files may not.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use a fixed version of solidity.
 
## [L-**] Not all tokens support approve-max

#### Description

Some tokens consider uint256 as just another value. If one of these tokens is used and the approval balance eventually reaches only a couple wei, nobody will be able to send funds because there won't be enough approval.

#### Lines of code 

- []()

