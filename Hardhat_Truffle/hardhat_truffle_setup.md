# React Project Setup Using Hardhat & Truffle - part 1

We will explore Truffle and Hardhat side by side to translate their commands and how to adapt from one to the other by creating a small project in React.

## About

---
Truffle and Hardhat are both a development enviroment for writing smart contracts on the Ethereum blockchain. These tools allows developers to:

- Compile contracts

- Test contracts

- Deploy contracts

- Debug contracts

You can learn more about each here:

[Truffle](https://www.trufflesuite.com/docs/truffle/overview)

[Hardhat](https://www.trufflesuite.com/docs/truffle/overview)

## Project Setup

---

The first step we need to do is set up a project with React before we start writing our smart contracts.

- [ ] Go to the folder where you want the project to live

<br>

### Truffle Setup Method

---

```sh
npx create-react-app <project name>
```

<details> <summary>See output</summary>

```sh
npx create-react-app truffle-example

Creating a new React app in /Examples/truffle-example.

Installing packages. This might take a couple of minutes.
Installing react, react-dom, and react-scripts with cra-template...



Created git commit.

Success! Created truffle-example at /Examples/truffle-example
Inside that directory, you can run several commands:

  yarn start
    Starts the development server.

  yarn build
    Bundles the app into static files for production.

  yarn test
    Starts the test runner.

  yarn eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd truffle-example
  yarn start

Happy hacking!
```

</details>

- [ ] Then move into that folder you just created

```sh
cd <project name>
```

> Another option is using Truffle boxes, there is one created with React that you can use. To learn more about Truffle boxes, go here [Truffle Boxes]("https://www.trufflesuite.com/boxes")

> If you don't have truffle installed globally

```sh
npx truffle unbox react
```

>If you have truffle installed globally

```sh
truffle unbox react
```

<details> <summary>See output</summary>

```sh
truffle unbox react

Starting unbox...
=================

✔ Preparing to download box
✔ Downloading
✔ Cleaning up temporary files
✔ Setting up box

Unbox successful, sweet!

Commands:

  Compile:              truffle compile
  Migrate:              truffle migrate
  Test contracts:       truffle test
  Test dapp:            cd client && npm test
  Run dev server:       cd client && npm run start
  Build for production: cd client && npm run build
```

</details>

<br>

### Hardhat Setup Method

---
Since hardhat is a lighter tool that utilizes more on plugins, there is only a need for it to be installed as a dependency in your project

```sh
npx create-react-app <project name>
```

<details> <summary>See output</summary>

```sh
npx create-react-app hardhat-example

Creating a new React app in /Examples/hardhat-example.

Installing packages. This might take a couple of minutes.
Installing react, react-dom, and react-scripts with cra-template...



Created git commit.

Success! Created hardhat-example at /Examples/hardhat-example
Inside that directory, you can run several commands:

  yarn start
    Starts the development server.

  yarn build
    Bundles the app into static files for production.

  yarn test
    Starts the test runner.

  yarn eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd hardhat-example
  yarn start

Happy hacking!
```

</details>

- [ ] Then move into that folder you just created

```sh
cd <project name>
```

## Installation

---
Now that the folders are setup, let's install the development tools

<br>

### Truffle Installation Method

---

In the project folder you just created, install truffle

>This is only if you  didn't use truffle unbox! If you use ```truffle unbox``` you can skip this step

```sh
truffle init
```

<details> <summary>See output</summary>

```sh
truffle init

Starting init...
================

> Copying project files to /Examples/truffle-example

Init successful, sweet!
```

</details>

### Hardhat Installation Method

---
Go into the project folder and install hardhat as a dependency for the project

```sh
npm i hardhat
```

Now install hardhat

```sh
npx hardhat
```
<details> <summary>See output</summary>

```sh
npx hardhat
888    888                      888 888               888
888    888                      888 888               888
888    888                      888 888               888
8888888888  8888b.  888d888 .d88888 88888b.   8888b.  888888
888    888     "88b 888P"  d88" 888 888 "88b     "88b 888
888    888 .d888888 888    888  888 888  888 .d888888 888
888    888 888  888 888    Y88b 888 888  888 888  888 Y88b.
888    888 "Y888888 888     "Y88888 888  888 "Y888888  "Y888

👷 Welcome to Hardhat v2.6.1 👷‍

? What do you want to do? …
❯ Create a basic sample project
  Create an advanced sample project
  Create an empty hardhat.config.js
  Quit
```

</details>

Select

```sh
 Create a basic sample project
 ```

 Then set your project root directory

```sh
✔ What do you want to do? · Create a basic sample project
? Hardhat project root: › /Examples/hardhat-example
```

Since react already has a .gitingnore file, select no

```sh
? Do you want to add a .gitignore? (Y/n) › n
```
Since hardhat relies on other dependencies, we will need to install them, however for the purpose of keeping the comparision as close as possible, we will install them ourselves

>Hardhat usually use ethers.js but since truffle uses web3.js, we will use web3.js with hardhat as well

```sh
? Do you want to install this sample project dependencies with yarn (@nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers ethers)? (Y/n) › n
```

You might see some warnings during this installation but it should be fine for now just as long as you get a project created confirmation

```sh
✨  Done in 47.89s.

✨ Project created ✨
See the README.txt file for some example tasks you can run.
```

## Installing Dependencies

For this section, we will only install dependencies for hardhat since that is it's nature and truffle already comes with everything you need

### Hardhat Installing Depenedencies

We will need web3.js to interact with the blockchain in our project later on

>This lets hardhat intercact with web3.js library

```sh
npm i @nomiclabs/hardhat-web3
```

>This installs web3.js library in our project

```sh
npm i web3
```

 We have nowseen how to completely set up and install a React project with both Truffle and Hardhat

Next we will configure both the development enviroment and start writing a contract!
