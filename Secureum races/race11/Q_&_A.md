#### [Q1] Which statements are true in withdraw()?

- (A) Can be successfully executed when contract is paused
- (B) User can withdraw only after _minDepositLockTime elapsed since last withdrawal
- (C) Follows checks-effects-interaction pattern best practice
- (D) User can withdraw more than deposited

#### [Q2] Which mitigations are applicable to withdraw()?

- (A): Transferred amount should be minimum of amount and _userBalances[msg.sender]
- (B): Move if/else block before safeTransferFrom
- (C): Require amount to be <= user’s balance deposited earlier
- (D): Remove if/else block and add _userBalances[msg.sender] -= amount before safeTransferFrom

#### [Q3] The security concern(s) in pause() is/are:

- (A): Does not emit an event
- (B): Access control is not strict enough
- (C): Will always revert
- (D): None of the above

#### [Q4] Which statement(s) is/are true for unpause()?

- (A): Will unpause deposits and withdrawals
- (B): Will unpause withdrawals only
- (C): Anyone can successfully call the function
- (D): None of the above

#### [Q5] Which statement(s) is/are true in depositFor()?

- (A): Can be executed when contract is paused
- (B): Allows a user to deposit for another user
- (C): Allows a user to fund the deposit for another user
- (D): None of the above

#### [Q6] The issue(s) in depositFor() is/are:

- (A): Cannot be paused for emergency
- (B): Exploitable re-entrancy attack
- (C): User withdrawals can be delayed indefinitely via DoS attack
- (D): None of the above

#### [Q7] Which of the following statement(s) is/are true?

- (A): Withdraw event is emitted with incorrect amount
- (B): Withdraw event is emitted with correct user
- (C): Deposit event is always emitted incorrectly
- (D): Deposit event is emitted with incorrect user

#### [Q8] Potential gas optimization(s) is/are:

- (A): Use immutable for all variables assigned in constructor
- (B): Use immutable for _token, _operator and _minDepositLockTime
- (C): Use unchecked
- (D): None of the above

Secureum answers:
-----------------

| Number | Answers       |
|--------|---------------|
| [A1]   | D             |
| [A2]   | A, C, D       |
| [A3]   | A             |
| [A4]   | B, C          |
| [A5]   | A, B          |
| [A6]   | A, C          |
| [A7]   | B, D          |
| [A8]   | B, C          |

My answers:
-----------

| Number | Answers       | Wrong Answers |
|--------|---------------|---------------|
| [A1]   | D             |               |
| [A2]   | A, C, D       |               |
| [A3]   | A             |               |
| [A4]   | B, C          |               |
| [A5]   | A, B          |               |
| [A6]   | A, C          |               |
| [A7]   | B, D          |               |
| [A8]   | B, C          |               |
