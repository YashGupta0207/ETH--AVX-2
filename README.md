# MetaMask ATM

This project implements a code for makin contract 'MyContract' which asks the use to take the initial value to make changes. It demonstrates basic Solidity and Ethereum functionality, such as incrementing value, decrementing value and compare the value.

## Description

This project includes a smart contract written in Solidity and a frontend application written in ReactJS. The smart contract allows the owner to set the value ,increment and decrement value, and compare the value. The frontend application interacts with the smart contract through MetaMask, providing a user-friendly interface for managing the value set by the user.

## Getting Started

### Prerequisites

To run this project, you need to have the following installed :

- [Node.js](https://nodejs.org/)
- [MetaMask](https://metamask.io/)

### Installing

1. You can use the 'Remix-Ethereum IDE' for running the solidity code. 

3. **Compile the Solidity contract:**
    You can compile your contract in Remix.

4. **Deploy the contract:**
    You can deploy your contract in Remix and use the address for Frontend

### Running the Application

Here is the Solidity code contract:


```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract MyContract {
    uint256 private value;

    // Function to set the value
    function setValue(uint256 _value) public {
        value = _value;
    }

    // Function to get the value
    function getValue() public view returns (uint256) {
        return value;
    }

    // Function to increment the value
    function incrementValue() public {
        value += 1;
    }

    function decrementValue() public {
        value -= 1;
    }

    function comparableValue() public {
        if (value>7){
            value *=2;
        }
    }
}
```



# JavaScript Application

Here is the React code for the frontend application:



```javascript

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Smart Contract Interaction</title>
    <script src="https://cdn.jsdelivr.net/npm/web3@1.3.5/dist/web3.min.js"></script>
</head>
<body>
    <h1>Smart Contract Interaction</h1>
    <div>
        <label for="setValueInput">Set Value:</label>
        <input type="number" id="setValueInput">
        <button onclick="setValue()">Set Value</button>
    </div>
    <div>
        <button onclick="incrementValue()">Increment Value</button>
    </div>
    <div>
        <button onclick="decrementValue()">Decrement Value</button>
    </div>
    <div>
        <button onclick="comparableValue()">Comparable Value</button>
    </div>
    <div>
        <button onclick="getValue()">Get Value</button>
        <p>Value: <span id="valueDisplay"></span></p>
    </div>

    <script>
        const contractAddress = '0xDA07165D4f7c84EEEfa7a4Ff439e039B7925d3dF';
        const contractABI = [
            {
                "inputs": [],
                "name": "getValue",
                "outputs": [
                    {
                        "internalType": "uint256",
                        "name": "",
                        "type": "uint256"
                    }
                ],
                "stateMutability": "view",
                "type": "function"
            },
            {
                "inputs": [
                    {
                        "internalType": "uint256",
                        "name": "_value",
                        "type": "uint256"
                    }
                ],
                "name": "setValue",
                "outputs": [],
                "stateMutability": "nonpayable",
                "type": "function"
            },
            {
                "inputs": [],
                "name": "incrementValue",
                "outputs": [],
                "stateMutability": "nonpayable",
                "type": "function"
            }
        ];

        let web3;
        let contract;

        window.addEventListener('load', async () => {
            if (window.ethereum) {
                web3 = new Web3(window.ethereum);
                await window.ethereum.enable();
                contract = new web3.eth.Contract(contractABI, contractAddress);
            } else {
                console.error('Please install MetaMask!');
            }
        });

        async function setValue() {
            const value = document.getElementById('setValueInput').value;
            const accounts = await web3.eth.getAccounts();
            await contract.methods.setValue(value).send({ from: accounts[0] });
        }

        async function incrementValue() {
            const accounts = await web3.eth.getAccounts();
            await contract.methods.incrementValue().send({ from: accounts[0] });
        }

        async function decrementValue() {
            const accounts = await web3.eth.getAccounts();
            await contract.methods.decrementValue().send({ from: accounts[0] });
        }
        async function comparableValue() {
            const accounts = await web3.eth.getAccounts();
            await contract.methods.comparableValue().send({ from: accounts[0] });
        }

        async function getValue() {
            const value = await contract.methods.getValue().call();
            document.getElementById('valueDisplay').innerText = value;
        }
    </script>
</body>
</html>
```

## Getting Started

To get this project running on your computer, follow these steps:

1. Go to Remix-Etherum IDE run your code and deploy your contract.

2. Copy the address.

3. Paste the address in JavaScript code and then go live. 

6. **Accessing the Application:**
   - Once the frontend is running, open your web browser and go to [[(http://127.0.0.1:5500/ass.html]] to access the application.


## Authors

YASH GUPTA  
@YASH GUPTA


## License

This project is licensed under the MIT License - see the LICENSE.md file for details
