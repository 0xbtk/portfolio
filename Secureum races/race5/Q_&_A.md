[Q1] InSecureum balanceOf()
(A): May be optimised by caching state variable in local variable
(B): May be optimised by changing state mutability from view to pure
(C): May be optimised by changing its visibility to external
(D): None of the above

Answer[D]

[Q2] In InSecureum, array lengths mismatch check is missing in
(A): balanceOfBatch()
(B): _safeBatchTransferFrom()
(C): _mintBatch()
(D): _burnBatch()

Answer[A, B, C, D]

[Q3] The security concern(s) with InSecureum _safeTransferFrom() is/are
(A): Incorrect visibility
(B): Susceptibility to an integer underflow
(C): Missing zero-address validation
(D): None of the above

Answer[A, B, C]

[Q4] The security concern(s) with InSecureum _safeBatchTransferFrom() is/are
(A): Missing array lengths mismatch check
(B): Susceptibility to an integer underflow
(C): Incorrect balance update
(D): None of the above

Answer[A, C]

[Q5] The security concern(s) with InSecureum _mintBatch() is/are
(A): Missing array lengths mismatch check
(B): Incorrect event emission
(C): Allows burning of tokens
(D): None of the above

Answer[A, C]

[Q6] The security concern(s) with InSecureum _burn() is/are
(A): Missing zero-address validation
(B): Susceptibility to an integer underflow
(C): Incorrect balance update
(D): None of the above

Answer[D]

[Q7] The security concern(s) with InSecureum _doSafeTransferAcceptanceCheck() is/are
(A): isContract check on incorrect address
(B): Incorrect check on return value
(C): Call to incorrect isContract implementation
(D): None of the above

Answer[B, C]

[Q8] The security concern(s) with InSecureum isContract() implementation is/are
(A): Incorrect visibility
(B): Incorrect operator in the comparison
(C): Unnecessary because Ethereum only has Contract accounts
(D): None of the above

Answer[B]

Secureum answers:
-----------------

| Number | Answers       |
|--------|---------------|
| [A1]   | D             |
| [A2]   | A, B, C, D    |
| [A3]   | A, B, C       |
| [A4]   | A, C          |
| [A5]   | A, B, C       |
| [A6]   | D             |
| [A7]   | B, C          |
| [A8]   | B             |

My answers:
-----------

| Number | Answers       | Wrong Answers |
|--------|---------------|---------------|
| [A1]   | D             |               |
| [A2]   | A, B, C, D    |               |
| [A3]   | A, B, C       |               |
| [A4]   | A, C          |               |
| [A5]   | A, C          | Missed B      |
| [A6]   | D             |               |
| [A7]   | B, C          |               |
| [A8]   | B             |               |