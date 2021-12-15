# Project Setup Using Hardhat & Truffle - part 4

Now that we have a smart contract, let's deploy it to the blockchain


## Deployment on Truffle

- [ ] In the terminal make sure we are in the ```truffle-example``` directory

```sh
cd truffle-example
```

 Before we can deploy our contract, we first have to add a new file under the migrations directory

- [ ] Create a new file under the migrations directory and prefix the name of the file with ```2_```

  ```2_NumberChanger.js```

- [ ]Inside ```2_NumberChanger.js``` we will write the following script

```js 
const NumberChanger = artifacts.require("NumberChanger");

module.exports = function (deployer) {
  deployer.deploy(NumberChanger);
};
```

We defined a variable called NumberChanger, but this can be any name you wish. Inside the variable, we call the ```artifacts.require``` method and pass in the name of our contract to interact with(not the name of the file), which in this case is also called ```"NumberChanger"```

Afterwards, we export the function that would deploy the contract

> To learn more about how migrations work, go here [Truffle Migration]("https://trufflesuite.com/docs/truffle/getting-started/running-migrations#migration-files")


Now that we are setup, lets deploy our contract

- [ ] Run the following in the terminal

```sh
truffle compile
```

<br>

<details> <summary>See output</summary>

```sh
Compiling your contracts...
===========================
✔ Fetching solc version list from solc-bin. Attempt #1
> Compiling ./contracts/Migrations.sol
> Compiling ./contracts/NumberChanger.sol
> Artifacts written to /Users/Desktop/Examples/truffle-example/build/contracts
> Compiled successfully using:
   - solc: 0.8.10+commit.fc410830.Emscripten.clang
```

</details>

Once compiled, there should be a folder created called ```build```

This is where your contracts ABI is so that the front end can interact with it and the byte code is create for the EVM

Now that we have compiled our contracts, we can deploy it. For this example, we will deploy it to the localnet, Ganache.

- [ ] First in the terminal, run the following command

```sh
ganache-cli
```

You should now see the following:

<details> <summary>See output</summary>

```sh
Ganache CLI v6.12.2 (ganache-core: 2.13.2)

Available Accounts
==================
(0) 0x735d731D1B90eBFD8B35E550e7430282c98133eC (100 ETH)
(1) 0x59dc305ac3564D0aF51b770311F182890023ed73 (100 ETH)
(2) 0xb8a3fAC0eeD31dFF5E5A641a3278DC34afbFb35C (100 ETH)
(3) 0xC703D178A5F529186F035bf83E7EC4155951e537 (100 ETH)
(4) 0x8951B99e2fA2e5E721552d2091Ac922A140581A7 (100 ETH)
(5) 0x32919628CFCE86CcA027C09FabAe15643Ef6DEd2 (100 ETH)
(6) 0x3ae65932Ee15a270B8876845b5Cf6D23A4ee801E (100 ETH)
(7) 0xC429c4836504aF3Aa4b687163c9be108Fa3d35E4 (100 ETH)
(8) 0x7a9026b25Ceb30A0934384b354a53690c889FCfd (100 ETH)
(9) 0xd8F267534a42B91B8469127695c200E571a8c2F4 (100 ETH)

Private Keys
==================
(0) 0x7ab485a29412a9d4f466778d2d1de37c19fc1c10217e5bc10153af185541c445
(1) 0xc9fc3d2e11d0701dc52820187ad830f0f0b7cfc77365a8e1b8df7f38a3df2d90
(2) 0x09a2d80b06649bafe479d7f6610e41df6b5e77420aaa0d45cef9bb09016def90
(3) 0x54e49af326e58a98b831acf00ce8799f2cd23f470b382c5b184397b23450f18d
(4) 0x952d1e27ef8289a5988c89ea9096c694e2f376356972d73388fe3a48fd201b56
(5) 0x96ff3b0f11c396e4eb696b325fff8aeca0899bae5285c15a2096e503583edf68
(6) 0xd9b0ef3b02245d05588295836040df476c0298d1f33291e55556a874cabbccf3
(7) 0x4b2899ed136d6bff17f352a2aa6c2eb162ba183861dfb28487540c473b91f992
(8) 0x75fa379cd3b1e925849587af471e7000fe36d63496720147c8ceb13ca70d2872
(9) 0x907a9ee73f5fa3d3a79565106236f57687dc710c6e7a3bed97256ea494bb0b32

HD Wallet
==================
Mnemonic:      just always youth crew song dust frost virtual program amused scene cash
Base HD Path:  m/44'/60'/0'/0/{account_index}

Gas Price
==================
20000000000

Gas Limit
==================
6721975

Call Gas Limit
==================
9007199254740991
```

</details>

<br>
Now that we have our local blockchain running, we can now deploy our contract

- [ ] Running the following code in the terminal:

```sh
  truffle migrate
```

>```truffle migrate``` is similar to ```truffle deploy``` You can find out more information on this topic here [Truffle Migration]("https://trufflesuite.com/docs/truffle/getting-started/running-migrations#migration-files")

<details> <summary>See output</summary>

```sh
Compiling your contracts...
===========================
✔ Fetching solc version list from solc-bin. Attempt #1
> Compiling ./contracts/Migrations.sol
> Compiling ./contracts/NumberChanger.sol
> Artifacts written to /Users/Desktop/Examples/truffle-example/build/contracts
> Compiled successfully using:
   - solc: 0.8.10+commit.fc410830.Emscripten.clang



Starting migrations...
======================
> Network name:    'development'
> Network id:      1639592180037
> Block gas limit: 6721975 (0x6691b7)


1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > transaction hash:    0x41f9ad193605295c1424325c13c6f36e41ddfebd9836605542e8ff47af33e929
   > Blocks: 0            Seconds: 0
   > contract address:    0x01Dd5F52EC31A26C51D4EB42f0A448d863F342e0
   > block number:        21
   > block timestamp:     1639598127
   > account:             0x735d731D1B90eBFD8B35E550e7430282c98133eC
   > balance:             99.95056962
   > gas used:            248854 (0x3cc16)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.00497708 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00497708 ETH


2_NumberChanger.js
==================

   Deploying 'NumberChanger'
   -------------------------
   > transaction hash:    0x8aa0925fd1df6669566f89c4751e44b8fb905ca07618392e216f3223609dda9e
   > Blocks: 0            Seconds: 0
   > contract address:    0x2CdfF21817CEe737eBeB8fAd13af0f0964A1D907
   > block number:        23
   > block timestamp:     1639598127
   > account:             0x735d731D1B90eBFD8B35E550e7430282c98133eC
   > balance:             99.9472063
   > gas used:            125653 (0x1ead5)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.00251306 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00251306 ETH


Summary
=======
> Total deployments:   2
> Final cost:          0.00749014 ETH

```

</details>

<br>

>You can see that ```truffle migrate``` compiles the contract and the deploys it. You can just use ```truffle migrate``` to compile and deploy your contract with one command

The contract is now deployed, can you can see the contact addresses

One last thing is to move the ```build``` folder. By default, it will be created in the root directory, but since we will be interacting with in from the front end with React, it should be located in the ```src``` folder.

In the truffle-config.js file,
add the following code before ```module.exports```

```sh
const path = require("path")
```
place the following code under the ```module.exports```

```sh
   contracts_build_directory: path.join(__dirname, "src/build"),
```

The result should look like the following:

```js
const path = require("path");


module.exports = {
  contracts_build_directory: path.join(__dirname, "src/build"),
  networks: {
    development: {
      host: "127.0.0.1",
      port: 8545,
      network_id: "*", 
    },
  },
  compilers: {
    solc: {
      version: "pragma",
    },
  },
};
```

Now when we redeploy our contract, the build folder should be created inside the ```src``` folder

<br>

## Deployment on Hardhat

- [ ] In the terminal make sure we are in the ```hardhat-example``` directory

```sh
cd hardhat-example
```

 Before we can deploy our contract, we first have to add some code for hardhat to deploy our contract

- [ ] Go to the scripts folder and rename the file ```sample-script.js``` to ```deploy.js```

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

- [ ] Run the following in the terminal

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

>To specify the network to deploy to, use the following command in the terminal ```npx hardhat run scripts/deploy.js --network <network name>```

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