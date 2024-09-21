# EthGlobal Singapore (September 2024)

# HarvestReward
HarvestReward is a decentralized platform designed to transform the agricultural supply chain using blockchain technology. Built on Hedera Hashgraph, the platform offers secure, transparent, and efficient solutions for farmers, cooperatives, buyers, agribusinesses, and regulators. HarvestReward enables seamless information sharing, product traceability, and automated financial transactions through smart contracts, while fostering sustainability and financial inclusion.

# Key Features
## Supply Chain Transparency
Track agricultural products from farm to consumer using an immutable ledger that ensures transparency and traceability at every step of the supply chain.

## Smart Contracts
Automate agreements between farmers, buyers, logistics providers, and other stakeholders. Contracts automatically trigger payments, logistics updates, and insurance payouts based on predefined conditions.

## Decentralized Finance (DeFi)
Farmers can access microloans, insurance, and decentralized payments using tokenized assets like future crop yields. This feature supports financial inclusion, particularly for smallholder farmers in underserved regions.

## IoT Integration
Real-time data from IoT devices, such as soil moisture sensors and weather data, is integrated into the blockchain to provide actionable insights and ensure accurate contract execution.

## Tokenization
Crop yields, livestock, and environmental assets like carbon credits can be tokenized, allowing fractional ownership and easier trading on global markets.

# Technology Stack

## Hedera Hashgraph
Powers the platform with its high throughput, low transaction costs, and energy-efficient consensus mechanism, ensuring secure and scalable transactions.

## Worldcoin
Provides decentralized identity (DID) verification for farmers and stakeholders, ensuring secure and inclusive access to the platform, enhancing trust and preventing identity fraud.

## Chainlink Oracles
Integrates real-world data, such as weather conditions and logistics updates, into the blockchain, enabling accurate and reliable execution of smart contracts.

# Project Example

The following are project examples to demonstrate the high-level project features and functions. 

## Hedera Hashgraph Example

Prerequisites:
(1) Node.js installed.
(2) Hedera SDK installed (npm install @hashgraph/sdk).
(3) Testnet or Mainnet access with account credentials (private key and account ID).

// Import the Hedera Hashgraph SDK
const { Client, AccountId, PrivateKey, Hbar, AccountCreateTransaction, TransferTransaction, AccountBalanceQuery } = require("@hashgraph/sdk");

// Set up your Hedera testnet credentials
const operatorId = AccountId.fromString("your-account-id");
const operatorPrivateKey = PrivateKey.fromString("your-private-key");

// Create a Hedera client for the testnet
const client = Client.forTestnet();
client.setOperator(operatorId, operatorPrivateKey);

// Function to create a new account
async function createAccount() {
    // Generate a new key pair for the account
    const newPrivateKey = PrivateKey.generate();
    const newPublicKey = newPrivateKey.publicKey;

    // Create a new account with an initial balance of 10 HBAR
    const transaction = new AccountCreateTransaction()
        .setKey(newPublicKey)
        .setInitialBalance(new Hbar(10)); // 10 HBAR

    // Submit the transaction
    const txResponse = await transaction.execute(client);

    // Get the receipt of the transaction
    const receipt = await txResponse.getReceipt(client);

    // Get the new account ID
    const newAccountId = receipt.accountId;

    console.log("New account created with ID:", newAccountId.toString());
    console.log("New account private key:", newPrivateKey.toString());

    return { newAccountId, newPrivateKey };
}

// Function to transfer HBAR between accounts
async function transferHbar(fromAccountId, fromPrivateKey, toAccountId, amount) {
    // Create a transfer transaction
    const transaction = new TransferTransaction()
        .addHbarTransfer(fromAccountId, new Hbar(-amount))  // Sending HBAR
        .addHbarTransfer(toAccountId, new Hbar(amount));    // Receiving HBAR

    // Sign the transaction with the sender's private key
    const signTx = await transaction.freezeWith(client).sign(fromPrivateKey);

    // Submit the transaction to Hedera
    const txResponse = await signTx.execute(client);

    // Get the receipt of the transaction
    const receipt = await txResponse.getReceipt(client);

    console.log(`Transfer of ${amount} HBAR from ${fromAccountId} to ${toAccountId} was successful: Status - ${receipt.status}`);
}

// Function to get account balance
async function getAccountBalance(accountId) {
    const balance = await new AccountBalanceQuery()
        .setAccountId(accountId)
        .execute(client);

    console.log(`Account ${accountId} balance: ${balance.hbars.toString()} HBAR`);
}

// Example usage
(async () => {
    // Create a new account
    const { newAccountId, newPrivateKey } = await createAccount();

    // Get balance of the new account
    await getAccountBalance(newAccountId);

    // Transfer HBAR from operator to the new account
    await transferHbar(operatorId, operatorPrivateKey, newAccountId, 5);

    // Get balance of the new account after transfer
    await getAccountBalance(newAccountId);
})();

## Worldcoin Example

## Chainlink Oracles Example





