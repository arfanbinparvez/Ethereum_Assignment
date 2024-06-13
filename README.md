
# MyToken Smart Contract

`MyToken`

## Contract Details

### Public Variables

- `name`: The name of the token.
- `symbol`: The symbol/abbreviation of the token.
- `totalSupply`: The total supply of tokens in circulation.

### Mapping

- `balances`: A mapping from addresses to their respective balances (`address => uint256`).

### Functions

#### `mint(address _to, uint _value)`

- Increases the total supply of tokens by `_value`.
- Increases the balance of the `_to` address by `_value`.

```solidity
function mint(address _to, uint _value) public;
```

**Example:**

```solidity
myToken.mint(0xRecipientAddress, 100);
```

#### `burn(address _from, uint256 _value)`

- Checks if the balance of `_from` is greater than or equal to `_value`.
- If the balance is sufficient, it decreases the total supply of tokens by `_value`.
- Decreases the balance of the `_from` address by `_value`.

```solidity
function burn(address _from, uint256 _value) public;
```

**Example:**

```solidity
myToken.burn(0xSenderAddress, 50);
```



## Complete Contract Code


```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.18;

contract MyToken {

    // Public variables
    string public name;
    string public symbol;
    uint public totalSupply;

    // Mapping from addresses to balances
    mapping(address => uint256) public balances;

    // Constructor to initialize the token details
    constructor(string memory _name, string memory _symbol, uint _initialSupply) {
        name = _name;
        symbol = _symbol;
        totalSupply = _initialSupply;
        // Initially assign all tokens to the contract's deployer
        balances[msg.sender] = _initialSupply;
    }

    // Mint function to create new tokens
    function mint(address _to, uint _value) public {
        totalSupply += _value;
        balances[_to] += _value;
    }

    // Burn function to destroy tokens
    function burn(address _from, uint256 _value) public {
        if (balances[_from] >= _value) {
            totalSupply -= _value;
            balances[_from] -= _value;
        } else {
            // Handle the case where balance is insufficient
            revert("Insufficient balance to burn");
        }
    }
}
```

---
