# BlockChain

## What exactly is Blockchain?

The blockchain is general terms is defined in following manner:

- A technology that permits transactions to be recorded permanently.
- A technology that cryptographically secure the system and chains data in chronological order.
- A technology that remove intermediaries and create trust through the algorithm.

Blockchain was first introduced in the white paper for Bitcoin in 2009 by unknown person named as Satoshi Nakamoto. Currently, blockchain is used my multiple organizations to tackle their problems and provideabetter solution.

### Problems with current system

- Account Hacking
- Internet Frauds
- High Transaction Costs
- High Transaction Time due to intermediaries
- Dependency on Banks

### How Blockchain solves the current problem?

- Security through Cryptography
- Availability through multiple machines
- Low transaction costs
- Remove of central parties and intermediaries.

### Summarizing Blockchain

- It'sadigitized store for information in the form of transactions.
- It is distributed. Thus, nobody controls it.
- Consensus algorithms make sure of the security and immutability.
- Whenanew block is added toablockchain, it is linked to the previous block using a cryptographic hash.
- Data gets recorded in chronological order.
- Everyone present over the network can view the transactions

### BlockChain Definition

A blockchain isadigitized, distributed, consensus-based secure storage of information protected from revision and tampering over the peer-to-peer network.

### Difference between Blockchain and Database

Characteristic | Blockchain          | Database
---------------|---------------------|----------------------------
Authority      | Decentralized       | Centralized
Architecture   | Distributed         | Client-Server Architecture
Data Handling  | Only Read and Write | CRUD operations
Integrity      | Nobody can change   | Alterations are allowed
Transparency   | Built In            | Not Transparent
Trust          | Algorithms          | Owner of the Database

### Function of Intermediaries

- Information Gathering
- Promotion
- Contact
- Negotiation
- Physical Distribution
- Financing
- Risk Analysis

### Introduction to Cryptography

Cryptography is an important aspect when we deal with network security. 'Crypto' means secret or hidden.

### Types of Cryptography

- Symmetric aka Private Key Cryptography
- Asymmetric aka Public Key Cryptography

### Summarising

- This spreadsheet created in the example is calledablock.
- The whole chain of blocks is collectively called as Blockchain. Every node holdsacopy of the Blockchain. Once a block reaches a certain number of approved transactions, then a new block is formed.
- The Bitcoin Blockchain updates itself every ten minutes.
- As soon as the spreadsheet or ledger or registry is updated, it can no longer be changed. Thus, it's impossible to forge it.

Blockchain Accounts-Private Key

- In general once you create an account on Blockchain, you will getaPrivate Key and a public address.
- Private Key is used to generateasignature for each transaction over the blockchain.
- The generated signature is used to confirm that the transaction has come from a specific user, and also prevents the transaction from being altered by any malign entity.
- In simple words-"Private Keys are used to sign the cryptocurrencies you send to others."
- Example: L34EXrFCuxQCorfE66sxQe8Tyh71SyU8cc9z7HnbEWwW8YsgbvTw

Transactions

- Transactions are records of data in chronological order
- Transactions are stored inaMerkle tree inside the Block.
- The transactions, when submitted, are picked up by the blockchain network and is inserted intoa'pool of unconfirmed transactions.' The transaction pool is a collection of all the transactions on that network that have not been confirmed yet.
- Miners on the network select transactions from this pool and add them to their 'block.' Transactions also contain metadata information which can be utilized to store data over the Blockchain.

```[] font-family="Cascadia Code"
transactions of bitcoin -
        +---------------+       +---------------+       +---------------+
        | Transaction   |       | Transaction   |       | Transaction   |
        |+-------------+|       |+-------------+|       |+-------------+|
        ||  Owner 1's  ||       ||  Owner 2's  ||       ||  Owner 3's  ||
        || Public Key  ||       || Public Key  ||       || Public Key  ||
        |+-------+-----+|       |+-------+-----+|       |+-------+-----+|
      --+---+    |   :  |-------+---+    |   :  |-------+---+    |      |
        |   |    |   :  |       |   |    |   :  |       |   |    |      |
        |   +    +   '. |       |   +    +   '. |       |   +    +      |
        |   +----+     '|       |   +----+     '|       |   +----+      |
        |   |Hash|      |'      |   |Hash|      |'      |   |Hash|      |
        |   +----+      | verify|   +----+      | verify|   +----+      |
        |     |         |     '.|     |         |     '.|     |         |
        |     +         |       |+    +         |       |+    +         |
        | +-----------+ |       | +-----------+ |       | +-----------+ |
        | | Owner 0's | |       | | Owner 1's | |       | | Owner 2's | |
        | | Signature | |       | | Signature | |       | | Signature | |
        | +-----------+ |       | +-----------+ |       | +-----------+ |
        |               |       |+              |       |+              |
        +---------------+      .+---------------+      .+---------------+
                         .Sign'                  .Sign'
         +-------------+'        +-------------+'        +-------------+
         |  Owner 1's  |         |  Owner 2's  |         |  Owner 3's  |
         | Private Key |         | Private Key |         | Private Key |
         +-------+-----+         +-------+-----+         +-------+-----+
  ```

### Blocks

- A Block isacontainer data structure which containsaset of confirmed transactions.
- A block could contain different information, andachain of these blocks evolves into a blockchain as long as it links one and the other.
- The blocks are stored on the hard drives of many miners spread across the globe on a peer to peer network.
- In the Bitcoin algorithm,a block is created every 10 minutes. All the transactions happening over the network within 10 minutes interval are crunched into that block and added to the chain.

### Structure of Blocks

All blocks in the Blockchain are composed ofaheader, identifiers andalong list of transactions. The structure ofablock is as follows:

- Block Header
- Block identifiers
- Merkle Trees

Blocks

```[] font-family="Cascadia Code"
      +------------------+      +------------------+      +------------------+
      |    Block 1       |      |     Block 2      |      |     Block 3      |
      |    Header    ----+-+    |     Header   ----+-+    |     Header       |
      |+----------------+|  \   |+----------------+|  \   |+----------------+|
      ||Hash of previous||   -->||Hash of previous||   -->||Hash of previous||
      ||  Block Header  ||      ||  Block Header  ||      ||  Block Header  ||
      |+----------------+|      |+----------------+|      |+----------------+|
      |                  |      |                  |      |                  |
      | +--------------+ |      | +--------------+ |      | +--------------+ |
      | | Markle Root  | |      | | Markle Root  | |      | | Markle Root  | |
      | +-------+------+ |      | +-------+------+ |      | +-------+------+ |
      |         |        |      |         |        |      |         |        |
      +---------+--------+      +---------+--------+      +---------+--------+
                |                         |                         |
         +-------------+           +-------------+           +-------------+
         |   Block 1   |           |   Block 2   |           |   Block 3   |
         | Transaction |           | Transaction |           | Transaction |
         +-------+-----+           +-------+-----+           +-------+-----+
                      simplified Bitcoin block chain
  ```

Example of Bitcoin Block
 Field               | Description                  | Size
---------------------|------------------------------|--------------------------
 Magic No            | value always 0XD9B4BEF9      | 4bytes
 Blocksize           | number of bytes following up to end of block | 4bytes
 Blockheader         | consists of 6 items          | 80 bytes
 Transaction Counter | positive integer VI = Varlnt | 1-9 bytes
 Transactions        | The (non empty) list of transactions | Transaction counter-many transactions

### Block

- Mainnet
- Block Header - Block Height, Previous Block Hash, Size of the Block
- Transaction Counter - 2
- Merkle Root - 3irny3oryn@9yr3yr093r

### Transactions

- Alice sends 1 coin to Bob
- Bob sends 1 coin to Eve

- Block + Nonce 2^67 - Hash of the Block should always have 10 leading zeroes
- Nonce - Blockchain Diff

Merkle Tree

```[] font-family="Cascadia Code"
                    +-------------------------+
                    | Root Hash / Markle Root |
                    +-------------------------+
                                |
             Hash AB -----------------------  Hash CD
               |                                 |
     Hash A ------- Hash B             Hash C -------- Hash D
      /                \               /                 \
Transaction A    Transaction B    Transaction C    Transaction D

in detail -->
                      +------------------------------+
 +----------------+   | +----------------+ +-------+ |   +------------+
 | Previous Block |-->| | PrevBloch Hash | | Nonce | |-->| Next Block |
 +----------------+   | +----------------+ +-------+ |   +------------+
                      | +-------+   +-------------+  |
                      | |  PoW  |   |  Timestamp  |  |
                      | +-------+   +-------------+  |
                      |     +----------------+       |
                      |     |   Fill Field   |       |
                      |     +----------------+       |
                      |     +----------------+       |
                      |     |   Merkle Root  |       |
                      |     +----------------+       |
                      |        |         |           |
                      +--------+---------+-----------+
                               |         |
                           Hash 12      Hash 34
                           |     |      |     |
                          Tx1   Tx2    Tx3   Tx4
  ```

## Consensus Mechanism

### What is Consensus?

- Blockchains are decentralized systems which consist of different participants who act depending on incentives they receive and the information that is available to them.
- When a new transaction gets broadcasted on the network, nodes connected to the network have the option to either include that transaction to their copy of ledger or to ignore it. When the majority of the nodes which comprise the network decide onasingle state, the consensus is achieved.

Let's consider 2 Generals Problem and understand the consensus better.

```[] font-family="Cascadia Code"
      General 1            HIll /^\                General 2
        \__________________________________________/
              _____________________________________/ Not sure
  Not Sure  \______________________________________
  ```

### Byzantine Generals Problem

- A more generalized version of the Two Generals Problem describesagroup of generals agreeing on the time of the attack. Apart from that, one or more generals can be the traitors, meaning that they can lie about their attack choice (e.g., they say that they agree to attack at9am, but instead they do not attack).
- To reachaconsensus here, all the generals must agree on the same decision.
- Let's change the scenario to a Commanding General who issues the attack and all others as who will follow the same to attack.
- If the Commanding General isatraitor, the consensus is still achieved. As a result, all lieutenants take the majority vote over the Default value.
- This implies that the algorithm can reachaconsensus as long as 2/3 of the actors are honest. If the traitors are more than 1/3, the consensus is not reached, the armies do not coordinate their attack, and the enemy wins.

```[] font-family="Cascadia Code"
  Lieutenant is the Traitor
             +------------------------------+
             |        Commander             |
             +------------------------------+
           v /              v |              \ v
+--------------+      +--------------+      +==============+
| Lieutenant 1 |<--v--| Lieutenant 2 |<--x--|:Lieutenant 3:|
+--------------+      +--------------+      +==============+

Commander is the Traitor
             +==============================+
             |::::::::Commander:::::::::::::|
             +==============================+
           x /              y |              \ z
+--------------+      +--------------+      +--------------+
| Lieutenant 1 |<--y--| Lieutenant 2 |--y-->| Lieutenant 3 |
+--------------+      +--------------+      +--------------+
    +   |   |______x______+      +________z_______|  +  |
    |    \____________________x_____________________/   |
     \________________________z________________________/ 
  ```

### Solution

- Take an example; every Lieutenant take 10 mins to convey orders. In other words, 10 minutes are required for communicatingamessage for an attack. Moreover, the passing of messages is inaway where each message is appended to the last message before sending it to the next Lieutenant.
- Example:
  o General-Attack at9am
  o Lieutenant1-Attack at9am, Attack at9am
  o Lieutenant 2- Attack at9am, Attack at9am, Attack at4am
- If the Lieutenant2isatraitor, then the 3rd Lieutenant can verify that the incoming message is not in synchronization.
- Moreover, if Lieutenant 2 decides to change all the previous messages too, then each message would take 10 minutes thus Lieutenant 2 will be working for 30 mins.
- But Lieutenant 3 expects the message to come in 10 minutes, thus again giving in that Lieutenant 2 is a traitor.
- If the commander is a traitor, then he might send different orders to different Lieutenants, which will come into consensus but since the messages don't follow the structure of providing in the same attack time ,the default option of retreat will come to action.

**How does it relate to Blockchain?**

- This is solution which is described with Proof of Work for Bitcoin Blockchain.
- Each block has to follow the formulation guidelines of 10 mins in Bitcoin.
- Each block is appended to the last one by incorporating the Block hash.
- Consensus is achieved once of the actors agree on a block.
- Verification of the Blocks is done by the miners.

---

### Proof of Work

- Proof of Work is the consensus algorithm where miners compete to solve a difficult mathematical problem based onacryptographic hash algorithm.
- Some of the problems included with Proof of Work are:
  - Hash function - how to find the input knowing the output.
  - Integer factorization - how to present a number as a multiplication of two other numbers.
  - Guided tour puzzle protocol - If the server suspects a DoS attack, it requires a calculation of hash functions, for some nodes in a defined order.</br>
  In this case, it's a 'how to find a chain of hash function values' problem.
- Miners receive are ward when they solve the complex mathematical problem.
- For example in Bitcoin miners receive 12.5 bitcoins for solving the puzzle.
- Miners can also receive transaction fees in addition to rewards.

### Proof of Stake

- Proof-of-Work algorithm rewards miners who solve complex mathematical problems with the end goal of validating transactions and creating new blocks. On the other hand, in the Proof-of-Stake algorithm, the creator of a new block is chosen in a deterministic way, depending on its wealth/stake in the blockchain.
- No block reward.
- All the digital currencies are created at the start of the chain, and their number never changes. Miners only take the transaction fees.
- The blocks are validated as per the stake held by the person over the Blockchain.
- Miners/Validators only collect the transaction fees as per the stake.
- There is no complex computation involved that's why they are more efficient then proof of work systems

### How a Blockchain Transaction Works?

- **Step 1** A user creates a transaction from their wallet, attempting to send currency or data to someone else.
- **Step 2** The transaction is put across a 'pool of unconfirmed transactions'. This pool is a collection of unconfirmed transactions that are waiting to be processed by the miners.
- **Step 3** Miners on the blockchain select transactions from these pools and form them into a 'block'.A block is basically a collection of transactions with some extra metadata. Every miner creates their own block. Multiple miners can put in the same transactions in their block.
- **Step 4** Once the block is created, miners generates a block signature. This signature is created by solving a complex mathematical problem. Each block has a different mathematical problem as per the transactions.
- **Step 5** The miner that finds a target signature for its block first, broadcasts this block and the signature to all the other miners.
- **Step 6** Other miners verify the signature If it is valid, the other miners will confirm its validity and agree that the block can be added to the block chain. This process is also termed as consensus.

### Blockchain Projects

The Blockchain ecosystem is currently running with some major projects and more are under pipeline. Some of the major projects on Blockchain are:

- Bitcoin - This project introduced the world to Blockchain.
- Ethereum - This project came with concept of Smart Contracts where two parties adhere to certain rules and create a trust. This opens the world for more decentralized applications.
- Neo - This project positioned itself as the "Chinese Ethereum" but it bought the Python as the main language for the creation of Applications.
- Hyperledger Fabric - This is an enterprise graded project which can be easily programmed as per the enterprise needs. This is a modular project which supports multiple consensus algorithms.

### Blockchain Users

- Blockchain users are normal people like you and me, who make use of the blockchain or cryptocurrency to achieve some results. They can also be investors who buy cryptocurrencies to sell at a later date.
- For creating a Blockchain user base the technology or cryptocurrency should have some utility related to the problem being tackled.

- For Example:
  - Bitcoin serves the major utility of payment for goods and services. Currently there are over 50,000 merchants registered with Bitcoin including-Microsoft, PayPal and Subway. Bitcoin was the first mover in Blockchain and it's high utility as payment system made sure that a large part of its ecosystem is based upon users.

### Blockchain Exchanges

- Every Blockchain project has a robust ecosystem working under it, and it always include a decentralized exchange. These are developed by the Blockchain team or the community of other developers.
- A typical exchange is designed to find the cheapest rates of exchange between any two cryptocurrencies, making it more affordable to trade tokens/cryptocurrencies.
- Exchanges used for trading also might integrate with hardware wallets, or users can create their own wallet on the exchange website.

### Blockchain Verfiers/Miners

- To functionablockchain and maintain its integrity, it needsalarge network of independent nodes around the world to maintain it continuously. In private blockchains,a central organisation has the authority over every node on the network. In the case of public blockchains, on the other hand, anyone can set up their computer to act as a node. The owners of these computers are called miners.
- Since the integrity of the blockchain is directly related to the number of independent nodes on the network, there also needs to be some incentive to mining. Different blockchains utilize different mining systems however most of them contain some form of:
  - An incentive system
  - A consensus algorithm

### Blockchain Developers

- Blockchain technology is built by the potential of developers working behind it.Astrong team of developers can lead toasuccessful Blockchain project. Currently there are two types of developers in the blockchain ecosystem:
  1. Blockchain developers
  2. dApp developers
- Blockchain developers build new blockchains with different levels of functionalities andConsensus Algorithms.
- dApp developers work with decentralized applications that can run on blockchains thus providing a similar functionality like Google Play Store over the Blockchain Technology.
- The development of Smart Contracts over the Blockchain has open possibility for the developers to create extensive applications and use cases for the industries.

### Blockchain Applications

Apart from exchanges, platforms and users, another important aspect of the Blockchain
ecosystem is the applications that industries, developers and communities build to serve a specific purpose.
There are various examples of Applications being build upon Blockchain, some of the major working applications are:

- CryptPad - A decentralized document creation application.
- Humaniq - A fintech startup which connects unbanked people with global economy.
- Augur - A peer to peer oracle and prediction market place.
- Filament - Building the loT applications over the Blockchain.

### Why Industries Need Blockchain ?

### Current Blockchain Implementations

- Pharmaceuticals - DHL worked with Accenture to establishablockchain-based track-and-trace system in six areas worldwide. Currently, the system has 7 billion unique pharmaceutical serial numbers and handling more than 1,500 transactions per second.
- Fashion - CGS has developedasystem for tracking garments and compliances on raw materials for many apparels and fashion clients.
- Cross - Border Payments - IBM has developedanew blockchain banking solution that allows financial institutions to move quickly and cost-effectively process payments globally.
- Food Safety - IBM has partnered up with Dole, Nestlé, and Walmart to set up a blockchain for better regulation of food.
- United Nations - United Nations is currently using Blockchain for 16 agencies including Human Trafficking and World Food Program.
- Jewelry - Brilliant Earth has partnered up with Everledger to use blockchain in tracking and tracing the provenance of diamonds and other gemstones. This will also ensure that they are conflict-free.

### Blockchain Revolution

```[] font-family="Cascadia Code"
  +--------------------+   +------------------+   +----------------------------+
  |   Coins            |   |  Tokens          |   |   DAPPS and Enterprise     |
  +--------------------+   +------------------+   +----------------------------+
  | Cryptocurrencies   |   | Smart Contracts  |   | Decentralized Applications |
  | Payment Services   | + | Smart Properties | = | Supply Chain               |
  | Trade of resolures |   | ICOS             |   | Autonomous Organizations   |
  +--------------------+   +------------------+   +----------------------------+
  ```

### Exciting Disruptions Coming Soon

- Entertainment Industry - Movie Braid was the first movie to be produced by doing an ICO.
- Property Rental - Rentberry aims to address the common pitfalls and headaches of the traditional rental model. Politics-Sierra Leone carried out their elections on Blockchain.
- Education - Socrates Coin is making big moves to change the traditional approach to a "3DInternet".
- Digital Advertising - Basic Attention Token is takingacrack to solve the problems with Digital Advertisements.
- Internet of Things - Walton chain, an award - winning Chinese project that seeks to integrate loT and blockchain technology on an unprecedented scale.

### Industry Challenges for Blockchain Adoption

Energy Consumption

- Some major public Blockchains use Proof-of-Work algorithms.
- PoW involves the use of the computational power ofamachine to solve a complex mathematical puzzle to verify a transaction and add it to a block.
- Current Bitcoin energy consumption is almost equal to the consumption by Ireland.
- By 2020 it's estimated that Bitcoin will utilize more energy consumption than the entire world currently uses.
- A probable solution for this has emerged in the form of different consensus mechanisms like Proof-of-Stake, Delegated-Proof-of-Stake etc.

Scalability

- Scalability has appeared asasignificant issue for the Blockchain networks like Bitcoin and Ethereum.
- Blockchains are having trouble effectively supportingalarge number of users on the network.
- Moreover, the size of public blockchains keeps on increasing. Currently, Bitcoin ledger size is above 100 GB.
- One possible solution which has emerged is storingahash of data over the network.

Public Perception

- Presently, blockchain technology is almost synonymous with Bitcoin.
- The majority of the public is still oblivious to the existence and potential uses of Blockchain technology.
- As Bitcoin is anonymous and is used for shadowy dealings of money laundering, black market trade, and other illegal activities. The blockchain is also getting a bad reputation due to the same.
- Mainstream adoption is needed to remove the sometimes-negative undertones of Bitcoin.

Standards and Regulations

- Blockchains are continuously evolving, but still, countries are skeptic about it as there is no proper definition for standards and regulations.
- Enterprises and Governments require regulations to protect their customers.
- To tackle this problem, certain countries are trying to launch their regulations over the technology.
- Mass adoption might also standardize the Blockchain.

## Blockchain Examples

### Walmart Food Tracking

**Challenge**: It can take upto days weeks to track the source for an outbreak of a food-borne disease.

**Benefit**: Better trace a bility could help save lives by allowing companies to act faster and protect the livelihoods of farmers by only discarding produce from the affected farms.

**Approach**: Walmart createdafood traceability system based on Hyperledger Fabric. Walmart, together with IBM, ran two POCS to test the system. First one for tracing mangos sold in Walmart US stores and the other one to trace pork sold in its China stores. The tracing improved from 7 days to 2.2 seconds.

### Honeywell Marketplace

**Challenge**: To cut purchasing time for aerospace products from days or weeks down to seconds. Also, to connect each physical part to its digital equivalent.

**Benefit**: Purchased time reduced from days to minutes and boost to anti-counterfeit measures.

**Approach**: Honeywell created an online marketplace system based on Hyperledger Fabric.
Tracking of new and old parts for aircrafts is done with the same. Also, it createdatrust system due to cryptography as most purchases happened using bonds. Any seller can launch his/her own selling system for aircraft parts using Honeywell solution known as Go Direct.

---

1. Which best describes an asset that can be stored on a blockchain?
</br>-> Anything of value to a participant in a business network

2. What is a ledger?
</br>-> A system of record that logs the inputs and outputs of a business

3. What qualities of service does blockchain give to a business network?
</br>-> Consensus, provenance, immutability, and finality

4. Which of the following best describes a blockchain network for trusted identity?
</br>-> A decentralized approach that establishes trust and puts the end user in control

5. When designing and building a solution like TradeLens or IBM Food Trust it is important that ...
</br>-> all participants in the ecosystem gain benefit from using the platform

6. Who would often be considered a key stakeholder when implementing a blockchain for business?
</br>-> Regulators

7. What does Bitcoin have in common with blockchain for business?
</br>-> They both provide cryptographic proof that transactions happened

8. Hyperledger Fabric emphasizes which features?
</br>-> Smart contracts, consensus, confidentiality and scalability

9. Where can IBM Blockchain Platform networks be deployed?
</br>-> Across multiple cloud and on-premises infrastructures, including different vendors' clouds

10. What is the IBM Blockchain Platform?
</br>-> A set of tools for building, operating a growing a blockchain network.

11. Which of the following fact(s) about business networks is/are true?
</br>-> all of the facts are true

12. Which of the following best describes the Hyperledger project?
</br>-> All of these facts are true

13. What does the “provenance” quality of service provide to blockchain?
</br>-> History of transactions

14. Which of the following facts about assets is true?
</br>-> Assets are anything that is capable of being owned or controlled to produce value

15. Which of the following is the primary benefit of TradeLens?
</br>-> TradeLens provides end-to-end traceability of food in the supply chain
