# Project Setup Using Hardhat & Truffle - part 3

Now we will write a simple smart contract and deploy it to our local blockchain

## Writing the smart contract

---

>We can ignore the existing contract for now but feel free to explore them

For both Truffle and Hardhat, we can create a new file inside the contract folder

>Solidity is the lauguage that will be used for our example. More information about it can be found [HERE](https://docs.soliditylang.org/en/v0.8.7/)

- [ ] Name it ```NumberChanger.sol```

- [ ] Declare the SPDX-License with it being commented out

``` js
// SPDX-License-Identifier: MIT
```

- [ ] Define the version of Solidity the contract will be complied in, we will set it to the version to be the same as in our config file

>This allows it to be compiled with version 0.8.6 or higher

```js
pragma solidity ^0.8.6;
```

- [ ] Write our contract by first declaring it and giving it the same name as our file name

```js
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.6;

contract NumberChanger {

}
```

- [ ] Declare a state variable called number

```js
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.6;

contract NumberChanger {
  uint256 number;
}
```

- [ ] Create a function that allows to retrieve the number stored in the state variable

```js
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.6;

contract NumberChanger {
  uint256 number

  function getNumber() public views returns(uint256) {
    return number;
  }
}
```

- [ ] Create a function that updates the number in state variable

```js
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.6;

contract NumberChanger {
  uint256 number

  function getNumber() public views returns(uint256) {
    return number;
  }

  function setNumber(uint256 _number) public {
    number = _number
  }
}
```

Now we written a smart contract that allows the number to be stored and updated on the blockchain

## Hardhat

---

Hardhat allows the option to console log in Solidity, in order to do so

- [ ] Import hardhat/console.sol after the version of Solidity has been declared

```js
import "hardhat/console.sol";
```

```js
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.6;

import "hardhat/console.sol";
```

- [ ] Add it to where you would like to see an output

```js
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.6;

import "hardhat/console.sol";

contract NumberChanger {
  uint256 number

  function getNumber() public view returns(uint256) {
    return number;
  }

  function setNumber(uint256 _number) public {
    number = _number
    console.log(number)
  }
}
```

> The import of ``` hardhat/console.sol ``` and ```console.log``` is optional only if you are using Hardhat

The finished contract should look like this

```js
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.6;

contract NumberChanger {
  uint256 number

  function getNumber() public view returns(uint256) {
    return number;
  }

  function setNumber(uint256 _number) public {
    number = _number
  }
}
```

In part 4 we will deploy our contract to the local blockchain