[Q1] Which of the following is/are true?
(A): NFT ownership is tracked by _ownerOf
(B): NFT balance is tracked by _balanceOf
(C): NFT approvals are tracked by getApproved
(D): NFT operator can transfer all of owner’s NFTs

ABC

[Q2] InSecureumERC721 recognizes the following role(s)
(A): Owner
(B): Spender (Approved address)
(C): Operator
(D): None of the above

ABC

[Q3] The security concern(s) addressed explicitly in _mint include
(A): Prevent minting to zero address
(B): Prevent reminting of NFTs
(C): Transparency by emitting event
(D): None of the above

ABC

[Q4] The security concerns in _burn include
(A): Anyone can arbitrarily burn NFTs
(B): Potential integer underflow because of unchecked
(C): Incorrect emission of event
(D): None of the above

AB

[Q5] The security concern(s) addressed explicitly in _safeMint include
(A): Validating if the recipient is an EOA
(B): Ensuring that the recipient can only be an EOA
(C): Validating if the recipient is an ERC721 aware contract
(D): None of the above

AC

[Q6] Function approve
(A): Allows the NFT owner to approve a spender
(B): Allows the NFT spender to approve an operator
(C): Allows the NFT operator to approve a spender
(D): None of the above

AC

[Q7] Function setApprovalForAll
(A): Approves msg.sender to manage operator’s NFTs
(B): Gives everyone approval to manage msg.sender’s NFTs
(C): Revokes everyone’s approvals to manage msg.sender’s NFTs
(D): None of the above

D

[Q8] The security concern(s) in transferFrom include
(A): Allowing the msg.sender to transfer any NFT
(B): NFTs potentially stuck in recipient contracts
(C): Potential integer underflow
(D): None of the above

BC

Secureum answers:
-----------------

| Number | Answers       |
|--------|---------------|
| [A1]   | A, B, C, D    |
| [A2]   | A, B, C       |
| [A3]   | A, B, C       |
| [A4]   | A             |
| [A5]   | A, C          |
| [A6]   | A, C          |
| [A7]   | D             |
| [A8]   | A, B, C       |

My answers:
-----------

| Number | Answers       | Wrong Answers |
|--------|---------------|---------------|
| [A1]   | A, B, C       | Missed D      |
| [A2]   | A, B, C       |               |
| [A3]   | A, B, C       |               |
| [A4]   | A, B          | No B          |
| [A5]   | A, C          |               |
| [A6]   | A, C          |               |
| [A7]   | D             |               |
| [A8]   | B, C          | Missed A      |