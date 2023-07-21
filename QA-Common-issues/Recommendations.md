| Total Recommendations |
|-----------------------|

| Risk    | Issues Details                                                                                          | Number        |
|---------|---------------------------------------------------------------------------------------------------------|---------------|
| [R-**]  | Missing checks for `address(0)`                                                                         |               |
| [R-**]  | Contracts should have full test coverage                                                                |               |
| [R-**]  | Value is not validated to be different than the existing one                                            |               |
| [R-**]  | Add a timelock to critical functions                                                                    |               |
| [R-**]  | Need Fuzzing test                                                                                       |               |
| [R-**]  | Consider using `delete` rather than assigning zero to clear values                                      |               |
| [R-**]  | Events that mark critical parameter changes should contain both the old and the new value               |               |
| [R-**]  | Use SMTChecker                                                                                          |               |

## [R-**] Missing checks for `address(0)`

#### Description

Check of the address for the critical changes to protect the code from address(0) problem in case of mistakes.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Add address(0) check

## [R-**] Contracts should have full test coverage

#### Description

While 100% code coverage does not guarantee that there are no bugs, it often will catch easy-to-find bugs, and will ensure that there are fewer regressions when the code invariably has to be modified. Furthermore, in order to get full coverage, code authors will often have to re-organize their code so that it is more modular, so that each component can be tested separately, which reduces interdependencies between modules and layers, and makes for code that is easier to reason about and audit.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Line coverage percentage should be 100%.

## [R-**] Value is not validated to be different than the existing one

#### Description

While the value is validated to be in the constant bounds, it is not validated to be different than the existing one. Queueing the same value will cause multiple abnormal events to be emitted, will ultimately result in a no-op situation.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Add a `require()` statement to check that the new value is different than the current one.

## [R-**] Add a timelock to critical functions

#### Description

It is a good practice to give time for users to react and adjust to critical changes. A timelock provides more guarantees and reduces the level of trust required, thus decreasing risk for users. It also indicates that the project is legitimate.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Consider adding a timelock to the critical changes.

## [R-**] Need Fuzzing test

#### Description

In total * contracts, more than ** `unchecked{}` are used, the functions used are critical. For this reason, there must be fuzzing tests in the tests of the project. Not seen in tests.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use should fuzzing test like Echidna. As Alberto Cuesta Canada said: Fuzzing is not easy, the tools are rough, and the math is hard, but it is worth it. Fuzzing gives me a level of confidence in my smart contracts that I didn’t have before. Relying just on unit testing anymore and poking around in a testnet seems reckless now.

Ref: https://medium.com/coinmonks/smart-contract-fuzzing-d9b88e0b0a05

## [R-**] Use SMTChecker

#### Description

The highest tier of smart contract behavior assurance is formal mathematical verification. All assertions that are made are guaranteed to be true across all inputs → The quality of your asserts is the quality of your verification.

> Ref: https://twitter.com/0xOwenThurm/status/1614359896350425088?t=dbG9gHFigBX85Rv29lOjIQ&s=19   

## [R-**] Events that mark critical parameter changes should contain both the old and the new value

#### Description

Events that mark critical parameter changes should contain both the old and the new value.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Add the old value to the event.

## [R-**] Consider using `delete` rather than assigning zero to clear values    

#### Description

The `delete` keyword more closely matches the semantics of what is being done, and draws more attention to the changing of state, which may lead to a more thorough audit of its associated logic.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Use the `delete` keyword.
