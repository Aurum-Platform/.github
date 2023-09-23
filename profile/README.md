<p align = "center"> 
  <img src="./svg.svg" height="70" width="80" style="background-color: black; display: inline-block;">
  <h2 align="center">Aurum-Protocol</h2>
</p align = "center">
  <p align="center">
   NFT Lending Borrowing Solution 
    <br />
    <a href="https://nft-lending-borrowing-protocol.vercel.app/"><strong>Try it out (on sepoli) »</strong></a>
    <br />
    <br />
    
- [About The Project](#about-the-project)
- [Inspiration](#inspiration)
- [Protocol Architecture](#protocol-architecture)
  - [Collateralization and Borrowing](#collateralization-and-borrowing)
  - [Loan Terms and Repayment](#loan-terms-and-repayment)
  - [Lenders and Yield Generation](#lenders-and-yield-generation)
  - [Advantages](#advantages-over-peer-to-peer-lending)
- [Oracle Architecture](#aurum-oracle)
  - [Chainlink Node Setup and Job Execution](#chainlink-node-setup-and-job-execution)
  - [NFT Floor Price request](#requesting-nft-floor-price-through-aurum-client-contract)
  - [Fetching Floor Price](#fetching-nft-floor-price-and-providing-to-user)
- [Links and references](#links-and-references)

---

## About The Project
✨ Aurum is an over-collateralized NFT Custodial Lending and Borrowing Protocol that allows users to borrow ETH using their NFT as collateral while enabling lenders to earn interest on their deposited ETH by participating in the protocol's lending pool. <br />
✨It offers easier access to liquidity, lower interest rates, and enhanced security compared to peer-to-peer lending platforms.

---
## Inspiration
The inspiration behind our NFT lending and borrowing platform emerged from the growing popularity and potential of non-fungible tokens (NFTs) in the digital asset space. <br /> <br />
As a team of passionate developers and financial enthusiasts, we recognized the immense value locked within NFTs and sought to harness their potential in the world of decentralized finance (DeFi).
The concept of collateralizing digital assets is not new, but the emergence of NFTs presented a unique opportunity to extend this practice to a previously untapped market. NFTs possess inherent value due to their uniqueness, scarcity, and the underlying digital art, collectibles, or virtual assets they represent. However, owners often faced challenges in unlocking liquidity from these illiquid assets. <br />
Driven by the desire to address this gap, we set out to create a **decentralized platform** that would empower NFT owners to leverage their assets to access the liquidity they need in a secure and trustless manner. 
***

## Protocol Architecture
![image](https://github.com/Aurum-Platform/.github/assets/106421807/daa31764-54ba-4be0-96f5-f98977a2c104)

### Collateralization and Borrowing:
  Users can securely borrow ETH by using their NFT as collateral. The collateral value of the NFT is determined by the **Chainlink NFT Price Feed oracles**, and it uses **Chainlink ETH to USD Price Feed oracle** to get the ETH to USD price for the protocol, which provides real-time price valuation of NFTs. Additionally, the user's borrowing power is calculated based on the NFT value fetched by the oracles multiplied by the loan-to-value ratio of the asset.

### Loan Terms and Repayment:
After determining the price of NFT and their borrowing power, users can secure a loan at an interest rate specified by the protocol. Borrowers must repay the loan before the debt maturity date to avoid liquidation of their collateral. If a borrower fails to repay the loan in time, the debt position is liquidated, and the NFT is auctioned in the protocol's "NFTs Auction" section, with the value determined by the Chainlink Price Feed oracle.

### Lenders and Yield Generation:
  Aurum allows lenders to participate in the protocol by lending ETH to the pool. Lenders earn interest on their participation initially set by the protocol's governance. The APY may vary based on the utilization of the pool, which refers to the `(total borrow / total supply)` in the pool. Lenders can have passive income while contributing to the liquidity of the protocol.

### Advantages over Peer-to-Peer Lending:
  Aurum offers several advantages compared to traditional peer-to-peer lending and borrowing protocols:

  * **Easy and Fast Liquidity Access:** Users can access liquidity more easily and quickly as there is no need to find specific lenders or borrowers. The protocol acts as an intermediary, matching borrowers with available liquidity.

  * **Lower Interest Rates and Fees:** Borrowers can benefit from lower interest rates and fees due to increased competition and efficiency within the protocol. The decentralized nature of the protocol eliminates the need for intermediaries, reducing costs for borrowers.

  * **Reduced Risk of Default and Fraud:** Aurum employs algorithms and incentives to value and verify NFTs, mitigating the risk of default and fraud. The protocol ensures that NFTs used as collateral are accurately valued and authentic, providing a secure borrowing environment.
  
---

## Aurum Oracle

![image](https://github.com/Aurum-Platform/.github/assets/106421807/486c4129-241c-4de0-bbaa-65687d48baf7)

### Chainlink Node Setup and Job Execution

 * A Chainlink node is established to facilitate data retrieval processes.
 * A Chainlink TOML job is configured within the node to interact with an external adapter via a Chainlink bridge.

### Requesting NFT Floor Price through Aurum Client Contract

 * When a user requests the floor price of an NFT, it triggers the Aurum client contract.
 * If the price is present in the contract before the deadline it is return.
 * Else this contract subsequently calls a pre-deployed oracle contract, initiating a connection with a live Chainlink node.

### Fetching NFT Floor Price and Providing to User

 * The Chainlink node, runnig the configured TOML job, through the bridge, calls the external adapter, which in turn contacts an external API to retrieve the NFT floor price.
 * The external adapter fulfills the TOML job, and the node calls the oracle with the acquired floor price.
 * The oracle verifies the address of the node and incoming data from the Chainlink node, ensuring its authenticity, and then provides the verified floor price to the user through multiple on chain calls.

### Chainlink standard schema for Any API
![architecture](https://github.com/Aurum-Platform/.github/assets/106421807/444b59f5-758d-409a-90d3-598f7a6d2879)
  
---
## Links and references
- Contract on Etherscan: [Etherscan](https://sepolia.etherscan.io/address/0xff0af63633f2feeb37a9e6bd46013a6333b20460)
- Figma File's: [Figma](https://www.figma.com/file/glPqL1ZHLqNwPauBKnm7Kw/Untitled?type=design&node-id=0-1&t=VFufaBNNwZgKHQ5y-0)
- Subgraphs' Link: [Subgraph](https://thegraph.com/studio/subgraph/aurumv1core_/)
- Reference chainlink repo: [Repo](https://github.com/zeuslawyer/cl-fall22-external-adapters.git)
