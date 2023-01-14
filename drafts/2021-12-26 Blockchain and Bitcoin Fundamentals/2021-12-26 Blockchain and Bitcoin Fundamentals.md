# Blockchain and Bitcoin Fundamentals

# Section 1 intro
# Section 2 Blockchain and bitcoin fundamentals
## What is a blockchain
permanent verifiable and unchangeable


A blockchain is a ledger that keeps a record of transactions.

Definition: a permanent record of all the transactions that have taken place, in a secure chronological and immutable
* Ledger
* Constantly growing: 200GB as of the video
* Permanent record of all transactions
    - can be explored using a block explorer
* Secure
* chronological
* immutable


## what is bitcoin

 A bitcoin is a type of digital asset that can be bought, sold or transferred securely over the Internet.

New asset, no middle man, secured

middleman is needed to verify the transactions

The problem: Double spending by copy pasting money

Double spending is one of the key problems with sending money over the Internet and why there has traditionally been a need for third parties such as banks and other institutions. Bitcoin solves this issue.


Bitcoin network uses blockchain to 

Decentralized vs centralized: no single point of failure comparing to traditional


## The role of bitcoin miners

Miners: process and confirm transactions

powerful bitcoin mining computers by solving math problems and cryptography problems

Miners are rewarded in bitcoin

bit coin is created by mining

### How the bitcoin blockchain is built

Role of the miner is to build the blockchain of records that form the bigcoin ledger.

Miners are in competetion of building these blocks

About 1 block every 10 minutes, and these blocks form a chain. 

## Demo: Hash Functions


https://demoblockchain.org/hash

SHA256 Hash

SHA-256 is a type of cryptographic hash function which is used in Bitcoin.


SHA: Secure Hash Algorithm, developed by NSA.

Used in bitcoin.

* always can generate a hash from any data, and it's the same
* one way function


not encryption, you can decrypt w
Hash is one way

Think of it as a digest

## Demo: Block hashes

https://demoblockchain.org/block

Miners

Hash need to have four leading 0s to be a valid.

Nonce is used to make a block to have a valid Hash with 0000.

Mining is the process of finding the Nonce. 

Hash is computed with combination of
* Block number
* Nounce: A nonce is a number that is used only once as part of the mining process in Bitcoin.
* Data

(Nonces are used in proof-of-work systems to vary the input to a cryptographic hash function so as to obtain a hash for a certain input that fulfils certain arbitrary conditions. In doing so, it becomes far more difficult to create a "desirable" hash than to verify it, shifting the burden of work onto one side of a transaction or system.)[https://en.wikipedia.org/wiki/Cryptographic_nonce]

## How block hashes work in a blockchain
https://demoblockchain.org/blockchain

Each block has
* Block #
* Nonce
* Data
* Prev: previous hash
* Hash


Every block in the blockchain is cryptographically tied.

Chaning any thing from any block, the chain will break. 

Like a dominal


4 leading 0 is related to **difficulty level**. How difficult 


"In this case, the difficulty level requires us to have a hash that is smaller than what we have in the target. And for this specific purpose, we would need a target that has at least four leading zeros. Now the difficulty level keeps increasing over time as new computers are added in, more cryptographic hashing is added to the Bitcoin network. So more hashing power means that the difficulty level needs to go up. And that difficulty level is adjusted every two weeks to make sure that the computers that are actually competing to try to solve these cryptographic problems take approximately a total of 10 minutes to mine a new block."

If someone want to change a block, they need to mine all the blocks after it
???? What
## Demo How a distributed blockchain works
https://demoblockchain.org/distributed


Copies of the block chains distributed all over the world

Miner that breaks the block chain will not affect the network. and will be ignored


## The four components of Bitcoin

software uses cryptography, runs on a network of hardwares

* Software
* Cryptography
* Hardware: the network of miners
* Gaming theory


TODO: how this works?
2:30

Proof of work: the validation of finding nounce

## The coinbase transaction

Block explorer: https://btc.com/en/btc


Every single block has a Coinbase transaction, that's where the miner gets rewarded. 

The miner receives
* the rewarded bitcoin
* All the transaction fee



## Virtual field trip: the bitcoin blockchain at work

https://www.blockchain.com/explorer
https://btc.com/en/btc

The genesis block: https://www.blockchain.com/btc/block/0

Bitcoin is a public blockchain, thus we can explore

Bitcoin price could vary in different exchanges

Hash rate: the processing power of miners

Higher hashrate has more probability to mine new blocks


https://www.blockchain.com/charts

Mempool: the number of transactions yet to be confirmed


Live update list of all the new transactions coming into bitcoin network.
https://www.blockchain.com/btc/unconfirmed-transactions

Use explorer to check specific transaction by searching transaction number.




## Key Concepts in Bitcoin

Sending Money over the internet: Need 3rd party(bank, paypal, credit card...) to avoid double spending. 3rd party 
* controls the transaction
* Keeps record of transaction
* centralized

Bitcoin transfer of value: Peer-to-peer

Four key concepts of bitcoin
* Disintermediated: the act of removing the middle man
    - middle man means unnecessary cost
* Distributed: the work is shared, reliable, no single point of failure
* Decentralized: no central control, no central point of failure, no goverment that regulate bitcoin
* Trustless: no need for a third party, the blockchain network make it trust-able
**distributed trustless concensus**: all nodes agree a transaction took place





## The birth of Bitcoin
### Birth
2008 financial crisis

Oct 2008 published white paper on bitcoin

### Early attempt at electronic cash
1976 MDL: Mutual Distributed ledgers
1983...



## The value of block chain

Internet was created as an open network for sharing information

Blockchain supports 3 key areas: on top of what internect offers
* **Value**: enables a unique asset to be transferred over the internet without a middle centralized agent
    - unique ness of digital asset, instead of copiable things like mp3
* **Trust**: creates a permanent, secure and unalterable record of who owns what. Using advance cryptography "Information integrity" is preserved
* **Reliability**: Decentralized network structure ensures there is no single point of failure


## The value of Block chain: Cryptocurrency
Cryptocurrency is a type of digital asset which can be used to exchange value between parties. It uses cryptography to secure how it's transferred and to control the creation of new units of that currency.


* not like fiat currency: can be printed by goverment. Bitcoin is created by miners


Other cryptocurrency
* litecoin: instead of wait 10mins, it does it in 2.5min, lower market cap
* Z-cash: more anonymous
* Monero: more anonymous
* Dash: digital cash?



## The value of block chain: Digital Tokens
aka, blockchain tokens
* transfer digital asset peer-to-peer. it's a piece of digital information
* recorded on blockchain
* Permanent and immutable
* distributed
* secured using cryptography 

Colored coin: adding additional information onto transaction, and can represent a physical 


### Digital token
A more useful concept is a digital token: A digital token is a digital asset that can represent anything. Some example include securities, loyalty points and real world assets

Digital token is also a type of crypto currency

Example:
* Audiocoin: cryptocurrency for music industry, buying CD contains audiocoin
* Golem: shared economy computing power. A way of outsourcing computing power
* Vechain: track supply chains on blockchain: track the path from raw material to end product 
* Steemit: rewards platform for content publisher. 
* CryptoKitties - Collect and breed digital cats


### Initial Coin Offering/Initial Token offerings
6 Billion in 2017 raised - new 







## The value of block chain: Smart Contracts
Cryptocurrency is only one application of blockchain. There is smart contracts. 


**"Disintermediated, Automated, Self-Executing and Immutable."**
* Disintermediation - no middleman
* automation: contract executed by software
* self executing and immutable





## The value of block chain: The birth of Smart Contracts

Nick Szabo - 1994

"A smart contract is a computerized transaction protocol that executes the terms of a contract. The general objectives are to satisfy common contractual conditions such as payment terms, liens, confidentiality and even enforcement, minimize exceptions both malicious and accidental, and minimize the need for trusted Intermediaries. Related economic goals include lowering fraud loss arbitrations and enforcement costs and other transaction costs."


## The value of block chain: DAOs and DACs

DAO: Decentralized Autonomous Organization (DAO)
DAC: Decentralized Autonomous Corporation (DAC)

A revolution concept

DAO is built on smart contracts, smart contracts are: "Disintermediated, Automated, Self-Executing and Immutable."
* A collection of agreements, smart contracts
* Distributed network on a blockchain: it's a network, 
* IoT: bots and human doesn't make a difference in the DAO

## Business use cases of blockchain beyond bitcoin
lectures publications:
* https://twitter.com/georgelevy
* https://www.youtube.com/GeorgeLevy
5 examples of real business cases
### Supply chain management - walmart
* Partnership with IBM

### Australian banks ANZ and Westpac
* partnership with IBM

### Insurance - Maersk
Partnership with Microsoft

Audit insurance shipping


### DNV

Partnership with deloitt

Improve tampering and reduce fraud

### UN uses Ethereum to aid refugees
Increase transparency, reduce fraud, lower intermediary cost

## Limitations of Blockchain technology
* Early stage, not many successful POC
* Lack of awareness
* Limited available technical talent
* it is immutable: no reversals or modifications
* Key Management: lose access to private keys
* Scalability: Bitcoin can't handle large scale volumn, 
* Time to process: 10 mins for bitcoin. Banks handles transactions in miliseconds. 

## Common Misconceptions about blockchain and bitcoin
* Bitcoin is Anonymous.
    - X, no it's public. Like a cover name for an artist.
    - Pseudononymous
* Bitcoin is used to launder money.
    - X, no not bitcoin
    - 
* Blockchain is a better type of database.
    - X, it's a ledger, not DB
    - chronological, and immutable
* Blockchain is bitcoin
    - X
* You need to buy a full bitcoin

## What is bitcoin cash?

* New cryptocurrency developed from a "Hard fork" in the bitcoin blockchain
* increases block size to 8mb from 1 mb limit
* No segwit

BitcoinCash.org
blockdozer.com
blockchare.com

### Hard fork: 2017 Aug 1
A block of 1.9MB causes a split of the chain of Bitcoin blockchain, this is a fork

Bitcoin cash are distributed for each bitcoin before this point. 

BCH

## On forks, transactions, segregated witness(SegWit)

### What is a fork?

A blockchain splits into two different paths forward

**Hard fork**: Introduces a change that forcs everyone to upgrade
**Soft fork**: Introduces change that is backward compatible, no upgrade needed

* Forks happen on regular basis
* Two or more miners solve a block at the same time - for a while there are extra chains
* Eventually one of the chains wins over the other
* Orphan block is the one of the blocks that are has lost
* Back to mempool: transactions in orphan block are returned to mempool

### Hard fork: bitcoin cash
UAHF: User activated Hard Fork
Caused a split in chain
* for those doesn't upgrade, they remain with bitcoin
* THose upgrade get bitcoin cash
### Soft fork: bitcoin w/ Segwit
UASF: User activated soft fork

Locked in at Aug 8th 2017 at block #479,707
Activated on Aug 24th of 2017 at #481824

Replaces block size limit with block weight limit

### What is Segwit
* Protocal upgrade: improves scalability without increasing block size
* Addresses a vulneralbility:  transaction malleability
* Does not require upgrading to remain on blockchain
* Did not split the chain

3 Main components of a bitcoin transaction
* Input
* Amount
* Output

Digital signature is needed for transaction. Signed with private key.

In a segwit transaction, singature data is "segregated" to an etended block, frees up 60~63% of the data size. 

Input and amount are also included as part of digital signature in the extended block.

## How many transactions are there in a block?

Bitcoin blockchain as

* Limited by how many transactions fit within the maximum "block weight"
* Current block weight limit is 4 million "Weight unites"
    - block size(before segwit) used to be 1MB
* Block weight is measured in bytes
* Transaction fees are also set based on the number of bytes in a transaction
* Miners try to maximize their profits by getting as many high fee transactions as will fit
* It is possible to have a block with onely 1 transaction, the coinbase transaction
* It is much more common to have many more transactions in a block

Visualization: https://txstreet.com/



## The controlled Supply of Bitcoin

The limit: 21 million

Started with 50 bitcoins for the first transaction, now 2021 the reward is 6.25. It halves every 210,000 blocks. about every for years.

50->25 -> 12.5 (July 2016) -> 6.25 (May 11, 2020) 900/day ...

The limit of halving is a Satoshi, 100million Satoshi in a bitcoin

This will be 2140.



## On the future of bitcoin mining
When there's no more bitcoins to be mined. Miners are compensated by transaction fee.

as more and more people use bitcoin, there will be more and
 more transaction, thus more fee

## Important Dates in bitcoin history
October 31st 2008 - The white paper
Jan 3rd 2009 Genesis block
May 22nd 2010 First retail purchase: 1 BTC = 0.0025
Nov 28th 2013: 1000USD
Mar 2nd 2017 past 1 oz of gold

## On merkle tree
A merkle tree is a mathematical data structure composed of hashes of different blocks of data and which serves as a summary of all the transactions in a block

* A.K.A. Hash tree
* named after Ralph Merkle
* it is possible to create a blockchain without a Merkle Tree

Merkle root: summary of all transactions in the block

Binary tree
transactions are on the leaves, on each level, parent's hash is the concatenation of children hashes.

Merkle root's hash is generated from all the transactions on a block, and merkle root is part of the block that is used to generate the block's hash. 
* merkle root's hash is consistent with all transactions, any change to any of then would break consistency
* block's hash is consistent with merkle root, any change to merkle root, would break the consistency

## quiz
Bitcoin is not anonymous, it is instead pseudonymous.

To send bitcoin over the Internet to someone else, you do not need the services of a bank. You simply send money directly to the other person and it will arrive securely and almost instantly.

Nick Szabo is regarded as the father of smart contracts for having written about and used the term "smart contracts" as far back as early as 1994

There will be a maximum number of 21 million bitcoins available. This number will be reached in the year 2140.

The Merkle Root in a Bitcoin transaction block is a single hash that presents a summary of all the transactions in that block.

## additional fun ways of looking at bitcoin at work
* blockchain.com/explorer
* bicoin-vr.github.io
* fiatleak.com
* realtimebitcoin.info
* blocks.wizb.it
* billfodl.com/pages/bitbonkers
bitlisten.com


# Section 3: Getting started with Bitcoin

## getting started with bitcoin
* transaction is irreversible
Steps
* learn about bitcoin
* choose your wallet
* get an address
* public and private keys
get bitcoins
spend bitcoins

## Choose your bitcoin wallet
bitcoin.org

https://bitcoin.org/en/choose-your-wallet

Hardware: most secure
Web
Mobile
Desktop

start with one wallet, gradually get into it. maybe start with a web one

keep a controllable amount on hot storage, rest on cold storage, to keep safe. 


## sending and receiving bitcoins
Public key and private key

private key to authorize transactions

Bitcoin address is generated from public key
Generate bitcoin address often so it's less easy for people to track, thus, safer

Bitcoin address: 26 to 35 alpha-numeric, begin with number 1 or 3, ending with h
Share bitcoin address, or QR code. 


## Store your bitcoins safely
1. make sure your devices are clean and virus-free
2. use firewalls
3. avoid public wifi
4. Use VPN

Hot storage vs cold storage
Hot storage:
* connected to internet
* easy and convernient
* Vulnerable to hackers
* Keep small amounts

Cold storage
* store **keys** offline
* Brain wallet: a passphrase -> generate a wallet online with the word
* paper wallet: safe, but vulnerable. paper can be destroyed
* USB drive: vulnerable
* hardware wallet: recommended

### Final thoughts
Never reveal your private keys
keep most cryptocurrency cold
make backups



### resources
* https://coinsutra.com/cold-storage-cryptocurrency/
* https://coinsutra.com/bitcoin-hard-fork-dos-and-donts/
* https://youtu.be/9fFDuJj459Q
* https://cryptocurrencyfacts.com/using-two-factor-authentication-in-cryptocurrency/

## Converting your bitcoins to Fiat currency

* use a crypto Exchange
    * coinbase
    * kraken
    * gemini
    * bitstamp
* bitcoin debit card
    - coinbase visa
    - bitwala
* sell them to someone else. Note transactions are irreversible
* Local trading site
    - localbitcoins.comc
* Bitcoin ATM, Bitcoin Teller Machine


# Section 4: Review and Free Resources
## Course review and valuable free resources


## Bonus Lecture

