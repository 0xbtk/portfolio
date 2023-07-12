#### [Q1] The function signature is the first 4 bytes of the keccak hash which

- (A): Includes the function name
- (B): Includes a comma separated list of parameter types
- (C): Includes a comma separated list of return value types
- (D): Is generated only for public and external functions

#### [Q2] The Proxy contract is most similar to a

- (A): UUPS Proxy
- (B): Beacon Proxy
- (C): Transparent Proxy
- (D): Metamorphic Proxy

#### [Q3] Gas will be saved with the following changes

- (A): Skipping initialization of counter variable
- (B): Making increase() function external to avoid copying from calldata to memory
- (C): Packing multiple implementation addresses into the same storage slot
- (D): Moving the calculation of the counter() function's signature hash to a constant

#### [Q4] Calling the increase() function on the Proxy contract

- (A): Will revert since the Proxy contract has no increase() function
- (B): Will revert for any other caller than the one that deployed the Proxy
- (C): Increases the integer value in the Proxy's storage slot located at index 1
- (D): Delegate-calls to the zero-address

####[Q5] Calling the decrease() function on the Proxy contract

- (A): Will revert because it was not correctly registered on the proxy
- (B): Will succeed and return the value of counter after it was decreased
- (C): Will succeed and return the value of counter before it was decreased
- (D): Will succeed and return nothing

####[Q6] Due to a storage clash between the Proxy and the Mastercopy contracts

- (A): Proxy's implementations would be overwritten by 0 during initialization of the Mastercopy
- (B): Proxy's implementations would be overwritten when the counter variable changes
- (C): Proxy's implementations variable's storage slot being overwritten causes a DoS
- (D): None of the above

#### [Q7] The Proxy contract

- (A): Won't be able to receive any ether when calldatasize is 0 due to a missing receive()
- (B): Will be the owner of the Mastercopy contract
- (C): Has a storage clash in slot 0 which will cause issues with the current Mastercopy
- (D): None of the above

#### [Q8] The fallback() function's assembly block

- (A): Can be marked as "memory-safe" for gas optimizations
- (B): Has the result of the delegate-call overwrite the the call parameters in memory
- (C): Interferes with the Slot-Hash calculation for the implementations-mapping by overwriting the scratch space
- (D): None of the above

Secureum answers:
-----------------

| Number | Answers       |
|--------|---------------|
| [A1]   | A, B, D       |
| [A2]   | C             |
| [A3]   | A             |
| [A4]   | B, C          |
| [A5]   | D             |
| [A6]   | D             |
| [A7]   | B             |
| [A8]   | B             |

My answers:
-----------

| Number | Answers       | Wrong Answers |
|--------|---------------|---------------|
| [A1]   | A, B, D       |               |
| [A2]   | C             |               |
| [A3]   | A             |               |
| [A4]   | B, C          |               |
| [A5]   | A             | No A, Just D  |
| [A6]   | D             |               |
| [A7]   | B             |               |
| [A8]   | A, B          | No A          |
