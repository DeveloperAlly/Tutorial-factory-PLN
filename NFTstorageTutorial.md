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

- Solidity (via Open Zeppelin smart contracts)
- React (front end)
- Ethers (React-JS client for web3)
- Hardhat (dev tool)
- Moralis (for contract calling & multi-chain deployments)
- NFT.Storage (IPFS CID creation and Filecoin metadata storage)
- Fleek (front-end deployment to the web on IPFS & Filecoin)
- MetaMask (ALWAYS use a NEW Wallet for testing - NEVER use wallets with real assets in them)
- Node installed
