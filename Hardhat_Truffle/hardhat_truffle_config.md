# React Project Setup Using Hardhat & Truffle - part 2

Now that we have our project set up, we will have to do some configurations before we start writing our contract

## Configuration Setup

---

Each project should now have a configuation file in the root directory
for Truffle it should be named ```truffle-config.js```

For Hardhat it should be named ```hardhat.config.js```

Let's configure our complier version for Solidity as well as the network we will be deploying our contract to

## Networks

---
This is referring to how we are planning to have our contract deployed to and interact with.

>In this example, we will use a localhost for our deployment.

* Localhost - running a small version of a blockchain on our computer

* Testnet - a simulation of the Ethereum mainnet where you use fake ethers to pay for contract interactions and gas fees below is a list of testnest:

  * [Ropsten](https://faucet.ropsten.be/)

  * [Kovan](https://github.com/kovan-testnet)

  * [Rinkey](https://faucet.rinkeby.io/)

  * [Goerli](https://goerli.net/)

* Mainnet - the Ethereum blockchain

<br>

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

The next step is to set up our networks. 

 Truffle provides two ways to create a local blockchain on our computer using [Ganache](https://www.trufflesuite.com/ganache)

* [Ganache CLI](https://github.com/trufflesuite/ganache-cli-archive)

* [Ganache GUI](https://www.trufflesuite.com/ganache)

We will go the route of using [Ganache CLI](https://github.com/trufflesuite/ganache-cli-archive) but feel free to try out [Ganache GUI](https://www.trufflesuite.com/ganache) as well

Install [Ganache CLI](https://github.com/trufflesuite/ganache-cli-archive) locally in the project

```sh
npm i ganache-cli
```

or globally on your computer

```sh
npm i -g ganache-cli
```

Once the installation is complete, we will set it up in our truffle-config.js by uncommentting the development object, host, port and network_id

```js
 networks: {
    // Useful for testing. The `development` name is special - truffle uses it by default
    // if it's defined here and no other network is specified at the command line.
    // You should run a client (like ganache-cli, geth or parity) in a separate terminal
    // tab if you use this network and you must also set the `host`, `port` and `network_id`
    // options below to some value.
    //
     development: {
     host: "127.0.0.1",     // Localhost (default: none)
      port: 8545,            // Standard Ethereum port (default: none)
      network_id: "*",       // Any network (default: none)
    // },
    
  },
```

Now that Ganache is configure, let's running it by going to our terminal

```sh
ganache-cli
```

<details> <summary>See output</summary>

```sh
Ganache CLI v6.12.2 (ganache-core: 2.13.2)

Available Accounts
==================
(0) 0x969bA70Cfe0C4F008420Fe8f3692a0E38F1651C7 (100 ETH)
(1) 0xcF284112963B78a15b7e4EbCcc4D0C375c7b7220 (100 ETH)
(2) 0x0aFb5969722AE021327B0bBA1BA9587aa990D7Ba (100 ETH)
(3) 0xF20419183d1b0de9cb95157A5fB7963625C85C7a (100 ETH)
(4) 0x8978E1f007f2Bb3C3baFB128575bD0706814E92E (100 ETH)
(5) 0xac5e8CD2A98a817b7D98870F3Bf1C879Eb3d3412 (100 ETH)
(6) 0xd684A1491adf5ad35d41e01b075e9c686d4af646 (100 ETH)
(7) 0x173eDC61f16734e6a62c02ACE582fD482074Daa3 (100 ETH)
(8) 0x8bA9684605E43f43CBcf7E834D8C0ab0AcF6CEcF (100 ETH)
(9) 0x926555b830c813C295137F461A972Ffe585dFBCC (100 ETH)

Private Keys
==================
(0) 0xc9822f6c7e9381cd8d22f2c6511368cf52039f7639e8000f9dc5d644e1fc470a
(1) 0xfa7161d4edd38f2e3f06f328333cda93de7cf39b23e736203152a945eb890c5b
(2) 0x3a923aaf69c4a2df7d4864e5a095d81a599732bb8a581ffe29bc0eac1b1e927e
(3) 0x1d9260184f297d12dcb20478c8f2606b87a7c21f6d4701df8dac381d878b6083
(4) 0xb48aa648f5a61c0980a1d14732cfe607d35906fa7b557d547d54839d60da2052
(5) 0x6cb1a078df151e83fc5d223dbf3a4276e977b2a6a6bd1664e3b750ed25fe0cd8
(6) 0xcd7d45a3dc279a2cde51aae947eb1c825a03ecbc2586d9ee148d1f6f8bd7be92
(7) 0x725b39ecf104da56d9038d7760bbf6bb5463f53197a1603cb74344cdc9129597
(8) 0x51f7bfaf19b66435dc24bd83c765779d403c94f0073eb484b35cf50b97b90810
(9) 0xfda751b7fda95c79f258f8a464dc5a2db1521a8e32f04b27f7735e521bfd3664

HD Wallet
==================
Mnemonic:      history element nuclear valve good west century obscure indoor during crime genius
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

Now we have a blockchain on our computer that has 10 accounts prefunded with 100 ethers and their private keys, along with the Mnemonic seed phrase

<br>

### Hardhat config

---

First we will set up our Solidity compiler to the version that we will be using in our smart contracts

Open ```hardhat.config.js``` file and under the compiler object go to ```solc:``` and set it to version ```0.8.6``` for this example