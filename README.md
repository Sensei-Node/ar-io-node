# AR.IO Full Node Setup (SenseiNode Fork)

## Overview
This repository is a fork of the AR.IO node, modified for SenseiNode deployment. It provides a streamlined setup process for running a full AR.IO node, including an observer and gateway.

## Requirements

- Docker and Docker Compose
- A domain (DNS) pointing to the server running the node
- Node.js and npm (for generating wallets)

## Clone the Repository

```sh
git clone https://github.com/Sensei-Node/ar-io-node.git
cd ar-io-node
```

## Generate Wallets

### Install ArDrive CLI

Ensure you have Node.js and npm installed, then install ArDrive CLI globally:

```sh
npm install -g ardrive-cli
```

Verify installation:

```sh
ardrive --version
```

### Generate Wallet with Manual Seed Phrase

1. Generate a seed phrase manually:

   ```sh
   ardrive generate-seedphrase
   ```

   This will output a 12-word seed phrase. Save it securely.

2. Use the seed phrase to generate the wallet:

   ```sh
   ardrive generate-wallet -s "your twelve word seed phrase here" > arweave-wallet.json
   ```

3. Verify that the wallet was created correctly:

   ```sh
   cat arweave-wallet.json
   ```

4. Get the wallet address:

   ```sh
   ardrive get-address -w arweave-wallet.json
   ```

5. Move the wallet to the `wallets` directory:

   ```sh
   mv arweave-wallet.json wallets/
   ```

## Configure Environment Variables

Copy the example environment file and modify it:

```sh
cp .example.env .env
```

Edit the `.env` file and update the necessary values:

```
# Gateway URL
TRUSTED_GATEWAY_URL="https://arweave.net"

# Arweave GraphQL settings
GRAPHQL_HOST=arweave.net
GRAPHQL_PORT=443

# Starting block height for transaction indexing
START_HEIGHT=0

# Observer Wallet (replace with your generated wallet address)
OBSERVER_WALLET="your-wallet-address"

# AR.IO Wallet (optional, required for participation in the network)
AR_IO_WALLET="<your wallet address>"

# Root Host for ArNS
ARNS_ROOT_HOST="your-domain"

# ARIO CU for the observer
AO_CU_URL=https://cu.ardrive.io
```

## Run the Node

Start the node using Docker Compose:

```sh
docker-compose up -d
```

This will initialize and run the node with the configured settings.

## Notes on Tokens

You can run an AR.IO node without holding AR tokens, but to earn rewards, you will need tokens in your wallet.

---
