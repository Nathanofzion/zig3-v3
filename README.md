# Zig3v3 a Soroswap soroban monorepo

This is a monorepo for Soroban projects.# Zig3V3 is a project that's bundled several open source projects in to reusable packages. The project utilise Stellars protocol 21 for soroban smart contract passkey hash signing. This achieves a decentralized exchange (DEX) that draws inspiration from the Uniswap V2 protocol and is specifically tailored for the Soroban network..

# What can you expact from this project?

We're using the new stellar protocol 20 (Soroban Platform or SVM) for our blockchain smart contracts, these contracts use the Rust programming language with WASM and js for frontend. With these smart contract we aim to provide a UI that interacts with Turing complete smart contracts. You can expact atomic swaps of assets, liquidity pools, Staking, a Zioncoin Airdrop play ground built with three.js, Bridging to other blockchains and passkey hash signing; so you don't need a wallet. We're also aim to build in a rewards program where, community memebers can be rewarded for introducing new members.


Before you begin, ensure you have met the following requirements:

- docker >= v24.0.2
- **Freighter Wallet v5.6.3** Please use this version. You can have an intependent environment following the instructios in [this post](https://discord.com/channels/897514728459468821/1135655444157833256/1135655444157833256)

## 🛠 Setting Up Zig3-Soroswap 🛠

1. Clone the Repository

```bash

git clone https://github.com/Nathanofzion/Zig3v3.git
cd packages/Zig3-soroswap
```

2. Set Up Environment Variables

Copy the .env.example file to create a new .env file:

```bash
cp .env.local.example .env
```

Now, edit the `.env` file and provide the `NEXT_PUBLIC_BACKEND_URL`, `NEXT_PUBLIC_SOROSWAP_BACKEND_API_KEY` and `NEXT_PUBLIC_TEST_TOKENS_ADMIN_SECRET_KEY` variables.
This will tell the frontend where to look for:

- the list of known tokens
- the SoroswapFactory address
- the SoroswapRouter address
- the admin key for token minting

If you are following the instructions in `https://github.com/soroswap/core` in order to deploy the smart contacts in your local environment and serve the API. you should have:
```bash
NEXT_PUBLIC_BACKEND_URL=http://localhost:8010
```
If you don't want to use the backend, you should also set the following variable:
```bash
NEXT_PUBLIC_SOROSWAP_BACKEND_ENABLED=false
```

Also, the variable `NEXT_PUBLIC_TEST_TOKENS_ADMIN_SECRET_KEY` should be the same as the one that deployed the tokens in the `core` repository.

If you are ready for production, you can take Futurenet Contracts information from `https://api.soroswap.finance` and just do

```bash
cp .env.production.example .env
```

❗️❗️ Note that some Futurenet RPC's might not have the same version, so we recomend you to connect to a local quickstart node following the instructions in `https://github.com/soroswap/core`; and setting up your Freighter Wallet as in step 6.

1. Install the monorepo dependencies so all packages are able to be consumed by Zig3-soroswap:

```bash
pnpm install
```

2. Run the Development Instance

Now you are ready to start the development instance. To run the main Zig3-soroswap UI application, use:

```bash
pnpm --filter zig3-soroswap run dev
```

This command will start only the `ui-package`, allowing it to consume the dependencies from the other submodules.
Use start to run outside dev.

```bash
pnpm --filter zig3-soroswap start
```

### 7. Update or Clone with Submodules

When you clone your main repository, remember to initialize and update the submodules:

```bash
git clone --recurse-submodules <repository-url>
```

If you've already cloned the repository, you can use:

```bash
git submodule update --init --recursive
```


1. Start Docker

Navigate to the the `run.sh` script inside the `docker` folder

```bash
bash docker/run.sh
```

This script will set up and start the Docker containers required for Soroswap.

4. Install the Dependencies (This should be done in the package.json via script when pnpm install is envoked from root)

After the Docker container is up, you will be inside the root folder on the container. Then, install the dependencies using Yarn:

```bash
yarn install
```

5. Run the Development Instance

Now you are ready to start the development instance. Run the following command:

```bash
yarn dev
```

This will start the Soroswap development instance.

6. Configure your Freigher Wallet

For Standalone network
| | |
|---|---|
| Name | Local Standalone |
| HORIZON RPC URL | http://localhost:8000 |
| SOROBAN RPC URL | http://localhost:8000/soroban/rpc |
| Passphrase | Standalone Network ; February 2017 |
| Friendbot | http://localhost:8000/friendbot |
| Allow HTTP connection | Enabled |
| Switch to this network | Enabled |

For Futurenet network
| | |
|---|---|
| Name | Local Futurenet|
| HORIZON RPC URL | http://localhost:8000 |
| SOROBAN RPC URL | http://localhost:8000/soroban/rpc |
| Passphrase | Test SDF Future Network ; October 2022 |
| Friendbot | http://localhost:8000/friendbot |
| Allow HTTP connection | Enabled |
| Switch to this network | Enabled |

** Important:** You should also do: Preferences> Allow experimental mode

7. Last, but not least, add some lumens to your Freighter wallet!

Do it directly on the wallet or use:

For Standalone: `http://localhost:8000/friendbot?addr=<your address>`
For Futurenet, visit: https://laboratory.stellar.org/#create-account

🚀 Congrats! 🚀

You have successfully set up Soroswap on your local machine! Start swapping, pooling, and exploring the possibilities of decentralized finance (DeFi) on the Soroban network.

## 🧪🔨 Testing 🧪🔨
To execute the tests, you must first start the development container. To do this, run the following command from your host machine:

```bash
bash docker/run.sh
```
Once the development container is running, you can install the dependencies for the tests by running the following command:

```bash
## 🧪🔨 Testing 🧪🔨
To execute the tests, you must first start the development container. To do this, run the following command from your host machine:

```bash
bash docker/run.sh
```
Once the development container is running, you can install the dependencies for the tests by running the following command:

```bash
yarn install
```

Finally, to run the tests, run the following command from within the development container:

```bash
yarn test
```
This will run all of the unit and integration tests for the project.

The tests are written using Vitest & testing-library.

For more information on Vitest, please see the Vitest documentation: https://vitest.dev/.

For more information on Testing Library, please see the Testing Library documentation: https://testing-library.com/docs/react-testing-library/intro/

## 🔧🧪 E2E - Integration test environment setup 🔧🧪
**1. Set up the development environment:**
>[!TIP]
>Instructions can be found in the "[🛠 Setting Up Soroswap 🛠](#-setting-up-soroswap-)" section from step 1 to 4, located at the beginning of the document.

**2. Install the new dependencies:**
```
yarn install
```
**3. Configure Freigther wallet:**

1. Start the test browser for the first time:**
```
yarn wdio
```
> [!IMPORTANT]
>(This will take a moment and all tests will fail. This is normal because the wallet is not yet configured and the application is not running yet.)

2. Create a wallet or import an existing one:

In a new tab, go to:
> chrome-extension://bcacfldlkkdogcmkkibnjlakofdplcbk/index.html#

and create/import a wallet, configure a password, and save it in the file ./test/specs/e2e.test.ts within the variable "walletPassword".

3. Configure the network for testing:
>[!TIP]
>To configure the network, you can review step 6 of "[🛠 Setting Up Soroswap 🛠](#-setting-up-soroswap-)" and configure the network of your choice.
4. Fund the wallet with firendbot

**4. Run the development instance:**

In the terminal opened in step 1 (Which runs the development container), run the command:
```
yarn dev
```

**5. Restart the tests:**
1. Press **Ctrl**+**C** in the tests terminal to kill the test process.
>[!TIP]
>If after shutting down wdio your terminal seems to be stucked, press intro to refresh it

2. Run the following command to restart the tests:
```
yarn wdio
```

**6. Evaluate the test results:**

After the tests have been executed, you will find the output in the terminal detailing which tests passed and which did not, as well as the reason for the failure in these.


## Contributing

If you find a bug or have a feature request, please create an issue or submit a pull request. Contributions are always welcome!

License: MIT

## Acknowledgments

Special thanks to the Uniswap team for providing the base protocol on which Soroswap is built.
Thank you to the Stellar Community for the continuous support.

---

---

Made with ❤️ by the Soroswap Team.