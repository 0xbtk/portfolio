## [Stakehouse Overview](https://code4rena.com/contests/2022-11-lsd-network-stakehouse-contest#top)

| Protocol   | Website     | Twitter     | Contest Pot | Length |
|------------|-------------|-------------|-------------|--------|
| Stakehouse | [Website]() | [Twitter]() | 90,500 USDC | 7 days |

### About Stakehouse

Surge is a hyperstructure lending protocol that allows anyone to deployer their own lending pool. It utilizes a novel mechanism called Algorithmic Collateral Ratios in order to eliminate the need for price oracles in DeFi lending.

### Findings Summary

| Risk   | Title                                                         |
|--------|---------------------------------------------------------------|
| [H-01] | Reentrancy attack may occur on withdraw ETH For Knot function |

## [H-01] Reentrancy attack may occur on withdraw ETH For Knot function

#### Impact
A reentrancy attack can occur when the contract fails to update its state before the interaction, the attacker can make a recursive call back to the original function in an attempt to drain funds.

#### Proof of Concept
Provide direct links to all referenced code in GitHub. Add screenshots, logs, or any other relevant proof that illustrates the concept.

#### Tools Used

#### Recommended Mitigation Steps
