# React Project Setup Using Hardhat & Truffle - part 2

Now that we have our project set up, we will have to do some configurations before we start writing our contract

## Configuration Setup

---

Each project should now have a configuation file in the root directory
for Truffle it should be named ```truffle-config.js```

For Hardhat it should be named ```hardhat.config.js```

Let's configure our complier version for Solidity as well as the network we will be deploying our contract to

### Truffle config

---

First we will set up our Solidity compiler to the version that we will be using in our smart contracts

Open ```truffle-config.js``` file and under the compiler object go to ```solc:``` and set it to version ```0.8.6``` for this example

>You have the option to leave the other parameters commented out or they can be deleted since this example will not utilize them. It is left commented out to match as close to the example you might see.

```js
compilers: {
    solc: {
       version: "0.8.6",    // Fetch exact version from solc-bin (default: truffle's version)
      // docker: true,        // Use "0.5.1" you've installed locally with docker (default: false)
      // settings: {          // See the solidity docs for advice about optimization and evmVersion
      //  optimizer: {
      //    enabled: false,
      //    runs: 200
      //  },
      //  evmVersion: "byzantium"
      // }
    }
```

The next step is to set up our networks. This is referring to how we are planning to have our contract deployed to and interact with.

* Localhost - running a small version of a blockchain on our computer

* Testnet - a simulation of the Ethereum mainnet where you use fake ethers to pay for contract interactions and gas fees below is a list of testnest:

  * [Ropsten](https://faucet.ropsten.be/)

  * [Kovan](https://github.com/kovan-testnet)

  * [Rinkey](https://faucet.rinkeby.io/)

  * [Goerli](https://goerli.net/)

* Mainnet - the Ethereum blockchain

In this example, we will use a localhost for our deployment. Truffle provides two ways to create a local blockchain on our computer using [Ganache](https://www.trufflesuite.com/ganache)

* [Ganache CLI](https://github.com/trufflesuite/ganache-cli-archive)

* [Ganache GUI](https://www.trufflesuite.com/ganache)

We will go the route of using [Ganache CLI](https://github.com/trufflesuite/ganache-cli-archive) but feel free to try out [Ganache GUI](https://www.trufflesuite.com/ganache) as well

### Hardhat config

---