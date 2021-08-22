# Project Setup Using Hardhat & Truffle - part 3

Now we will write a simple smart contract and deploy it to our local blockchain

## Writing the smart contract

---

For both Truffle and Hardhat, we can create a new file inside the contract folder

>Solidiyt is the lauguage that will be used for our example. More information about it can be found [HERE](https://docs.soliditylang.org/en/v0.8.7/)

- [ ] Name it ``` NumberChanger.sol```

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
contract NumberChanger {

}
```

- [ ] Declare a state variable called number

```js
contract NumberChanger {
  uint256 number;
}
```
