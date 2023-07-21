| Total Non-Critical issues |
|---------------------------|
 
| Number  | Issues Details                                                                               | Context |
|---------|----------------------------------------------------------------------------------------------|---------|
| [NC-**] | Include return parameters in NatSpec comments                                                |         |
| [NC-**] | Non-usage of specific imports                                                                |         |
| [NC-**] | Use `require()` instead of `assert()`                                                        |         |
| [NC-**] | Lack of event emit                                                                           |         |
| [NC-**] | Require messages are too short and unclear                                                   |         |
| [NC-**] | Unused `receive()` Function Will Lock Ether In Contract                                      |         |
| [NC-**] | Critical changes should use-two step procedure                                               |         |
| [NC-**] | Solidity compiler optimizations can be problematic                                           |         |
| [NC-**] | Mark visibility of `initialize()` functions as external                                      |         |
| [NC-**] | Use `bytes.concat()` and `string.concat()`                                                   |         |
| [NC-**] | Reusable require statements should be changed to a modifier                                  |         |
| [NC-**] | Use a more recent version of OpenZeppelin dependencies                                       |         |
| [NC-**] | The protocol should include NatSpec                                                          |         |
| [NC-**] | Constants in comparisons should appear on the left side                                      |         |
| [NC-**] | The `nonReentrant` modifier should occur before all other modifiers                          |         |
| [NC-**] | Use a more recent version of solidity                                                        |         |
| [NC-**] | Signature Malleability of EVM's `ecrecover()`                                                |         |
| [NC-**] | Use `immutable` instead of `constant` for values such as a call to `keccak256()`             |         |
| [NC-**] | `revert()` Statements Should Have Descriptive Reason Strings                                 |         |
| [NC-**] | Lock pragmas to specific compiler version                                                    |         |
| [NC-**] | There is no need to cast a variable that is already an uint, such as `uint(x)`               |         |
| [NC-**] | Assembly Codes Specific – Should Have Comments                                               |         |
| [NC-**] | Adding a `return` statement when the function defines a named return variable, is redundant  |         |
| [NC-**] | Add NatSpec Mapping comment                                                                  |         |
| [NC-**] | Constants should be defined rather than using magic numbers                                  |         |
| [NC-**] | There is no need to cast a variable that is already an address, such as `address(x)`         |         |
| [NC-**] | Not using the named return variables anywhere in the function is confusing                   |         |
| [NC-**] | Use `uint256` instead `uint`                                                                 |         |
| [NC-**] | Using vulnerable dependency of solmate                                                       |         |
| [NC-**] | Use scientific notation rather than exponentiation                                           |         |

## [NC-**] Include return parameters in NatSpec comments

#### Description

If Return parameters are declared, you must prefix them with `/// @return`.
Some code analysis programs do analysis by reading [NatSpec](https://docs.soliditylang.org/en/v0.8.15/natspec-format.html) details, if they can't see the `@return` tag, they do incomplete analysis.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Include `@return` parameters in NatSpec comments

## [NC-**] Non-usage of specific imports

#### Description

The current form of relative path import is not recommended for use because it can unpredictably pollute the namespace. Instead, the Solidity docs recommend specifying imported symbols explicitly. 

- https://docs.soliditylang.org/en/v0.8.15/layout-of-source-files.html#importing-other-source-files

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use specific imports syntax per solidity docs recommendation.

## [NC-**] Use `require()` instead of `assert()`

#### Description

Assert should not be used except for tests, require should be used

Prior to Solidity 0.8.0, pressing a confirm consumes the remainder of the process's available gas instead of returning it, as `request()/revert()` did.

The big difference between the two is that the `assert()` function when false, uses up all the remaining gas and reverts all the changes made.

Meanwhile, a `require()` statement when false, also reverts back all the changes made to the contract but does refund all the remaining gas fees we offered to pay. This is the most common Solidity function used by developers for debugging and error handling.

Assertion should be avoided even after solidity version 0.8.0, because its documentation states "The Assert function generates an error of type `Panic(uint256)`. Code that works properly should never Panic, even on invalid external input. If this happens, you need to fix it in your contract. there's a mistake".

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use `require()` instead of `assert()`

## [NC-**] Lack of event emit

#### Description

The below methods do not emit an event when the state changes, something that it's very important for dApps and users.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Emit event.

## [NC-**] Require messages are too short and unclear

#### Description

The correct and clear error description explains to the user why the function reverts, but the error descriptions below in the project are not self-explanatory. These error descriptions are very important in the debug features of DApps like Tenderly. Error definitions should be added to the require block, not exceeding 32 bytes.

#### Lines of code 

- []()

## [NC-**] Unused `receive()` Function Will Lock Ether In Contract

#### Description

If the intention is for the Ether to be used, the function should call another function, otherwise it should revert.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

The function should call another function, otherwise it should revert.

## [NC-**] Critical changes should use-two step procedure

#### Description

Lack of two-step procedure for critical operations leaves them error-prone.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Consider adding two step procedure on the critical functions.

## [NC-**] Solidity compiler optimizations can be problematic

#### Description

Protocol has enabled optional compiler optimizations in Solidity. There have been several optimization bugs with security implications. Moreover, optimizations are actively being developed. Solidity compiler optimizations are disabled by default, and it is unclear how many contracts in the wild actually use them.

Therefore, it is unclear how well they are being tested and exercised. High-severity security issues due to optimization bugs have occurred in the past. A high-severity bug in the emscripten-generated solc-js compiler used by Truffle and Remix persisted until late 2018. The fix for this bug was not reported in the Solidity CHANGELOG.

Another high-severity optimization bug resulting in incorrect bit shift results was patched in Solidity 0.5.6. More recently, another bug due to the incorrect caching of keccak256 was reported. A compiler audit of Solidity from November 2018 concluded that the optional optimizations may not be safe. It is likely that there are latent bugs related to optimization and that new bugs will be introduced due to future optimizations.

Exploit Scenario A latent or future bug in Solidity compiler optimizations—or in the Emscripten transpilation to solc-js—causes a security vulnerability in the contracts.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Short term, measure the gas savings from optimizations and carefully weigh them against the possibility of an optimization-related bug. Long term, monitor the development and adoption of Solidity compiler optimizations to assess their maturity.

## [NC-**] Mark visibility of `initialize()` functions as external

#### Description

- If someone wants to extend via inheritance, it might make more sense that the overridden `initialize()` function calls the internal {...}_init function, not the parent public `initialize()` function.

- External instead of public would give more the sense of the `initialize()` functions to behave like a constructor (only called on deployment, so should only be called externally)

- Security point of view, it might be safer so that it cannot be called internally by accident in the child contract

- It might cost a bit less gas to use external over public

- It is possible to override a function from external to public ("opening it up") but it is not possible to override a function from public to external ("narrow it down").

> Ref: https://github.com/OpenZeppelin/openzeppelin-contracts/issues/3750

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Change the visibility of `initialize()` functions to external

## [NC-**] Use `bytes.concat()` and `string.concat()`

#### Description

Solidity version 0.8.4 introduces: 

- `bytes.concat()` vs `abi.encodePacked(<bytes>,<bytes>)`
- `string.concat()` vs `abi.encodePacked(<string>,<string>)`

https://docs.soliditylang.org/en/v0.8.17/types.html?highlight=bytes.concat#the-functions-bytes-concat-and-string-concat

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use `bytes.concat()` and `string.concat()`

## [NC-**] Reusable require statements should be changed to a modifier

#### Description

Reusable require statements should be changed to a modifier.

#### Lines of code 

- []()

## [NC-**] Use a more recent version of OpenZeppelin dependencies

#### Description

For security, it is best practice to use the latest OpenZeppelin version.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Old version of OpenZeppelin is used `(4.6.0)`, newer version can be used [`(4.8.2)`](https://github.com/OpenZeppelin/openzeppelin-contracts/releases/tag/v4.8.2).

## [NC-**] The protocol should include NatSpec

#### Description

It is recommended that Solidity contracts are fully annotated using NatSpec, it is clearly stated in the Solidity official documentation.

- In complex projects such as Defi, the interpretation of all functions and their arguments and returns is important for code readability and auditability. 

- Some code analysis programs do analysis by reading NatSpec details, if they can't see the tags `(@param, @dev, @return)`, they do incomplete analysis.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Include [`NatSpec`](https://docs.soliditylang.org/en/v0.8.15/natspec-format.html) comments in the codebase.

## [NC-**] Constants in comparisons should appear on the left side

#### Description

Constants in comparisons should appear on the left side, doing so will prevent typo [bug](https://www.moserware.com/2008/01/constants-on-left-are-better-but-this.html).

```solidity
if (num == 0) revert();
```

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Constants should appear on the left side:

```solidity
if (0 == num) revert();
```

## [NC-**] The `nonReentrant` modifier should occur before all other modifiers

#### Description

This is a best-practice to protect against reentrancy in other modifiers.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use the `nonReentrant` modifier first.

## [NC-**] Use a more recent version of solidity

#### Description

For security, it is best practice to use the [latest Solidity version](https://github.com/ethereum/solidity/blob/develop/Changelog.md).

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Old version of Solidity is used `(0.8.**)`, newer version can be used `(0.8.19)`.

## [NC-**] Signature Malleability of EVM's `ecrecover()`

#### Description

The function calls the Solidity `ecrecover()` function directly to verify the given signatures. However, the `ecrecover()` EVM opcode allows malleable (non-unique) signatures and thus is susceptible to replay attacks.

Although a replay attack seems not possible for this contract, I recommend using the battle-tested OpenZeppelin's ECDSA library.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use the ecrecover function from OpenZeppelin's ECDSA library for signature verification. (Ensure using a version > 4.7.3 for there was a critical bug >= 4.1.0 < 4.7.3).

## [NC-**] Use `immutable` instead of `constant` for values such as a call to `keccak256()`

#### Description

While it doesn't save any gas because the compiler knows that developers often make this mistake, it's still best to use the right tool for the task at hand. There is a difference between constant variables and immutable variables, and they should each be used in their appropriate contexts. constants should be used for literal values written into the code, and immutable variables should be used for expressions, or values calculated in, or passed into the constructor.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use `immutable` instead of `constants` 

## [NC-**] `revert()` Statements Should Have Descriptive Reason Strings

#### Description

The correct and clear error description explains to the user why the function reverts, but the error descriptions below in the project are not self-explanatory. These error descriptions are very important in the debug features of DApps like Tenderly.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Error definitions should be added to the `revert("...")` block.

## [NC-**] Lock pragmas to specific compiler version

#### Description

Pragma statements can be allowed to float when a contract is intended for consumption by other developers, as in the case with contracts in a library or EthPM package. Otherwise, the developer would need to manually update the pragma in order to compile locally. 

> Ref: https://swcregistry.io/docs/SWC-103

#### Lines of code 

- []()

#### Recommended Mitigation Steps

[Ethereum Smart Contract Best Practices](https://consensys.github.io/smart-contract-best-practices/development-recommendations/solidity-specific/locking-pragmas/): Lock pragmas to specific compiler version. 

## [NC-**] There is no need to cast a variable that is already an uint, such as `uint256(x)`

#### Description

There is no need to cast a variable that is already an uint, such as uint256(0), 0 is also uint.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use directly variable.

## [NC-**] Assembly Codes Specific – Should Have Comments  

#### Description

Since this is a low level language that is more difficult to parse by readers, include extensive documentation, comments on the rationale behind its use, clearly explaining what each assembly instruction does

This will make it easier for users to trust the code, for reviewers to validate the code, and for developers to build on or update the code.

Note that using Aseembly removes several important security features of Solidity, which can make the code more insecure and more error-prone.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Include NatSpec in assembly codes.

## [NC-**] Adding a `return` statement when the function defines a named return variable, is redundant

#### Description

Adding a `return` statement when the function defines a named return variable, is redundant.

#### Lines of code 

- []()

## [NC-**] Add NatSpec Mapping comment  

#### Description

Add NatSpec comments describing mapping keys and values.

```solidity
mapping(address => uint) nonce; 
```

#### Lines of code 

- []()

#### Recommended Mitigation Steps

```solidity
/// @dev address(owner) => uint(nonce)
mapping(address => uint) nonce; 
```

## [NC-**] Constants should be defined rather than using magic numbers 

#### Description

Constants should be defined rather than using magic numbers.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Define a constant.

## [NC-**] There is no need to cast a variable that is already an address, such as `address(x)`

#### Description

There is no need to cast a variable that is already an `address`, such as `address(x)`, `x` is also `address`.

#### Lines of code 

- []()

#### Recommended Mitigation Steps     

## [NC-**] Not using the named return variables anywhere in the function is confusing

#### Description

Not using the named return variables anywhere in the function is confusing.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Consider changing the variable to be an unnamed one.

## [NC-**] Use `uint256` instead `uint`

#### Description

`** results in * files`.

Some developers prefer to use `uint256` because it is consistent with other `uint` data types, which also specify their size, and also because making the size of the data explicit reminds the developer and the reader how much data they've got to play with, which may help prevent or detect bugs.

For example if doing `bytes4(keccak('transfer(address, uint)’))`, you'll get a different method sig ID than `bytes4(keccak('transfer(address, uint256)’))` and smart contracts will only understand the latter when comparing method sig IDs.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use `uint256` instead `uint`.

## [NC-**] Using vulnerable dependency of solmate

#### Description

The `package.json` configuration file says that the project is using `6.2.0` of solmate which has a not last update version.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use solmate latest version.

## [NC-**] Use scientific notation rather than exponentiation

#### Description

While the compiler knows to optimize away the exponentiation, it's still better coding practice to use idioms that do not require compiler optimization, if they exist.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use scientific notation `(e.g. 1e18)` rather than exponentiation `(e.g. 10**18)`.
