#### [Q1] The security concern(s) with InSecureumLand is/are

- (A): Single-step ownership change
- (B): Incorrectly implemented KYC check using Merkle proofs
- (C): Missing time-delayed change of critical parameters
- (D): Accidentally sent Ether gets locked in contract

#### [Q2] The security concern(s) with InSecureumLand setOperator() is/are

- (A): Missing zero-address validation
- (B): Missing event emission
- (C): Incorrect modifier
- (D): None of the above

#### [Q3] The security concern(s) with InSecureumLand mintLands() is/are

- (A): Minting could exceed max supply
- (B): Minting could exceed maxMintPerTx
- (C): Minting could exceed maxMintPerAddress
- (D): None of the above

#### [Q4] Missing threshold check(s) on parameter(s) is/are a concern in

- (A): mintLands
- (B): startPublicSale
- (C): contributorsClaimLand
- (D): None of the above

#### [Q5] The security concern(s) with InSecureumLand contributors claim functions is/are

- (A): Anyone can call startContributorsClaimPeriod
- (B): Anyone can call stopContributorsClaimPeriod
- (C): Anyone can call contributorsClaimLand
- (D): None of the above

#### [Q6] The security concern(s) with InSecureumLand random number usage is/are

- (A): It depends on miner-influenceable block.timestamp
- (B): It depends on miner-influenceable blockhash
- (C): It depends on deprecated Chainlink VRF v1
- (D): None of the above

#### [Q7] The documentation/readability concern(s) with InSecureumLand is/are

- (A): Stale comments
- (B): Missing NatSpec
- (C): Minimal inlined comments
- (D): None of the above

[Q8] Potential gas optimization(s) (after appropriate security considerations) in InSecureumLand is/are

- (A): Removing nonReentrant modifier if mint addresses are known to be EOA
- (B): Using _mint instead of _safeMint if mint addresses are known to be EOA
- (C): Using unchecked in for loop increments
- (D): None of the above

Secureum answers:
-----------------

| Number | Answers       |
|--------|---------------|
| [A1]   | A, C          |
| [A2]   | A, B          |
| [A3]   | A             |
| [A4]   | B, C          |
| [A5]   | C             |
| [A6]   | C             |
| [A7]   | B, C          |
| [A8]   | A, B, C       |

My answers:
-----------

| Number | Answers       | Wrong Answers      |
|--------|---------------|--------------------|
| [A1]   | A, C          |                    |
| [A2]   | A, B, C       | No C               |
| [A3]   | A             |                    |
| [A4]   | B             | Missed C           |
| [A5]   | C             |                    |
| [A6]   | A, B          | No A, B / Missed C |
| [A7]   | B, C          |                    |
| [A8]   | A, B, C       |                    |
