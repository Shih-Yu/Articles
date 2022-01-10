# Truffle Simple Storage on Cronos Testnet

In this article, we will explore how to deploy a Simple Storgage contract from Truffle to Cronos' testnet.

## About

---
Truffle is a development environment for writing smart contracts on the Ethereum blockchain. It allows developers to:

- Compile contracts

- Test contracts

- Deploy contracts

- Debug contracts

Cronos Chain is a EVM that runs parallel on to Crypto.org's blockchain
It provides many usability including:

- EVM Compatibility

- Fast and efficient scalability

- Easy to port Dapps from Etheruem and other EVM compatable chains

You can learn more about each here:

[Truffle](https://www.trufflesuite.com/docs/truffle/overview)

[Cronos Chain](https://cronos.crypto.org/)

<br>

## Project Setup

---

The first step we need to do is set up a project with Truffle before we start writing our smart contract.

- [ ] Go to the folder where you want the project to live

<br>

```sh
mkdir <project name>
```

- [ ] Then move into that folder you just created

```sh
cd <project name>
```

Now we will install Truffle into out project with the following cmmand:

```sh
truffle init
```

You should get a similar output

<details><summary>See Output</summary>

```sh
Starting init...
================

> Copying project files to /Users/Desktop/cronos-truffle-example

Init successful, sweet!

Try our scaffold commands to get started:
  $ truffle create contract YourContractName # scaffold a contract
  $ truffle create test YourTestName         # scaffold a test

http://trufflesuite.com/docs
```

</details>

<br>

Next install npm so that we can add a couple of dependencies.
Use the following command to install npm.

```sh
 npm i -y
 ```

 >You can use ```npm i```, I chose to use ```-y``` to bypass each setup step questions during the install

 Once we installed npm, we will import two dependecies we will use for our project

- [ ] [dotenv](https://www.npmjs.com/package/dotenv) to hide our private keys

- [ ] [Truffle's HDWalletProvider](https://trufflesuite.com/docs/truffle/reference/configuration.html) as a Web3 provider

Run the following command to install them both

```sh
npm i dotenv @truffle/hdwallet-provider
```

## Writing the smart contract

Inside the contracts directory, create a new file and name it ```SimpleStorage.sol```

Then put the following code into the file

```js
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.6;

contract SimpleStorage {
  string public word;

  constructor() {
    word = "Welcome!";
  }

  function setWord(string memory _word) public {
    word = _word;
  }
}

```

>We won't get into too much of the code since this tutorial is more about deploying a contract using Truffle to the Cronos Testnet. Here is information on writing smart contracts using [Solidity](https://docs.soliditylang.org/en/latest/)

Before moving on to configure the network, we will have to write a migration script.

Inside the ```migrations``` directory, add another file and name it ```2_deploy_SimpleStorage.js```

Now inside the file, write the following code:

```js
const SimpleStorage = artifacts.require("SimpleStorage");

module.exports = function (deployer) {
  deployer.deploy(SimpleStorage);
};
```

> To learn more on how migrations in Truffle works, click [Here](https://trufflesuite.com/docs/truffle/getting-started/running-migrations.html)

<br>


## Cronos Testnet Configuration

Now that we have a smart contract, we first have to configure the network before we are able to deploy it to the testnet.

Let's set up the Cronos testnet configuration by going into the ```truffle-config.js``` file

There are a lot of information about how to use this file, but we will simplfy it.

Right above the ```module.exports = {``` , we will add the following:

```js
require("dotenv").config();

const HDWalletProvider = require('@truffle/hdwallet-provider');
```

Here we are getting the ```dotenv``` package to hide our private key later on and also getting the ```HDWalletProvider``` as a Web3 provider

Next, we will setup the Cronos testnet configuration.

Inside the ```networks: {``` find the rospten network and repalce it with the following code:

```js
 cronosTestnet: {
    provider: () => new HDWalletProvider(process.env.PRIVATE_KEY, "https://cronos-testnet-3.crypto.org:8545"),
    network_id: "*",       // Cronos's testnet id
    skipDryRun: true     
    },
```

This code added the Cronos testnet address ```https://cronos-testnet-3.crypto.org:8545``` to the config file and uses the ```HDWalletProvider``` to connect to with by using a given private key from an account.

Let's simply the whole file and the code should look like the following:

```js
require("dotenv").config();

const HDWalletProvider = require('@truffle/hdwallet-provider');

module.exports = {

  networks: {
   
    cronosTestnet: {
    provider: () => new HDWalletProvider(process.env.PRIVATE_KEY, `https://cronos-testnet-3.crypto.org:8545`),
    network_id: "*",       // Cronos's testnet id
    skipDryRun: true 
    },
  },

  // Set default mocha options here, use special reporters etc.
  mocha: {
    // timeout: 100000
  },

  // Configure your compilers
  compilers: {
    solc: {
      version: "*",    // Fetch exact version from solc-bin (default: truffle's version)
    }
  },

};

```

## Setting Up Test Account

Before we can deploy our contract, we first have to connect our wallet to the testnet. In order to do so, we will configure it using Metamask. 

You can find out more about Metamask [here](https://metamask.io/)

- [ ] Log into Metamask

- [ ] Under the network menu at the top, click on the button to ```Add Network```
 
- [ ] Input the following information to add a new network:

  - Network Name: ```<Name to call Cronos Testnet>```

  - RPC Url : ```https://cronos-testnet-3.crypto.org:8545/```

  - ChainId: ```338```

  - Symbol: ```tCro```

  - Block Explorer URL: ```https://cronos.crypto.org/explorer/testnet3/```

  Once the testnet is added to Metamask, we fill fund it with some test Cronos.

  Go to the [faucet](https://cronos.crypto.org/faucet) and fund the account you will be testing with.

  Now that we have setup our test network and have tCro, the last thing we need to do before deploying our contract is to pass in our account's private key in our ```truffle-config``` file.

  In order to do this more securely, we will store the private key in a ```.env``` file.

  In the root directory of the project, type in the following command:

  ```sh
  touch .env
  ```

  This will create a file called ```.env``` in the root directoy. 

  Inside this directory, we will assign a the variable ```PRIVATE_KEY=``` our private key

  To get the private key, go to the Metamask account you are using for the test and wen you click the 3 dots next to it, select the ```Account details```

  Select the ```Export Private Key``` button. Metamask will ask for your account password and once you type that in, you should be given the private key. Now copy this key into the ```.env``` file.

  It should look similar to the following.

```js
PRIVATE_KEY=e902eef0dd0a0c03845b9b743c7834839
```
>Note that this is not a real private and is used for demonstation purpose

Since we already declared this variable in our ```truffle-config``` file in the ```HDWallet-Provder``` method, we do not have to do anything else.

<details><summary>See Output</summary>

```js
provider: () => new HDWalletProvider(process.env.PRIVATE_KEY, `https://cronos-testnet-3.crypto.org:8545`),
```
</details>

## Deploy smart contract

Now that we have:

- A smart contract

- Newtwork configuration setup

- Connected Metamask account to the testnet

- Fund the account with test tokens

We are able to deploy our contract to the testnet:

In the root directory of the project, we can run the following truffle command to deploy our contract:

```sh
truffle deploy --network cronosTestnet
```

You should get similar output in the terminal

<details><summary>See Output</summary>

```sh
Compiling your contracts...
===========================
> Everything is up to date, there is nothing to compile.



Starting migrations...
======================
> Network name:    'cronosTestnet'
> Network id:      338
> Block gas limit: 81500000 (0x4db9760)


1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > transaction hash:    0x5be6f16117df6f65b170af759df881be8afc8f6b144790cec2fe26dc2ee8eeb7
   > Blocks: 0            Seconds: 4
   > contract address:    0xAAEc9B476c0897d7A4b80Cdd61314446A402237e
   > block number:        1301726
   > block timestamp:     1641843771
   > account:             0x2880627569ffA41965536CE20B0596009eDfA744
   > balance:             98.74523
   > gas used:            250954 (0x3d44a)
   > gas price:           5000 gwei
   > value sent:          0 ETH
   > total cost:          1.25477 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:             1.25477 ETH


2_deploy_SimpleStorage.js
=========================

   Deploying 'SimpleStorage'
   -------------------------
   > transaction hash:    0x4feb1d3bd554d44a12e115646448224d36be69d8d9626f4d83e181c6bd97b50a
   > Blocks: 1            Seconds: 5
   > contract address:    0xA7fB592C7651091e7fe24969c05262Aaa3300883
   > block number:        1301730
   > block timestamp:     1641843795
   > account:             0x2880627569ffA41965536CE20B0596009eDfA744
   > balance:             96.97724
   > gas used:            308985 (0x4b6f9)
   > gas price:           5000 gwei
   > value sent:          0 ETH
   > total cost:          1.544925 ETH


   ⠋ Saving migration to chain.
```

</details>

You should also notice that the amount of your test tokens has reduced.

Finally, you can check that the contract has been deployed to Cronos' testnet by getting the contracts address that was created in the output of the terminal when it was deployed and paste it into Cronos' testnet block explorer [Here]( https://cronos.crypto.org/explorer/testnet3/)