# Coding NFTs the Right Way

## With IPFS & Filecoin

### Original presentation created by: Ally Haire (Developer Advocate--Filecoin Foundation)

### Adapted to written tutorial by: Dawn Kelly (Developer Advocate--Protocol Labs)

## Introduction

This workshop will provide a brief introduction to IPFS and Filecoin. We will then dive into making an NFT using IPFS and FIlecoin to store the metadata persistently and immutably to protect the value of your digital assets over time. Before we are through, we will walk through all the code you need to create your very own immutable NFTs using NFT.storage to upload and store your metadata.

[comment]: # (TODO: link needed)

*TL; DR: If you are already familiar with IPFS & Filecoin, you can jump straight to the coding demo [here] (link to demo section in this doc)*

First, let’s clear up any confusion that may be out there around a few names you’ve probably heard floating around the web3 ecosystem and how they fit together. You have probably heard of Protocol Labs, IPFS, Filecoin, and the Filecoin Foundation. Many times these names are used interchangeably and, while they are all tightly affiliated, they are all actually separate organizations.

[comment]: # (TODO: infographic showing PL, FF, F, & IPFS logos & relationships)

![Infographic showing relationships between Protocol Labs, Filecoin Foundation, Filecoint, & IPFS](https://www.markdownguide.org/assets/images/tux.png)

### Protocol Labs

Founded in 2013 by Juan Benet, Protocol Labs is a fully distributed open-source R&D organization which builds protocols, tools, and services aimed at helping to radically improve the internet and drive breakthroughs in computing to help move humanity forward. These are some big goals for sure and, luckily, some truly powerhouse people are working to help drive this research and mission.

### IPFS (InterPlanetary File System)

[comment]: # (TODO: link to IPFS docs)

[IPFS] (link to IPFS docs) is more than just a cool, futuristic name. As a distributed, peer to peer network for files and folders, it was designed to be able to work even when the network is between planets! IPFS uses cryptography to address content by what it is instead of where it is. This creates the ability to retrieve content from the peer closest to you. If we were all hanging out in our shiny, new Mars colony, we could request files from each other quickly rather than waiting for signals to travel to centralized servers back on Earth and then back to us. IPFS is distributed and decentralized by design , has no central authority servers for censorship resistance, is designed to be offline first for resilience, and provides trustless verifiability of stored data through cryptographic hashes called Content IDs (CIDs).

[comment]: # (TODO: infographic showing same CID = same content)

![Infographic showing relationship between CID and data content](https://www.markdownguide.org/assets/images/tux.png)

It’s worth taking a moment to talk a bit more here about Content Ids (CIDs). IPFS takes content and uses SHA-256 cryptography to create a deterministic hash representation of that data. In simple terms, changing one character or pixel of that saved data would create a completely new CID. In practice, this means you can be assured a CID match means you are getting back the data you expected and it remains immutable. You can see why this is desirable for use cases like NFTs where value is derived from authenticity and uniqueness.

### Filecoin

A peer to peer network is only useful if you have a healthy number of distributed peers to participate in storing and sharing data. Most people require an incentive to participate in this type of structure. Filecoin is designed to leverage a crypto-economic incentive model together with cryptographic proofs in order to ensure data is stored persistently, reliably, and verifiably across a distributed network. Its use of cryptographic proofs also enables smart-contract based permanence, and means that it is designed to be as permanent as you, the data owner, want it to be. Whether that permanence requirement is for 500 years or 5 minutes, you have total control over the timeframe you want for your storage and how many copies of it you want to ensure for resilience.

### Filecoin Foundation

[comment]: # (TODO: link to FF docs)

The Filecoin [Foundation] (link to FF docs) is the steward of the Filecoin community, aspiring to put the power of humanity’s most important information back into the hands of everyone. The foundation provides resources, guidance, and fair, equitable principles to help the ecosystem flourish, and to open up the internet for a safer, stronger, and more reliable environment where everyone can thrive.

## NFT Use Case

Whether you want to use the ERC-721 token standard, or the more recently released ERC-1155 multi-token standard, a best practice approach is to leverage the community vetted, security audited, open-sourced smart contracts available through Open Zeppelin. Open Zeppelin has a range of standard implementations and utility contracts and libraries that are used widely by the community to create NFTs on any ethereum compatible chains.

[comment]: # (TODO: add graphic GameItem contract from OZ)

![Image showing sample Open Zeppelin ERC721 contract](https://www.markdownguide.org/assets/images/tux.png)

The main function we want to look at here is the mint and setTokenURI functions though. If we look at this example contract implementation, we can see that this contract creates a numbered ID GameItem for a player (with a wallet address) and takes a tokenURI (or Universal resource identifier) as a parameter. This is where it gets interesting, because the tokenURI is simply a JSON object containing the unique characteristics of the NFT - Thor’s hammer in this example.

[comment]: # (TODO: add graphic tokenURI JSON example)

![Image showing tokenURI JSON document](https://www.markdownguide.org/assets/images/tux.png)

What’s important is that we really want to ensure that our metadata conforms to the characteristics we’re looking for in our NFT - particularly its non-fungibility and uniqueness . So where and how we save this metadata is an important consideration.

There are three main options to save this NFT metadata. 1) You can save it on-chain via the contract itself. This can get prohibitively expensive on higher gas fee chains, particularly for larger files like images, music or video files. 2) You can use a http address to fetch the NFT properties, as shown with the image address in the JSON object above. There are unfortunately multiple issues with this approach. One is that we are relying on someone to continue to pay for this storage. We are also relying on this http address always resolving to the same data. If someone wants to change this data and has access to this server, our non-fungible property will be lost. 3) This brings us to the third option. You can save this metadata as an IPFS CID and store it on Filecoin. This approach guarantees verifiable immutability of your NFT metadata to give your holders peace of mind.

## IPFS & Filecoin: DevTools

Now you know why you want to store your NFT metadata using IPFS and Filecoin but, how do you get started? Let’s take a look at some developer tools to make it easier to use IPFS and Filecoin in your projects.

### NFT.storage

[comment]: # (TODO: link to NFT.storage docs)

[NFT.storage] (link to NFT.storage docs) was created as a public good to archive and persist NFT data. It creates an IPFS CID for your NFT metadata and then makes an automatic deal to store this content persistently on Filecoin with eight or more times redundancy. Over 25 million NFTs are currently stored on NFT.storage and it is used by both OpenSea and Magic Eden. The service is free as the team is committed to NFT metadata as a public good. Work is in progress to build renewal of Filecoin storage deals into smart contracts so there will be no need to trust a centralized entity for renewals.

### Web3.storage

[comment]: # (TODO: link to Web3.storage docs)

[Web3.storage] (link to docs)  is another project built by IPFS and Filecoin and designed to give you the benefits of decentralized storage and IPFS content addressing with the frictionless experience you expect in a modern storage solution. The service is also free to use and store up to 1 TB of data and compatible with both JavaScript and Go client libraries.

### Fleek hosting

[comment]: # (TODO: link to Fleek docs)

[Fleek] (link to Fleek docs) is a CI/CD tool you can use to deploy your apps for free as simply and easily as you would with some of the web2 tools you might be familiar with like Netlify or Vercel. Fleek uses IPFS to host your site or app and even offers ENS domain routing on their platform.

## NFT Demo

It’s the part we’ve all been waiting for: let’s build something! The tech stack for this demo includes:

[comment]: # (TODO: links to docs for each)

- [Solidity] (link) (via Open Zeppelin smart contracts)
- [React] (link to docs) (front end)
- [Ethers] (link to docs) (React-JS client for web3)
- [Hardhat] (link to docs) (dev tool)
- [Moralis] (link to docs) (for contract calling & multi-chain deployments)
- [NFT.Storage] (link to docs) (IPFS CID creation and Filecoin metadata storage)
- [Fleek] (link to docs) (front-end deployment to the web on IPFS & Filecoin)
- [MetaMask] (link to docs) (ALWAYS use a NEW Wallet for testing - NEVER use wallets with real assets in them)
- [Node] (link to docs) installed

[comment]: # (TODO: links to GH repos)

The full GitHub code repo is [here] (link to repo). You can view the ReadMe and Quickstart guide here.

For this demonstration, we’ve created a small dynamically minted NFT project with the option of using the Open Zeppelin ERC-721 or ERC-1155 smart contract and leveraging NFT.storage; a devtool which does the heavy lifting of IPFS and Filecoin for us and is designed specifically for NFTs. Dynamically minting the NFT just means that we aren’t creating/minting the NFT until the contract is called. This contract call could come from your website front end or in-game logic like a player leveling up or similar. You can deploy these contracts to any EVM-compatible chain including Polygon, AVAX, BSC or, of course, Ethereum.

If you are taking the build it from scratch approach, follow these steps:

:rocket: In your terminal, install and create either a NextJS app or React app

```npx create-next-app@latest``` or ```npx create-react-app[projectName]```

:rocket: Navigate to your app

```cd [projectName]``` and rename the README.md file (ex. README_React.md)

:rocket: Still in the terminal, install and make a Hardhat project
```npm install –save-dev hardhat```
```npx hardhat```

- Choose create a basic sample project and say yes to all the questions
- Rename the README.md file (ex. README_Hardhat.md)

:rocket: Install dotenv and create .env file
```npm install dotenv```
```touch.env```

[comment]: # (TODO: link to Moralis docs)

:rocket: Create a server for the smart contracts as per the [Moralis] (link to docs) documentation. We’ve used Moralis so we can deploy to multiple EVM-compatible chains and can use their React hooks. Other options are Chainstack, Alchemy, Infura, and Quicknode.

[comment]: # (TODO: add graphic Moralis screenshot)

![Image showing user interface to create a new server on Moralis](https://www.markdownguide.org/assets/images/tux.png)

[comment]: # (TODO: link to GH .env.example)

:rocket: Add your .env variables as per [.env.example] (GH link) We will add the deployed contract ones later so you can leave these blank for now.

[comment]: # (TODO: link to HH config docs & sample hardhat.config.js file)

:rocket: Create your [hardhat.config] (HH config docs link) file per [hardhat.config.js] (HH config example file link from repo) example.

[comment]: # (TODO: link to Remix docs)

:rocket: Time to make our contract and test it on [Remix](link to Remix docs)!

- In the terminal, install some more dependencies:

```npm install @openzeppelin/contracts @nomiclabs/hardhat-etherscan```

[comment]: # (TODO: link to OZ docs)

- We don’t need to write a smart contract from scratch when using EVM-compatible chains. We can use a template library provided by [OpenZeppelin] (link to docs) which is security audited and community tested.

A note on ERC standards: The original standard template for NFTs was defined in the Ethereum Improvement Proposal ERC-721. EIPs describe the standards for the Ethereum platform like core protocol specs, client APIs and contract standards. Many chains also have their own versions of Improvement Proposals (like FIP - Filecoin Improvement Proposal). An improvement proposal is "proposed" by the community - this could be core dev's, members of the ecosystem or anyone in the world. The community then discusses this proposal and it then goes through a process of approval which generally includes an auditing review also. ERC's on the other hand are Ethereum Request for Comments. It's a weird name leftover from an original developer draft proposal, that basically means it's related to a specific category of EIPs that work on the application level (ie. it means that it's not a core function of the chain's code and doesn't need to be adopted by all participants). 

[comment]: # (TODO: link to EIP1155, link to OZ ERC1155, link to Stack Overflow)

ERC721 is perfectly fine for creating a basic NFT and when this demo was first created - it was the only one available. However, there's recently been a new proposal that is a multi token standard called [EIP1155] (link to EIP1155). This standard proposes the ability to create NFTs and fungible tokens in one contract and adds some cool new features like batch minting to NFTs. While I don't need either of these new features for this demo, I'm choosing to use OpenZeppelin's ERC1155 [template] (link to OZ template) because of the gas optimisations it provides due to it's more efficient method for data storage (see [this] (link to SO) great write up on Eth StackOverflow) and also because who knows where this project might go - maybe we'll want to add fungible tokens at some point?

:rocket: create a file for a new Solidity smart contract called FilGoodNFT.sol

:rocket: Import the ERC1155 contract. We’re also going to use a debugger tool from Hardhat that will give us the ability to console.log variables and a counter utility library from OpenZeppelin that will allow us to give the NFTs individual numbers easily

```import "@openzeppelin/contracts/token/ERC1155/ERC1155.sol";
  import "@openzeppelin/contracts/utils/Counters.sol";
  import "hardhat/console.sol";```

