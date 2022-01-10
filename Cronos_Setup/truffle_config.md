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