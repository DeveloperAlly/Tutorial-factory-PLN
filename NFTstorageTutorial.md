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
