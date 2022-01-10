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
