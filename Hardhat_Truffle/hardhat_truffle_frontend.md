# Project Setup Using Hardhat & Truffle - part 5

For the final part of this project, we are going to connect our contract to the front end with React. Since this is about writing smart contracts, we won't go too much in to styling the page.

## Frontend setup with Truffle

### Checklist

Here is a quick check list before connect to the frontend

- [ ] Ganache is still running
- [ ] Our contract is compiled and the ```build``` directory is under our ```src``` directory
- [ ] In another terminal, change into ```scr``` directory of this project

```sh
cd truffle-example/src
```

- [ ] Run ```npm start``` to make sure React is working and you should get something similar
to the following:

```sh
Compiled successfully!

You can now view truffle-example in the browser.

  Local:            http://localhost:3000
  On Your Network:  http://192.168.5.107:3000

Note that the development build is not optimized.
To create a production build, use yarn build.
```

Now that everything is set up, lets connect the frontend to our contract

Under the ```scr```, find the file ```App.js```, the defautl code sould look like the following:

<details> <summary> See Output </summary>

```sh
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;

```

</details>

Now remove the following code and we will write our own script, the result should be a blank page

<details><summary> See output </summary>

```sh
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
         <h1>Welcome to Number Changer</h1>
         <h3>Your new number:</h3>
        <input />
        <button>Get Number</button>
        <button>Set Number</button>
      </header>
    </div>
  );
}

export default App;

```

</details>

Your page should now look like [this](assets/Number1.png)

### Interacting with the blockchain

First we need to install and import Web3.js library into our file, which allows us to interact with the blockchain

> Learn more about Web3.js library [here]("https://web3js.readthedocs.io/en/v3.0.0-rc.5/)

In the terminal 

``` sh
npm i web3
```

and in App.js

``` js
import Web3 from "web3";
```

Now we will need to import our contract ABI so that we can have access to our smart contract's functions fromt the blockchain

```js
import NumberChanger from "./build.NumberChanger.json";
```

The first 3 lines of ```App.js``` should look like this

```js
import './App.css';
import Web3 from "web3";
import NumberChanger from "./build/NumberChanger.json";
```

Now we need connect to the blockchain with ```Web3.js``` by creating an instance of it. Since we created a local blockchain with ```ganache-cli```, the address will be on localhost:8545

```js
const web3 = new Web3("http://localhost:8545");
```

> This is hard coded and will be different when you are connecting to the testnet or mainnet

Next, we need to get our contracts address so Web3.js can connect to it. When Truffle migrated the smart contract, it gave information about the transaction and the contract's address is one of them.

```js
2_NumberChanger.js
==================

   Deploying 'NumberChanger'
   -------------------------
   > transaction hash:    0xc879826ffe4bb0d246edd988a414ad2b6544c85a8bde98cabd0e140c91ebd02f
   > Blocks: 0            Seconds: 0
   > contract address:    0x7c2481b87100844E11df966BcCD55E82A138Fe84
   > block number:        3
   > block timestamp:     1639941021
   > account:             0x8f506C687ec10f6c91B7E3A368aF150D970Ccbec
   > balance:             99.9916596
   > gas used:            125653 (0x1ead5)
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.00251306 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00251306 ETH

```

We will now get the contract address and store it in a variable.

```js
const contractAddress = "0x7c2481b87100844E11df966BcCD55E82A138Fe84";
```

> Your contract address will be different from mine when it is deployed

After we have our contract address and our contract's ABI, we can now get our contract's functions and call them. Let's pass them through the Web3.js method ```Contract(contract ABI, contract's address)```store them in a variable called contract

```js
const contract = new web3.eth.Contract(NumberChanger.abi, conctractAddress);
```

> The contract's abi must be appended with ```.abi```

Your code should now look like the following:
<details><summary> See output </summary>

```js
import './App.css';
import Web3 from "web3";
import NumberChanger from "./build/NumberChanger.json";

const contractAddress = "0x7c2481b87100844E11df966BcCD55E82A138Fe84";

function App() {

const web3 = new Web3("http://localhost:8545");


let contract = new web3.eth.Contract(NumberChanger.abi, contractAddress);

  return (
    <div className="App">
      <header className="App-header">
        <h1>Welcome to Number Changer</h1>
        <h3>Your new number:</h3>
        <input />
        <button>Get Number</button>
        <button>Set Number</button>
      </header>
    </div>
  );
}

export default App;

```

</details>

Now that we are able to interact with our contract on the blockchain, we will now write a function to get the current number from the state and set a new number by changing the state

Since we have to change state in React, import ```useState``` from ```react```

```js
import {useState} from "react";
```

Then we will declare in inside the function

```js
const [number, setNewNumber] = useState();
```

Now we will create a function of getting the number from the contract

```js
// Function that gets number from the smart contract
  async function getNumber() {
    try {
      const getStateNumber = await contract.methods.getNumber().call();
      setNewNumber(getStateNumber);
    } catch (error) {
      console.log("Error:", error);
    }
  }
```

We can get the value of the number stored in state from our contract by using the ```methods``` property of ```Contract``` , then the ```getNumber()``` function in our smart contract and finally using ```.call()``` to retreive the number stored in the state variable

Now that we are able to retreive the number set in state from the blockchain, let's now write a function to change the state of number variable with a setter function

```js
async function changeNumber() {
    // Assign array of accounts into getAccount variable
    let getAccount = await web3.eth.getAccounts();
    // Calling setNumber function and using first account to send transaction
    await contract.methods.setNumber(number).send({ from: getAccount[0] });
    // Resets input and h3 to blank
    setNewNumber("");
```

We get the accounts from Ganache using the ```getAccounts()``` method from Web3.js and then assign it a variable. Then using ```contract.methods``` similar to our ```getNumber()``` function, we will use it to call our ```setNumber()``` function from our smart contract from the blockchain and pass in the new number that the user will input. Then we will use the ```send()``` method and pass in the account we want to transact from.

The code should look like this...

```js
import './App.css';
import Web3 from "web3";
import NumberChanger from "./build/NumberChanger.json";

const contractAddress = "0x7c2481b87100844E11df966BcCD55E82A138Fe84";

function App() {

const web3 = new Web3("http://localhost:8545");


let contract = new web3.eth.Contract(NumberChanger.abi, contractAddress);

async function getNumber() {
    try {
      const getStateNumber = await contract.methods.getNumber().call();
      setNewNumber(getStateNumber);
    } catch (error) {
      console.log("Error:", error);
    }
  }

  async function changeNumber() {
    // Assign array of accounts into getAccount variable
    let getAccount = await web3.eth.getAccounts();
    // Calling setNumber function and using first account to send transaction
    await contract.methods.setNumber(number).send({ from: getAccount[0] });
    // Resets input and h3 to blank
    setNewNumber("");

  return (
    <div className="App">
      <header className="App-header">
        <h1>Welcome to Number Changer</h1>
        <h3>Your new number:</h3>
        <input />
        <button>Get Number</button>
        <button>Set Number</button>
      </header>
    </div>
  );
}

export default App;
```

Finally we will implement the functions and update the state on our page with the following in the ```return```:

```jsx
return (
    <div className="App">
      <header className="App-header">
        <h1>Welcome to Number Changer</h1>
        <h3 >
          Your number is: {number}
        </h3>
        <input
          placeholder="Enter a number"
          onChange={ (e) => setNewNumber(e.target.value) }
          value={number}
           />
        <button onClick={getNumber}>Get Number</button>
        <button onClick={changeNumber}>Set Number</button>
      </header>
    </div>
  );
```

Now experiment by setting the number and then getting them. You should also notice the funds in the first account balance lower each time the number is set to pay for the transaction fee.

##