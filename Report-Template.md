## Title of this finding

## Overview

Brief description of the finding.

## Impact

Detailed description of the impact of this finding.

## Proof of Concept

#### Vulnerability Details

Provide direct links to all referenced code in GitHub. Add screenshots, logs, or any other relevant proof that illustrates the concept.

#### Here is a coded PoC to demonstrate the issue:

```solidity
    function testMax() public {
        uint256 max = a.max(5, 10);
        console.log("Max is =", max);
    }
```

#### Logs result: 

```yaml
Max is : 10
```

#### Test Setup:

- Incorporate the tests in [**`Contract link`**](link)
- Execute: **`forge test --mc contract-name --mt test-name -vvv`**

## Tools Used

Manual review

## Recommended Mitigation Steps

Your suggested fix for the finding.
