# Project Setup Using Hardhat & Truffle - part 4

Now that we have a smart contract, let's deploy it to the blockchain

### Deployment on Truffle

- [ ] In the terminal make sure we are in the ```truffle-example``` directory

```sh
cd truffle-example
```

 Before we can deploy our contract, we first have to add a new file under the migrations directory

- [ ] Create a new file under the migrations directory and prefix the name of the file with ```2_```

  ```2_NumberChanger.js```

- [ ]Inside ```2_NumberChanger.js``` we will write the follwoing script

```js 
const NumberChanger = artifacts.require("NumberChnager");

module.exports = function (deployer) {
  deployer.deploy(NumberChanger);
};
```
We defined a variable called NumberChanger, but this can be any name you wish. Inside the variable, we call the ```artifacts.require``` method and pass in the name of our contract to interact with(not the name of the file), which in this case is also called ```"NumberChanger"```

Afterwards, we export the function that would deploy the contract

> To learn more about how migrations work, go here [Truffle Migration]("https://trufflesuite.com/docs/truffle/getting-started/running-migrations#migration-files")

Now that we are setup, lets deploy our contract

- [ ] In th
