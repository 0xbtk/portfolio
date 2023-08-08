## [Escher Overview](https://code4rena.com/contests/2022-12-escher-contest#top)

| Protocol | Website     | Twitter     | Contest Pot | Length | Time spent |
|----------|-------------|-------------|-------------|--------|--------|
| Escher   | [404]() | [404](L) | 36,500 USDC | 3 days | < 3 Hours |

### About Escher

Escher is a decentralized curated marketplace for editioned artwork.

### Findings Summary

| Risk   | Title                                                                             |
|--------|-----------------------------------------------------------------------------------|
| [M-01] | call() should be used instead of transfer() M-2 Use safeMint instead of mint for ERC721       |

## [M-01] call() should be used instead of transfer() M-2 Use safeMint instead of mint for ERC721

## Impact

If `saleReceiver` and `feeReceiver` where smart contracts and one of the scenarios described in the POC occurred, neither of them will be able to withdraw their funds, and they (funds) will be frozen in the contract, resulting in a loss of funds for both users and the protocol.

## Proof of Concept

The use of the deprecated `transfer()` function for a payable address will certainly make the transaction fail when:

1. The claimer smart contract does not implement a payable fallback function.
2. The claimer smart contract does implement a payable fallback which uses more than 2300 gas unit.
3. The claimer smart contract implements a payable fallback function that needs less than 2300 gas units but is called through proxy, raising the call's gas usage above 2300.
4. Some multisig wallets might also require higher gas than 2300.

> A more detailed explanation can be found [here](https://consensys.io/diligence/blog/2019/09/stop-using-soliditys-transfer-now/).

## Tools Used

Manual Review

## Recommended Mitigation Steps

Consider using .call() instead with the CEI pattern implemented correctly. .

```solidity
        (bool success, ) = payable(msg.sender).call{value: owed}("");
        require(success, "Call failed");
```

```solidity
        (bool success, ) = ISaleFactory(factory).feeReceiver().call{value: address(this).balance / 20}("");
        require(success, "Call failed");  
```
