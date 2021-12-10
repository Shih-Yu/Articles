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

- [ ] In the





### Deployment on Hardhat

- [ ] In the terminal make sure we are in the ```hardhat-example``` directory

```sh
cd hardhat-example
```

 Before we can deploy our contract, we first have to add some code for hardhat to deploy our contract

- [ ] Go to the scripts folder and rename the file ```sample-script.js``` to ``deploy.js```

- [ ] Next, under the line:

 ```js
 console.log("Greeter deployed to:", greeter.address);
 ```

Type the following code:

```js
const NumberChanger = await hre.ethers.getContractFactory("NumberChanger");
  const numberChanger = await NumberChanger.deploy();

  await numberChanger.deployed();
  console.log("Number deployed to:", numberChanger.address);

```

What this code does is create a new variable that will take the NumberChanger contract and deploy it. Once the contract is deployed, it will log out in the terminal the address of the deployed NumberChanger contract.

> In Hardhat, you can put all the contracts to be compiled and deployed in the same file, which is located in the scripts folder.

The code should look like the following with the default Greeter contract provided by Hardhat.

```js

const hre = require("hardhat");

async function main() {
 
  const Greeter = await hre.ethers.getContractFactory("Greeter");
  const greeter = await Greeter.deploy("Hello, Hardhat!");

  await greeter.deployed();

  console.log("Greeter deployed to:", greeter.address);

  const NumberChanger = await hre.ethers.getContractFactory("NumberChanger");
  const numberChanger = await NumberChanger.deploy();

  await numberChanger.deployed();
  console.log("Number deployed to:", numberChanger.address);
}


main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```

- [ ] Run the follwoing in the terminal

```sh
npx hardhat compile
```

<details> <summary>See output</summary>

```sh
Compiling 3 files with 0.8.0
Compilation finished successfully
```

</details>

Once compiled, there should be a folder created called ```artifacts```

This is where your contracts ABI is so that the front end can interact with it and the byte code is create for the EVM

Now that we have compiled our contracts, we can deploy it. For this example, we will deploy it to the localnet provided by Hardhat

>To specify the nextworkt to deploy to, use the following command in the terminal ```npx hardhat run scripts/deploy.js --network <network name>```

- [ ] Run the following command in the terminal:

```js
npx hardhat run scripts/deploy.js
```

<details> <summary>See output</summary>

```sh
Deploying a Greeter with greeting: Hello, Hardhat!
Greeter deployed to: 0x5FbDB2315678afecb367f032d93F642f64180aa3
Number deployed to: 0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512
```

</details>

Now we are given the address to our contracts.

One last thing is to move the artifacts folder. By default, it will be created in the root directory, but since we will be interacting with in from the front end with React, it should be located in the ```src``` folder.

In the hardhat-config.js file, place the following code under the where the version of the solidity compiler version is declared.

```js
 paths: {
    artifacts: './src/artifacts',
  },
```

The code should look like the following:

```js
module.exports = {
  networks: {
    hardhat: {
      chainId: 1337
    },
 },
  solidity: "0.8.0",
  paths: {
    artifacts: './src/artifacts',
  },
};
```

Now that we set the path, delete the artifacts folder in the root directory and redeploy it with ```npx hardhat run scripts/deploy.js``` and it should show up in the ```src``` folder.

In part 5, we will build a simple front end in react and interact with our contract.