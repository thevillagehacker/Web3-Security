# Basic Concepts of Solidity
## Hello World | Solidity 0.8
```sol
// SPDX-License-Identifier: MIT
// compiler version must be greater than or equal to 0.8.17 and less than 0.9.0
pragma solidity ^0.8.17;

contract HelloWorld {
    string public greet = "Hello World!";
}
```

## Value Types | Solidity 0.8
- Data types -> Values and references
  - Value - means data stores a value
  - references - means do not store value instead it will store reference that where it actually stored
  
```sol
// SPDX-License-Identifier: MIT
// compiler version must be greater than or equal to 0.8.17 and less than 0.9.0
pragma solidity ^0.8.17;

contract HelloWorld {
    bool public b = true;
    uint public u = 123;
    int public i = -123;

    // find out the min and max value for int
    int public minInt = type(int).min;
    int public maxInt = type(int).max;
    address public addr = 0xdafea492d9c6733ae3d56b7ed1adb60692c98bc5 // random address copied from etherscan
    byte 32 public b32 = 0xb5f06d28dc5da96e28139109c2922da59a26aa2f993f48cb71876bce20dda49b // byte 32 used for cryptographic hash functions
    
}
```
[Solidity by Example](https://solidity-by-example.org/primitives/)

## Introduction to Functions | Solidity 0.8
```sol
// SPDX-License-Identifier: MIT
// compiler version must be greater than or equal to 0.8.17 and less than 0.9.0
pragma solidity ^0.8.17;

contract example {
    function add(uint x, uint y) external pure returns (uint) {
        return x + y;
    }
    function sub(uint x, uint y) external pure returns (uint) {
        return x - y;
    }
}
```
[Solidity by Example](https://solidity-by-example.org/function/)

## State Variables | Solidity 0.8

3 types of variables in solidity
- local
- state
- global
### State Variable example
```sol
// SPDX-License-Identifier: MIT
// compiler version must be greater than or equal to 0.8.17 and less than 0.9.0
pragma solidity ^0.8.17;

contract statevariable {
    uint public myuint = 123; // will be stored on the blockchain
    function foo() external {
        uint notstate = 456; // variable will only stored inside this function

    }

}
```
[Solidity by Example](https://solidity-by-example.org/variables/)

### Local Variables | Solidity 0.8
```sol
// SPDX-License-Identifier: MIT
// compiler version must be greater than or equal to 0.8.17 and less than 0.9.0
pragma solidity ^0.8.17;

contract localvariable {
    uint public i;
    bool public b;
    address public addr;
    function foo() external{
        uint x = 123;
        bool f = true;
        // more code
        x += 234;
        f = false;
        // above local variables only exist while the function is running

        // below code update values to the state variable
        i = 123;
        b = true;
        addr = address(1);
    }
}
```
[Solidity by Example](https://solidity-by-example.org/variables/)

### Global Variables | Solidity 0.8
- Global variables store data such as blockchain transactions

```sol
// SPDX-License-Identifier: MIT
// compiler version must be greater than or equal to 0.8.17 and less than 0.9.0
pragma solidity ^0.8.17;

contract Globalvariable {
    function globalVars() external view returns (address, uint, uint) { // view is same as pure but it can read data from state and global varialbles
        address sender = msg.sender;
        uint timestamp = block.timestamp;
        uint blocknum = block.number;
        return (sender,timestamp,blocknum);
    }
}
```
## View and Pure Functions | Solidity 0.8
```sol
// SPDX-License-Identifier: MIT
// compiler version must be greater than or equal to 0.8.17 and less than 0.9.0
pragma solidity ^0.8.17;

contract viewandpure {
    uint public number;
    fundtion viewFun() external view returns (uint) {
        return number; // view is reading data from state variable in the blockchain
    }
    function pureFun() external pure returns (uint) {
        return 1; // only return the readonly data in the blockchain
    }
    function addtonumber(uint x) external view returns (uint) {
        return number + x; // read data from state variable
    }
    function add(uint x, uint y) externals pure returns (uint) {
        return x + y; // reads data inside the function
    }
}
```
## Counter | Solidity 0.8 Application
```sol
// SPDX-License-Identifier: MIT
// compiler version must be greater than or equal to 0.8.17 and less than 0.9.0
pragma solidity ^0.8.17;

contract counter {
    uint public count;
    function inc() external {
        count += 1;
    }
    function dec() external {
        count -= 1;
    }
}
// the functions are not view or pure because in the function the state variable values are changing
```
## Default Values | Solidity 0.8
```sol
// SPDX-License-Identifier: MIT
// compiler version must be greater than or equal to 0.8.17 and less than 0.9.0
pragma solidity ^0.8.17;

contract counter {
    bool public b; //false
    uint public u; //0
    int public i; //0
    address public addr; //0x000000000000000000000000000000000000000
    bytes32 public b32; //0x0000000000000000000000000000000000000000000000000000000000000000
    function inc() external { // change the state variable value
        addr = address(1);
    }
}
```

## Constants | Solidity 0.8
```sol
// SPDX-License-Identifier: MIT
// compiler version must be greater than or equal to 0.8.17 and less than 0.9.0
pragma solidity ^0.8.17;
// 21420 gas used
contract Constants {
    address public constant ADDR = 0x12AE66CDc592e10B60f9097a7b0D3C59fce29876;
    uint public constant INT = 123;
    
}
// 23553 used
contract Var {
    address public ADDR = 0x8ba1f109551bD432803012645Ac136ddd64DBA72;

}
```
[Solidity by Example](https://solidity-by-example.org/constants/)
