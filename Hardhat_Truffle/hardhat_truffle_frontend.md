# Project Setup Using Hardhat & Truffle - part 5

For the final part of this project, we are going to connect our contract to the front end with React. Since this about writing smart contracts, we won't go too much in to styling the page.

## Frontend setup with Truffle

### Checklist

Here is a quick check list before connect to the frontend

- [ ] Ganache is still running
- [ ] Our contract is compiled and the ```build``` directory is under our ```src``` directory
- [ ] In anther terminal, change into ```scr``` directory of this project

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

Now remove the following code and we will write our own html, the result should be a blank page

<details><summary> See output </summary>

```sh
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
         <h1>Welcome to Number Changer</h1>
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

