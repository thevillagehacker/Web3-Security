## ****If Else | Solidity 0.8****

[Solidity by Example](https://solidity-by-example.org/if-else/)

## ****For and While Loops | Solidity 0.8****

[Solidity by Example](https://solidity-by-example.org/loop/)

## ****Error | Solidity 0.8****

### Custom Error in Contract to save gas used for transaction

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract Error {
    function testRequire(uint _i) public pure {
        // Require should be used to validate conditions such as:
        // - inputs
        // - conditions before execution
        // - return values from calls to other functions
        require(_i > 10, "Input must be greater than 10");
    }

    function testRevert(uint _i) public pure {
        // Revert is useful when the condition to check is complex.
        // This code does the exact same thing as the example above
        if (_i <= 10) {
            revert("Input must be greater than 10");
        }
    }

    uint public num;

    function testAssert() public view {
        // Assert should only be used to test for internal errors,
        // and to check invariants.

        // Here we assert that num is always equal to 0
        // since it is impossible to update the value of num
        assert(num == 0);
    }

    // custom error
    error InsufficientBalance(uint balance, uint withdrawAmount);

    function testCustomError(uint _withdrawAmount) public view {
        uint bal = address(this).balance;
        if (bal < _withdrawAmount) {
            revert InsufficientBalance({balance: bal, withdrawAmount: _withdrawAmount});
        }
    }
}
```

### Transaction code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract Account {
    uint public balance;
    uint public constant MAX_UINT = 2 ** 256 - 1;

    function deposit(uint _amount) public {
        uint oldBalance = balance;
        uint newBalance = balance + _amount;

        // balance + _amount does not overflow if balance + _amount >= balance
        require(newBalance >= oldBalance, "Overflow");

        balance = newBalance;

        assert(balance >= oldBalance);
    }

    function withdraw(uint _amount) public {
        uint oldBalance = balance;

        // balance - _amount does not underflow if balance >= _amount
        require(balance >= _amount, "Underflow");

        if (balance < _amount) {
            revert("Underflow");
        }

        balance -= _amount;

        assert(balance <= oldBalance);
    }
}
```

## ****Function Modifier | Solidity 0.8****

Modifiers are code that can be run before and / or after a function call.

Modifiers can be used to:

- Restrict access
- Validate inputs
- Guard against reentrancy hack

[Solidity by Example](https://solidity-by-example.org/function-modifier/)

## ****Constructor | Solidity 0.8****

A `constructor` is an optional function that is executed upon contract creation.

Here are examples of how to pass arguments to `constructors`.

[Solidity by Example](https://solidity-by-example.org/constructor/)

## Events ****| Solidity 0.8****

`Events` allow logging to the Ethereum blockchain. Some use cases for events are:

- Listening for events and updating user interface
- A cheap form of storage

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract Event {
    // Event declaration
    // Up to 3 parameters can be indexed.
    // Indexed parameters helps you filter the logs by the indexed parameter
    event Log(address indexed sender, string message);
    event AnotherLog();

    function test() public {
        emit Log(msg.sender, "Hello World!");
        emit Log(msg.sender, "Hello EVM!");
        emit AnotherLog();
    }
}
```

[Solidity by Example](https://solidity-by-example.org/events/)

## ****Ownable | Solidity 0.8****

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract ownable {
    address public owner;

    constructor() {
        owner=msg.sender;
    }
    modifier onlyowner {
        require(msg.sender == owner,  "not owner");
        _;
    }
    function setowner(address _newowner) external onlyowner{
        require(_newowner != address(0), "invalid address");
        owner = _newowner;
    }

    function onlyownercancall () public onlyowner {
        
        
    }
    function anyonecancall (uint x, uint y) public pure returns (uint) {
        return x + y;
    }
}
```

## ****Function Outputs | Solidity 0.8****

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract func_out {
    function returMany() public pure returns (uint ,bool) {
        return (1, true);
    }
    function named() public pure returns (uint x, bool b) {
        return (1, true);
    }
    function assigned() public pure returns (uint x, bool b){
        x = 12;
        b = false;
        x += 1;
    }
}
```

[Solidity by Example](https://solidity-by-example.org/function/)

## ****Array | Solidity 0.8****

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract Array{
    uint [] public nums = [1, 2, 3];
    uint [5] public numsFixed = [1, 2, 3, 4, 5];

    function example() external{
        nums.push(4); // [1, 2, 3, 4]
        uint x = nums[1];
        nums[2] = 333; // [1, 2, 333, 4]
        delete nums[1]; //delete the value from the array [1, 0, 333, 4]
        nums.pop(); // [1, 0, 333] removed the last element from the array
        uint len = nums.length;

        // create in memory
        uint[] memory a = new uint[](5); // 5 is size of the array
        // fixed sixe array cannot be removed or pushed
        a[1] = 123;
    }
    // function to return the array from the memory
    function returnMenory() external view returns (uint [] memory){
        return nums;
    }

}
```

## ****Array Remove An Element By Shifting | Solidity 0.8****

[Solidity by Example](https://solidity-by-example.org/array/)
