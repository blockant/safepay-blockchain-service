# safepay-blockchain-service
Blockchain service for Safepay smart contract integration

Tasks List:
1. Integrate Metamask
2. Call smart contract function to lock amount in escrow contract once contractor and freelancer finalizes the cost and number of milestones. This function will receive a number of milestones, the cost of a full project, percentages of the cost paid after completion of each milestone.
This function will pay the contract amount in USDT and platform fees in ERC20  (SafePay) Token and Matic as transaction cost.
3. Once a freelancer finishes a milestone and the contractor approves the completion then after this event happens the backend calls a smart contract function to pay the freelancer for the completed milestone. This function will receive freelancer’s address, contractor address, milestone amount based on percentage and total cost.
This function will pay ERC20 (SafePay) token as platform fees and MATIC as transaction cost to receive the USDT amount of the finished milestone. This smart contract function will transfer the USDT from escrow contract to the freelancer’s address upon payment of platform fee in SafePay tokens
4. If a freelancer delays the submission then call the smart contract function to update completion time. This function will receive updated expected finish time of milestones.
5. If a freelancer doesn’t complete work or the contractor is not satisfied with submission and in case of cancellation of contract, call a smart contract function to receive the remaining locked amount of the project. Contractor will pay ERC20(safepay) token to receive the remaining locked USDT


**Required Methods**

Note: Basic validations 

**1. To Lock amount in Escrow**

```javascript
function lockAmountInEscrow(){}
```

Expected Arguments from backend

```json
{
    "milestoneCount": "<Number > 0>",
    "projectCost": "<Number > 0>",
    "projectCurrency": "<safe token / USDT>",
    "percentageToBePaid":[
        "<Array of numbers > 0 denoting percentage, order denote the milestone #>, must sum up to be 100"
    ],
    "platformFees": "< Number > 0 >",
    "platformCurrency": ""
}
```
Associated Smart Contract Method
```sol
function initializeJob()
```

**2. Complete Milestone**


```javascript
function completeMilestone(){}
```

Expected Argument from backend
```json
{
    "freelancerAddress": "",
    "contractorAddress": "",
    "mileStoneCompleted": "<Index of which Milestone is completed>"
}
```

Associated Smart Contract Method
```sol
//TBD
```

**3. Update The Completion Time in smart Contract**

```javascript
function updateCompletionTime()
```

Exptected Argument From Backend

```json
{
    "freelancerAddress": "",
    "contractorAddress": "",
    "mileStoneIndex": "<Index of which Milestone is completed>",
    "completionTime": "<Date in ISO Format>"
}
```

Associated Smart Contract Method

```sol
//TBD
```

**4. Cancel the contract**

```javascript
function cancelContract()
```

Expected Argument from backend
```json
{
    "freelancerAddress": "",
    "contractorAddress": ""
}
```
- Subsequent API Calls will be required from frontend, to fetch 
the remaining price.
- Metamask Integration Will be required to pay safepay token.

Associated Smart Contract Method
```sol
function cancelJob()
```

**5. Claim money by freelancer**

```javascript
function claimMoney(){}
```

Expected Argument from backend

```json
{
    "freelancerAddress": "",
    "contractorAddress": ""
}
```

Associated Smart Contract Method

```sol
function claimPayment(){}
```