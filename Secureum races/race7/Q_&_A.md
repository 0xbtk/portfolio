[Q1] The mint price of an InSecureumApe is
(A): 0.0008 ETH
(B): 0.008 ETH
(C): 0.08 ETH
(D): 0.8 ETH

[Q2] The security concern(s) with InSecureumApe access control is/are
(A): Owner can arbitrarily pause public minting of InSecureumApes
(B): Owner can arbitrarily mint InSecureumApes
(C): Single-step ownership change
(D): Missing event emits in and time-delayed effects of owner functions

[Q3] The security concern(s) with InSecureumApe constructor is/are
(A): Missing sanity/threshold check on maxNftSupply
(B): Missing sanity/threshold check on saleStart
(C): Potential integer overflow
(D): None of the above

[Q4] The total number of InSecureumApes that can ever be minted is
(A): maxApePurchase
(B): MAX_APES
(C): MAX_APES + 30
(D): type(uint256).max

[Q5] The public minting of InSecureumApes
(A): Must be paid the exact amount in Ether
(B): May be performed 19 NFTs at a time
(C): Uses _safeMint to prevent locked/stuck NFTs
(D): None of the above

[Q6] The security concern(s) with InSecureumApe is/are
(A): Use of a floating pragma and an older compiler version
(B): Oracle price manipulation
(C): Reentrancy allowing bypass of maxApePurchase check
(D): None of the above

[Q7] The starting index determination
(A): Is meant to randomize NFT reveal post-mint
(B): Can be triggered by the owner at any time
(C): May be triggered only 9 days after sale start
(D): Accounts for the fact that EVM only stores previous 256 block hashes

[Q8] Potential gas optimization(s) in InSecureumApe is/are
(A): Caching of storage variables
(B): Avoiding initializations of variables to default values of their types
(C): Use of immutables
(D): None of the above

Secureum answers:
-----------------

| Number | Answers       |
|--------|---------------|
| [A1]   | D             |
| [A2]   | A, B, C, D    |
| [A3]   | A, B, C       |
| [A4]   | D             |
| [A5]   | B, C          |
| [A6]   | A, C          |
| [A7]   | A, B, D       |
| [A8]   | A, B, C       |

My answers:
-----------

| Number | Answers       | Wrong Answers |
|--------|---------------|---------------|
| [A1]   | D             |               |
| [A2]   | A, B, C, D    |               |
| [A3]   | A, B, C       |               |
| [A4]   | D             |               |
| [A5]   | B, C          |               |
| [A6]   | A, C          |               |
| [A7]   | D             | Missed A, B   |
| [A8]   | A, B, C       |               |