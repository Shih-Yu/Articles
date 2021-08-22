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
This is referring to where we are planning to have our contract deployed to and interact with.

>In this example, we will use a local blockchain for our deployment since we will be provided with accounts, private keys and already be funded

* Local - running a version of a blockchain on our computer

>When using a testnet option, a wallet will have to be created and you will have get fake ethers for testing from a faucet of the chosen testnet.
[Metamask](https://metamask.io/) is one option for a wallet and fairly easy to use

* Testnet - a simulation of the Ethereum mainnet where you use fake ethers to pay for contract interactions and gas fees below is a list of testnest:

  * [Ropsten](https://faucet.ropsten.be/)

  * [Kovan](https://github.com/kovan-testnet)

  * [Rinkey](https://faucet.rinkeby.io/)

  * [Goerli](https://goerli.net/)

>The real thing and uses real ether for interaction

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

>More can information on Truffle config can be found [Here](https://hardhat.org/config/)

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

Now that Ganache is configure, let's run it by going to our terminal

>This should be running when interacting with the smart contract

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

Open ```hardhat.config.js``` file and under ```module.exports``` go to ```solidity:``` and set it to version ```0.8.6``` for this example

>Hardhat already has it set to ```0.8.4```

```sh
/**
 * @type import('hardhat/config').HardhatUserConfig
 */
module.exports = {
  solidity: "0.8.6",
};
```

The next step is to set up our networks.

Since there's no format provided, we will set it up like this

>More can information on Hardhat config can be found [Here](https://hardhat.org/config/)

```sh
/**
 * @type import('hardhat/config').HardhatUserConfig
 */
module.exports = {
  networks: {
    hardhat: {
      chainId: 1337
    },
 },
  solidity: "0.8.6",
};
 
```

Now that Hardhat is configured, let's run it by going to our terminal

>This should be running when interacting with the smart contract

```sh
npx hardhat node
```

<details> <summary>See output</summary>

```sh

Started HTTP and WebSocket JSON-RPC server at http://127.0.0.1:8545/

Accounts
========
Account #0: 0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266 (10000 ETH)
Private Key: 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80

Account #1: 0x70997970c51812dc3a010c7d01b50e0d17dc79c8 (10000 ETH)
Private Key: 0x59c6995e998f97a5a0044966f0945389dc9e86dae88c7a8412f4603b6b78690d

Account #2: 0x3c44cdddb6a900fa2b585dd299e03d12fa4293bc (10000 ETH)
Private Key: 0x5de4111afa1a4b94908f83103eb1f1706367c2e68ca870fc3fb9a804cdab365a

Account #3: 0x90f79bf6eb2c4f870365e785982e1f101e93b906 (10000 ETH)
Private Key: 0x7c852118294e51e653712a81e05800f419141751be58f605c371e15141b007a6

Account #4: 0x15d34aaf54267db7d7c367839aaf71a00a2c6a65 (10000 ETH)
Private Key: 0x47e179ec197488593b187f80a00eb0da91f1b9d0b13f8733639f19c30a34926a

Account #5: 0x9965507d1a55bcc2695c58ba16fb37d819b0a4dc (10000 ETH)
Private Key: 0x8b3a350cf5c34c9194ca85829a2df0ec3153be0318b5e2d3348e872092edffba

Account #6: 0x976ea74026e726554db657fa54763abd0c3a0aa9 (10000 ETH)
Private Key: 0x92db14e403b83dfe3df233f83dfa3a0d7096f21ca9b0d6d6b8d88b2b4ec1564e

Account #7: 0x14dc79964da2c08b23698b3d3cc7ca32193d9955 (10000 ETH)
Private Key: 0x4bbbf85ce3377467afe5d46f804f221813b2bb87f24d81f60f1fcdbf7cbf4356

Account #8: 0x23618e81e3f5cdf7f54c3d65f7fbc0abf5b21e8f (10000 ETH)
Private Key: 0xdbda1821b80551c9d65939329250298aa3472ba22feea921c0cf5d620ea67b97

Account #9: 0xa0ee7a142d267c1f36714e4a8f75612f20a79720 (10000 ETH)
Private Key: 0x2a871d0798f97d79848a013d4936a73bf4cc922c825d33c1cf7073dff6d409c6

Account #10: 0xbcd4042de499d14e55001ccbb24a551f3b954096 (10000 ETH)
Private Key: 0xf214f2b2cd398c806f84e317254e0f0b801d0643303237d97a22a48e01628897

Account #11: 0x71be63f3384f5fb98995898a86b02fb2426c5788 (10000 ETH)
Private Key: 0x701b615bbdfb9de65240bc28bd21bbc0d996645a3dd57e7b12bc2bdf6f192c82

Account #12: 0xfabb0ac9d68b0b445fb7357272ff202c5651694a (10000 ETH)
Private Key: 0xa267530f49f8280200edf313ee7af6b827f2a8bce2897751d06a843f644967b1

Account #13: 0x1cbd3b2770909d4e10f157cabc84c7264073c9ec (10000 ETH)
Private Key: 0x47c99abed3324a2707c28affff1267e45918ec8c3f20b8aa892e8b065d2942dd

Account #14: 0xdf3e18d64bc6a983f673ab319ccae4f1a57c7097 (10000 ETH)
Private Key: 0xc526ee95bf44d8fc405a158bb884d9d1238d99f0612e9f33d006bb0789009aaa

Account #15: 0xcd3b766ccdd6ae721141f452c550ca635964ce71 (10000 ETH)
Private Key: 0x8166f546bab6da521a8369cab06c5d2b9e46670292d85c875ee9ec20e84ffb61

Account #16: 0x2546bcd3c84621e976d8185a91a922ae77ecec30 (10000 ETH)
Private Key: 0xea6c44ac03bff858b476bba40716402b03e41b8e97e276d1baec7c37d42484a0

Account #17: 0xbda5747bfd65f08deb54cb465eb87d40e51b197e (10000 ETH)
Private Key: 0x689af8efa8c651a91ad287602527f3af2fe9f6501a7ac4b061667b5a93e037fd

Account #18: 0xdd2fd4581271e230360230f9337d5c0430bf44c0 (10000 ETH)
Private Key: 0xde9be858da4a475276426320d5e9262ecfc3ba460bfac56360bfa6c4c28b4ee0

Account #19: 0x8626f6940e2eb28930efb4cef49b2d1f2c9c1199 (10000 ETH)
Private Key: 0xdf57089febbacf7ba0bc227dafbffa9fc08a93fdc68e1e42411a14efcf23656e
```

</details>

Now we have a blockchain on our computer that has 20 accounts prefunded with 1000 ethers and their private keys

In part 3 we will write a simple smart contract