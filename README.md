# 🚩 How to do a simple NFT on Conflux

📚 This tutorial is adapted from ETH Scaffold 2 for the purposes of deploying simple NFTs on Conflux

---

🎫 Create a simple NFT on Conflux:

👷‍♀️ You'll compile and deploy your first smart contracts. Then, you'll use a template React app full of important Ethereum components and hooks. Finally, you'll deploy an NFT to a public network to share with friends! 🚀

🌟 The final deliverable is an app that lets users purchase and transfer NFTs. Deploy your contracts to a testnet, then build and upload your app to a public web server. Share your experience and your work on Discord with other Conflux builders.

## Steps:

```sh
git clone https://github.com/intrepidcanadian/conflux-scaffold-nft-example
yarn install
```

- This clones the repo of eth scaffold 2 is adapted similarly to conflux-scaffold. The difference is now that the contract in packages/hardhat/contracts contains a file called "YourCollectible.sol". This solidity file contains the code of the NFT contract we are about to deploy.

The frontend in packages/nextjs/app contains the code for the frontend of the NFT which allow users to mint NFTs and transfer them to other users.

> in the same terminal, start your local network (a local instance of a blockchain):

```sh
yarn chain
```

> in a second terminal window, 🛰 deploy your contract (locally):

```sh
cd conflux-scaffold-nft-example
yarn deploy
```

> in a third terminal window, start your 📱 frontend:

```sh
cd conflux-scaffold-nft-example
yarn start
```

📱 Open [http://localhost:3000](http://localhost:3000) to see the app.

---

## Create your NFT

> ✏️ Mint some NFTs! Click the **MINT NFT** button in the `My NFTs` tab.

![image](https://github.com/scaffold-eth/se-2-challenges/assets/80153681/74cf02f2-4c1b-4278-9841-f19f668e0b1e)

👀 You should see your NFTs start to show up:

![image](https://github.com/scaffold-eth/se-2-challenges/assets/80153681/63dabceb-ad42-4c09-8e5d-a0139939e32d)

👛 Open an incognito window and navigate to http://localhost:3000

🎟 Transfer an NFT to the incognito window address using the UI:

![image](https://github.com/scaffold-eth/se-2-challenges/assets/80153681/3b92fb50-d43f-48a8-838c-c45c443b0b71)

👛 Try to mint an NFT from the incognito window.

> Can you mint an NFT with no funds in this address? You might need to grab funds from the faucet to pay for the gas!

🕵🏻‍♂️ Inspect the `Debug Contracts` tab to figure out what address is the owner of YourCollectible?

🔏 You can also check out your smart contract `YourCollectible.sol` in `packages/hardhat/contracts`.

💼 Take a quick look at your deploy script `00_deploy_your_contract.js` in `packages/hardhat/deploy`.

📝 If you want to edit the frontend, navigate to `packages/nextjs/app` and open the specific page you want to modify. For instance: `/myNFTs/page.tsx`. For guidance on [routing](https://nextjs.org/docs/app/building-your-application/routing/defining-routes) and configuring [pages/layouts](https://nextjs.org/docs/app/building-your-application/routing/pages-and-layouts) checkout the Next.js documentation.

---

## Checkpoint 3: 💾 Deploy your contract! 🛰

🛰 Ready to deploy to a public testnet?!?

> Change the defaultNetwork in `packages/hardhat/hardhat.config.ts` to `sepolia`.

![chall-0-hardhat-config](https://github.com/scaffold-eth/se-2-challenges/assets/55535804/f94b47d8-aa51-46eb-9c9e-7536559a5d45)

🔐 Generate a deployer address with `yarn generate`. This creates a unique deployer address and saves the mnemonic locally.

> This local account will deploy your contracts, allowing you to avoid entering a personal private key.

![chall-0-yarn-generate](https://github.com/scaffold-eth/se-2-challenges/assets/2486142/133f5701-e575-4cc2-904f-cdc83ae86d94)

👩‍🚀 Use `yarn account` to view your deployer account balances.

![chall-0-yarn-account](https://github.com/scaffold-eth/se-2-challenges/assets/2486142/c34df8c9-9793-4a76-849b-170fae7fd0f0)

⛽️ You will need to send ETH to your deployer address with your wallet, or get it from a public faucet of your chosen network.

> Some popular faucets are [https://sepoliafaucet.com/](https://sepoliafaucet.com/) and [https://www.infura.io/faucet/sepolia](https://www.infura.io/faucet/sepolia)

> ⚔️ Side Quest: Keep a 🧑‍🎤 [punkwallet.io](https://punkwallet.io) on your phone's home screen and keep it loaded with testnet eth. 🧙‍♂️ You'll look like a wizard when you can fund your deployer address from your phone in seconds.

🚀 Deploy your NFT smart contract with `yarn deploy`.

> 💬 Hint: You can set the `defaultNetwork` in `hardhat.config.ts` to `sepolia` **OR** you can `yarn deploy --network sepolia`.

---

## Checkpoint 4: 🚢 Ship your frontend! 🚁

> ✏️ Edit your frontend config in `packages/nextjs/scaffold.config.ts` to change the `targetNetwork` to `chains.sepolia` :

![chall-0-scaffold-config](https://github.com/scaffold-eth/se-2-challenges/assets/55535804/3b50c7a7-b9cc-4af3-ab2a-11be4f5d2235)

> You should see the correct network in the frontend (http://localhost:3000):

![image](https://github.com/scaffold-eth/se-2-challenges/assets/80153681/50eef1f7-e1a3-4b3b-87e2-59c19362c4ff)

> 🦊 Since we have deployed to a public testnet, you will now need to connect using a wallet you own or use a burner wallet. By default 🔥 `burner wallets` are only available on `hardhat` . You can enable them on every chain by setting `onlyLocalBurnerWallet: false` in your frontend config (`scaffold.config.ts` in `packages/nextjs/`)

![image](https://github.com/scaffold-eth/se-2-challenges/assets/80153681/f582d311-9b57-4503-8143-bac60346ea33)

> 💬 Hint: For faster loading of your transfer page, consider updating the `fromBlock` passed to `useScaffoldEventHistory` in [`packages/nextjs/app/transfers/page.tsx`](https://github.com/scaffold-eth/se-2-challenges/blob/challenge-0-simple-nft/packages/nextjs/app/transfers/page.tsx#L12) to `blocknumber - 10` at which your contract was deployed. Example: `fromBlock: 3750241n` (where `n` represents its a [BigInt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt)). To find this blocknumber, search your contract's address on Etherscan and find the `Contract Creation` transaction line.

🚀 Deploy your NextJS App

```shell
yarn vercel
```

> Follow the steps to deploy to Vercel. Once you log in (email, github, etc), the default options should work. It'll give you a public URL.

> If you want to redeploy to the same production URL you can run `yarn vercel --prod`. If you omit the `--prod` flag it will deploy it to a preview/test URL.

⚠️ Run the automated testing function to make sure your app passes

```shell
yarn test
```

#### Configuration of Third-Party Services for Production-Grade Apps.

By default, 🏗 Scaffold-ETH 2 provides predefined API keys for popular services such as Alchemy and Etherscan. This allows you to begin developing and testing your applications more easily, avoiding the need to register for these services.  
This is great to complete your **SpeedRunEthereum**.

For production-grade applications, it's recommended to obtain your own API keys (to prevent rate limiting issues). You can configure these at:

- 🔷`ALCHEMY_API_KEY` variable in `packages/hardhat/.env` and `packages/nextjs/.env.local`. You can create API keys from the [Alchemy dashboard](https://dashboard.alchemy.com/).

- 📃`ETHERSCAN_API_KEY` variable in `packages/hardhat/.env` with your generated API key. You can get your key [here](https://etherscan.io/myapikey).

> 💬 Hint: It's recommended to store env's for nextjs in Vercel/system env config for live apps and use .env.local for local testing.

---

## Checkpoint 5: 📜 Contract Verification

You can verify your smart contract on Etherscan by running (`yarn verify --network network_name`) :

```shell
yarn verify --network sepolia
```

> It is okay if it says your contract is already verified. Copy the address of YourCollectable.sol and search it on sepolia Etherscan to find the correct URL you need to submit this challenge.

## Checkpoint 6: 💪 Flex!

👩‍❤️‍👨 Share your public url with a friend and ask them for their address to send them a collectible :)

![gif](https://github.com/scaffold-eth/se-2-challenges/assets/80153681/547612f6-97b9-4eb3-ab6d-9b6d2c0ac769)

## ⚔️ Side Quests

### 🐟 Open Sea

> 🐃 Want to see your new NFTs on Opensea? Head to [Testnets Opensea](https://testnets.opensea.io/)

> 🎫 Make sure you have minted some NFTs on your Vercel page, then connect to Opensea using that same wallet.

![image](https://github.com/scaffold-eth/se-2-challenges/assets/80153681/c752b365-b801-4a02-ba2e-62e0270b3795)

> You can see your collection of shiny new NFTs on a testnet!

(It can take a while before they show up, but here is an example:) https://testnets.opensea.io/assets/sepolia/0x17ed03686653917efa2194a5252c5f0a4f3dc49c/2

---

> 🏃 Head to your next challenge [here](https://github.com/scaffold-eth/se-2-challenges).

> 💬 Problems, questions, comments on the stack? Post them to the [🏗 scaffold-eth developers chat](https://t.me/joinchat/F7nCRK3kI93PoCOk)
