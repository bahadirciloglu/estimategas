EstimateGas Project
This project demonstrates how to deploy and configure CCIP (Cross-Chain Interoperability Protocol) Sender and Receiver contracts across multiple networks, and how to evaluate gas consumption during message transfers.

Prerequisites
Node.js and npm
Hardhat framework
Solidity
Installation
Clone this repository:

bash
Copy code
git clone https://github.com/bahadirciloglu/estimategas
cd estimategas
Install the dependencies:

bash
Copy code
npm install
Compilation
To compile the Solidity contracts, run the following command:

bash
Copy code
npx hardhat compile
Output example:
yaml
Copy code
Generating typings for: 31 artifacts in dir: typechain-types for target: ethers-v6
Successfully generated 114 typings!
Compiled 33 Solidity files successfully (evm target: paris).
Running Tests
The test evaluates the gas consumption of the ccipReceive function. It sends a CCIP message to the MockCCIPRouter contract, triggering the MsgExecuted event. This event provides details on the gas used by the ccipReceive function.

Run the tests with:

bash
Copy code
npx hardhat test
Output example:
yaml
Copy code
Final Gas Usage Report:
Number of iterations 0 - Gas used: 5168
Number of iterations 50 - Gas used: 14718
Number of iterations 99 - Gas used: 24077
✔ should CCIP message from sender to receiver (1716ms)

1 passing (2s)
Deployment
Deploy the Sender contract on Avalanche Fuji testnet:

bash
Copy code
npx hardhat run scripts/deployment/deploySender.ts --network avalancheFuji
Output example:
csharp
Copy code
Deploying Sender contract on avalancheFuji...
wait for 20 blocks
Sender contract deployed at: 0x6C13a1b926264c343f126b0B87D4d69d8C68041E
Verifying Sender contract on avalancheFuji...
The contract 0x6C13a1b926264c343f126b0B87D4d69d8C68041E has already been verified on Etherscan.
https://testnet.snowtrace.io/address/0x6C13a1b926264c343f126b0B87D4d69d8C68041E#code
Deploy the Receiver contract on Ethereum Sepolia testnet:

bash
Copy code
npx hardhat run scripts/deployment/deployReceiver.ts --network ethereumSepolia
Output example:
csharp
Copy code
Deploying Receiver contract on ethereumSepolia...
Receiver contract deployed at: 0xe87f44A7065B4949B76Ab22aa693e68f5ca42FeB
Verifying Receiver contract on ethereumSepolia...
The contract 0xe87f44A7065B4949B76Ab22aa693e68f5ca42FeB has already been verified on Etherscan.
https://sepolia.etherscan.io/address/0xe87f44A7065B4949B76Ab22aa693e68f5ca42FeB#code
Authorize the Sender to send messages to Ethereum Sepolia:

bash
Copy code
npx hardhat run scripts/configuration/allowlistingForSender.ts --network avalancheFuji
Output example:
makefile
Copy code
Allowlisted: ethereumSepolia
Authorize the Receiver to receive messages from the Sender:

bash
Copy code
npx hardhat run scripts/configuration/allowlistingForReceiver.ts --network ethereumSepolia
Output example:
makefile
Copy code
Allowlisted: avalancheFuji, 0x6C13a1b926264c343f126b0B87D4d69d8C68041E
Contract Addresses
Receiver Contract on Ethereum Sepolia: 0xe87f44A7065B4949B76Ab22aa693e68f5ca42FeB
Sender Contract on Avalanche Fuji: 0x6C13a1b926264c343f126b0B87D4d69d8C68041E
Sending CCIP Messages
To send CCIP messages using the deployed contracts, run:

bash
Copy code
npx hardhat run scripts/testing/sendCCIPMessages.ts --network avalancheFuji
Output example:
mathematica
Copy code
Number of iterations 0 - Gas limit: 5685 - Message Id: 0x36f221457f3b3abc09a01cbe84addbb43d40f0031378280d25d2da62cca047fc
Number of iterations 50 - Gas limit: 16190 - Message Id: 0x468209ba10d8778f9c1054837626cad816d6406192088a2183d506aa242b5718
Number of iterations 99 - Gas limit: 26485 - Message Id: 0x420e2d369116008fede8ca360530a76fd42d5389fd4f161ce08290871e9ed1ea
License
This project is licensed under the MIT License.

