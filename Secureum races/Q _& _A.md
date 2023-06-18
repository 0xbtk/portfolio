[Q1] InSecureum implements
(A): Atypical decimals value
(B): Non-standard decreaseAllowance and increaseAllowance
(C): Non-standard transfer
(D): None of the above

[Q2] In InSecureum
(A): decimals() can have pure state mutability instead of view
(B): _burn() can have external visibility instead of internal
(C): _mint() should have internal visibility instead of external
(D): None of the above

[Q3] InSecureum transferFrom()
(A): Is susceptible to an integer underflow
(B): Has an incorrect allowance check
(C): Has an optimisation indicative of unlimited approvals
(D): None of the above

[Q4] In InSecureum
(A): increaseAllowance is susceptible to an integer overflow
(B): decreaseAllowance is susceptible to an integer overflow
(C): decreaseAllowance does not allow reducing allowance to zero
(D): decreaseAllowance can be optimised with unchecked{}

[Q5] InSecureum _transfer()
(A): Is missing a zero-address validation
(B): Is susceptible to an integer overflow
(C): Is susceptible to an integer underflow
(D): None of the above

[Q6] InSecureum _mint()
(A): Is missing a zero-address validation
(B): Has an incorrect event emission
(C): Has an incorrect update of account balance
(D): None of the above

[Q7] InSecureum _burn()
(A): Is missing a zero-address validation
(B): Has an incorrect event emission
(C): Has an incorrect update of account balance
(D): None of the above

[Q8] InSecureum _approve()
(A): Is missing a zero-address validation
(B): Has incorrect error messages
(C): Has an incorrect update of allowance
(D): None of the above

Secureum answers:
-----------------

| Number | Answers       |
|--------|---------------|
| [A1]   | A, B          |
| [A2]   | A, C          |
| [A3]   | A, B, C       |
| [A4]   | C, D          |
| [A5]   | D             |
| [A6]   | A, C          |
| [A7]   | B             |
| [A8]   | B, C          |

My answers:
-----------

| Number | Answers       | Wrong Answers |
|--------|---------------|---------------|
| [A1]   | A, B          |               |
| [A2]   | A, B, C       | No B          |
| [A3]   | A, C          | Missed B      |
| [A4]   | C, D          |               |
| [A5]   | D             |               |
| [A6]   | A, C          |               |
| [A7]   | B             |               |
| [A8]   | B             | Missed C      |
