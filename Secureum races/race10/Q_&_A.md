[Q1] Which statements are true in Test1()?
(A): The function does not use all supplied extra data
(B): The function can revert due to an underflow
(C): The function can revert due to an overflow
(D): The function accesses memory which it should not

A, B, C

[Q2] Which statements are true in Test2()?
(A): Result of encodePacked is deterministic
(B): abi.decode always succeeds
(C): It calls function Test1() without any problem
(D): It should use uint256 instead of uint

B, C

[Q3] Which statements are true in NextBookNonce()?
(A): wrap and unwrap cost additional gas
(B): It is safe to use unchecked
(C): There is  something suspicious about  the increment value
(D): It could have used x.nonce++

C

[Q4] Which statements are true in Test3()?
A: bookIndex.nonce is incremented in the loop
B: bookIndex.nonce cannot be incremented because NextBookNonce is pure
C: i++ can be made unchecked
D: memory can be changed to storage without any other changes

A, C

[Q5] Which statements are true In Test4()?
(A): The function always reverts with ZeroAddress()
(B): The function always reverts with ZeroAmount()
(C): The function never reverts with ZeroAddress()
(D): The function never reverts with ZeroAmount()

C, D

[Q6] Which statements are true in Test5()?
(A): modifier checkInvariants will pause the contract if too much is minted
(B): modifier checkInvariants will never pause the contract
(C): modifier checkInvariants will always pause the contract
(D): There are more efficient ways to handle the require

B, D

[Q7] Which statements are true about the owner?
(A): The owner is initialized
(B): The owner is not initialized
(C): The owner cannot be changed
(D): The owner can be changed

B, D

[Q8] Which statements are true In Test5() and related functions?
(A): pause is unsafe
(B): unpause is unsafe
(C): The emit is done right
(D): The emit is done wrong

A, D

Secureum answers:
-----------------

| Number | Answers       |
|--------|---------------|
| [A1]   | A, B, C       |
| [A2]   | A, C          |
| [A3]   | B, C          |
| [A4]   | A, C          |
| [A5]   | C, D          |
| [A6]   | B, D          |
| [A7]   | A, D          |
| [A8]   | A, D          |

My answers:
-----------

| Number | Answers       | Wrong Answers |
|--------|---------------|---------------|
| [A1]   |               |               |
| [A2]   |               |               |
| [A3]   |               |               |
| [A4]   |               |               |
| [A5]   |               |               |
| [A6]   |               |               |
| [A7]   |               |               |
| [A8]   |               |               |