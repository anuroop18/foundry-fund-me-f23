# FundMe - Crowd Sourcing App

Welcome to **FundMe**, a decentralized crowdfunding platform built on Ethereum, where users can securely fund projects and withdraw their contributions. This project demonstrates how a simple crowd-sourcing platform can be implemented using smart contracts with Solidity and tested using Foundry.

## Table of Contents
- [About](#about)
- [Getting Started](#getting-started)
  - [Requirements](#requirements)
  - [Quickstart](#quickstart)
- [Usage](#usage)
  - [Testing](#testing)
  - [Deploying Contracts](#deploying-contracts)
  - [Interacting with Contracts](#interacting-with-contracts)
- [Security](#security)
- [Contributing](#contributing)
- [License](#license)

---

## About

FundMe is a decentralized crowdfunding platform where users can contribute ETH to fund projects. The platform utilizes a price feed oracle (via Chainlink) to ensure that the minimum funding amount is always a specific value in USD. Users can fund the contract, and only the owner can withdraw the accumulated funds. The project uses smart contracts written in Solidity, tested with Foundry, and deployed to various Ethereum networks like Sepolia.

---

## Getting Started

Follow these steps to get the project up and running on your local machine.

### Requirements

- [Foundry](https://book.getfoundry.sh/) - Solidity development and testing framework
- [Node.js](https://nodejs.org/) - JavaScript runtime for managing packages
- [Alchemy](https://www.alchemy.com/) - For Ethereum network access (e.g., Sepolia Testnet)
- [Etherscan API](https://etherscan.io/) - For contract verification
- Ethereum account with some Sepolia ETH (for testing on Sepolia network)

### Quickstart

1. **Clone the repository:**
   ```bash
   git clone https://github.com/anuroop18/foundry-fund-me-f23
   cd foundry-fund-me-f23
   ```

2. **Install dependencies:**
   Foundry is required for building, testing, and deploying smart contracts. Ensure you have it installed.

   ```bash
   forge install
   ```

3. **Set up environment variables:**
   Create a `.env` file in the root directory and fill in your keys and URLs.
   ```bash
   SEPOLIA_RPC_URL = "https://eth-sepolia.g.alchemy.com/v2/YOUR_ALCHEMY_KEY"
   PRIVATE_KEY = "0xYOUR_PRIVATE_KEY"
   ETHERSCAN_API_KEY = "YOUR_ETHERSCAN_API_KEY"
   ```

4. **Compile the project:**
   Run the following command to compile the smart contracts.
   ```bash
   forge build
   ```

---

## Usage

### Testing

Run the tests using Foundry. The tests are essential for ensuring that all smart contracts work as intended.

```bash
forge test
```

To run specific tests with more detailed logs, use the verbose mode:
```bash
forge test --match-test testUserCanFundInteractions -vvv
```

### Deploying Contracts

To deploy the smart contract to a local testnet (Anvil) or public testnets like Sepolia, use the following steps.

1. **Deploy to Sepolia:**
   Make sure your `.env` file has the correct values for `SEPOLIA_RPC_URL`, `PRIVATE_KEY`, and `ETHERSCAN_API_KEY`.

   Run the deployment command:
   ```bash
   make deploy-sepolia
   ```

   This will deploy the `FundMe` contract to the Sepolia test network, and automatically verify the contract on Etherscan.

### Interacting with Contracts

Once deployed, you can fund the contract and withdraw funds using the interaction scripts.

1. **Funding the contract:**
   You can fund the contract by running the following script:

   ```bash
   forge script script/Interactions.s.sol:FundFundMe --rpc-url $(SEPOLIA_RPC_URL) --private-key $(PRIVATE_KEY) --broadcast
   ```

2. **Withdrawing funds:**
   To withdraw the funds as the contract owner, use:

   ```bash
   forge script script/Interactions.s.sol:WithdrawFundMe --rpc-url $(SEPOLIA_RPC_URL) --private-key $(PRIVATE_KEY) --broadcast
   ```

---

## Security

- **Private Key Protection:** Ensure that you never commit your private key to version control. Use a `.env` file to store sensitive information and avoid sharing it publicly.
- **Chainlink Oracle Security:** This contract relies on Chainlink oracles for getting price feeds, which adds a layer of security and reliability for determining the minimum funding in USD.

---

## Contributing

Contributions are welcome! If you'd like to contribute, please fork the repository and make your changes via a pull request.

### Steps to Contribute:

1. Fork the repository
2. Create a new branch (`git checkout -b feature-branch`)
3. Commit your changes (`git commit -m "Added new feature"`)
4. Push the branch (`git push origin feature-branch`)
5. Create a pull request

---

## License

This project is licensed under the MIT License.

