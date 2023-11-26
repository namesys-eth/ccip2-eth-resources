# [NameSys](https://namesys.xyz)

![](https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/png/banner.png)

> Draft may undergo minor edits until December 1, 2023

### NAME AND WEBSITE:

`namesys.eth` ([`namesys.eth.limo`](https://namesys.eth.limo) | [`namesys.xyz`](https://namesys.xyz))

### POINT OF CONTACT:

`dev.namesys.eth` (== `sshmatrix.eth`)

### WHAT DO YOU WANT TO BUILD ON ENS?

NameSys is a Research & Development Cooperative dedicated to creating cost-efficient, open-source and accessible cryptonative products, helping scale ENS adoption through immediate and tangible benefits to end users. High gas fees have been a burden on the accessibility of Ethereum and ENS for a while now. NameSys attempts to resolve these gas issues by developing secure off-chain infrastructures that can replace some of the on-chain functionailties of ENS domains, in particular the Resolver. This on-chain to off-chain offloading has massive impact on the overall gas overhead for managing and truly utilising an ENS name. [CCIP-Read](https://eips.ethereum.org/EIPS/eip-3668) (EIP-3668) and [ENS Wildcard Resolution](https://docs.ens.domains/ens-improvement-proposals/ensip-10-wildcard-resolution) (ENSIP-10) form the backbone of most of the NameSys infrastructure.

The on-chain to off-chain offloading of the Resolver has several beneficial features other than the cost efficiency. For instance, no-cost dynamic off-chain content can now be injected in ENS Records to replace the static and expensive on-chain content. This feature is most impactful in the [ENS Contenthash Field](https://docs.ens.domains/ens-improvement-proposals/ensip-7-contenthash-field) (ENSIP-07) responsible for decentralised web content. NameSys infrastructure makes it possible to render dynamic web-content in Contenthash at zero cost! This development has the potential to drastically expand the usecases emerging from ENS Contenthash.

Our approximate projected development path consists of the following throughout 2024:

#### CORE INFRASTRUCTURE

- **`NameSys.eth` :** ENS Off-Chain Records Manager
   
   Off-Chain Records are NameSys's core premise. NameSys's Record Manager infrastructure (including the on-chain Resolver) could be much more efficient and upgradeable than its current form. In particular, work is well underway for a permanent migration to Universal `v2` Resolver employing carbon-wrapping (EIP-2535) and proxying for upgradeability. 

- **`dAppSys.eth` :** dApp Store for ENS Domains 

   NameSys's Off-Chain infrastructure can be bootstrapped to provide a dApp Store-like feature where users can 'install' a dApp by posting a signed ENS Record, and then access the installed dApp at `dapp.domain.eth`.

- **`notAPI.eth` :** Serverless GET-Only JSON API using ENS Wildcard Resolution & On-Chain Data. 

   Work [is in progress](https://github.com/namesys-eth/notapi-eth) on a fully on-chain API (a contract) that returns JSON responses to queries formatted as subdomains, e.g. `https://erc20.dai.balanceof.<0xaddress>.notapi.eth.limo` shall return the DAI (ERC20) balance of an arbitrary `<0xaddress>`.

- **`htmx3.eth` :** On-Chain HTMX Generator using ENS Wildcard Resolution and On-Chain Data.

   HTMX Generator contract forms the infrastructural core to rendering dynamic dwebsite content in ENS Contanthash in `data:uri` format using only on-chain data.

- **`namesys.js` :** Open-Source Library for implementing NameSys Infrastructure. 

   End-to-end library to simplify native integration of NameSys infrastructure into marketplace clients, registrars and domain managers.

#### IPFS + ENS SERVICES
- **`ipns.eth` :** Public free-to-use IPFS + IPNS Hosting, Publishing and Pinning Service with Keyless Record Management for ENS Domains. This service will be developed with the ability to sync to IPFS Network and/or L2 Events or Data.

![](https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/png/infraStack.png)

#### OTHER SIDE PROJECTS
- ENS + Bitcoin Lightning Compatibility
- IPLD Integration in ENS Contenthash and other relevant fields

#### †FUTURISTIC STUFF
- ZK Proofs as ENS Records
- Off-Chain 2PC and MPC using ENS
- ENS + Secure NFC Hardware Stack for RWA

> † not covered by this stream

### PAST EXPERIENCE WORKING ON ENS
The team behind NameSys has been part of the Ethereum & ENS ecosystem for several years, and have already built useful infrastructure benefitting ENS, Ethereum and in some cases even generic crypto users. While NameSys is mostly known for its Off-Chain Records infrastructure, the team behind it has created an array of protocols and products in the past. Here goes:

#### `NameSys.eth` Stack
ENS Off-Chain Records Manager stack (Web Client + Support Services) with support for web3 IPFS and traditional web2 server for storage. Web Client can be accessed [here](https://namesys.xyz).

#### `CCIP2.eth` Resolver
Gasless [Resolver for Off-Chain Records](https://etherscan.io/address/0x839b3b540a9572448fd1b2335e0eb09ac1a02885) which functions adjacent to the Web Client 

#### `DOSTR.eth` Adaptor
[Dostr](https://dostr.xyz) is an ENS-aware Ethereum Adaptor for Nostr Network which allows Nostr to function with Ethereum wallets. At its heart lies a [seamless key generation algorithm](https://github.com/dostr-eth/nips/blob/ethkeygen/111.md) that interfaces the Bitcoin-native Schnorr Signature scheme and the Ethereum-native `secp256k1` scheme.

#### `IPFS2.eth` Gateway
Web3 IPFS Gateway [`IPFS2.eth.limo`](https://ipfs2.eth.limo) that uses ENS Wildcard Resolution (ENSIP-10) to resolve IPFS, IPNS or IPLD content.

#### `isTest.eth` Bridge
Testnet-to-Mainnet [Resolver](https://etherscan.io/address/0x0Db7E56BFE3cbCD7B952F750c303CbF809585C6b#code) (or vice-versa) for ENS Contenthash. Simply render your Testnet (Goerli) Contenthash for `domain.eth` on Mainnet as a subdomain `domain.istest.eth`

#### `Helix2.eth` Abstraction
ENS-compatible [Link Service Protocol](https://github.com/helix-coupler/resources/blob/master/yellow-paper/helix2.pdf) that allows for multi-party linking in configurable spaces.

#### `ed25519-keygen/ipns` Library
Contributed IPNS `base36` CID Support in [`paulmillr/ed25519-keygen`](https://github.com/paulmillr/ed25519-keygen/pull/10) library

### SIZE OF TEAM AND COMMITMENT
- Two Full-time Cryptographers & Engineers (`sshmatrix.eth` & `freetib.eth`)
- One Social & Public Relations Manager
- †One Frontend Web Developer
- †One Backend & SRE Developer
- †One Media Developer & Designer

> † to be hired when or if funds are available

### FURTHER INFORMATION AND LINKS:

**GITHUB:** [`github.com/namesys-eth`](https://github.com/namesys-eth)

**TWITTER/X:** [`x.com/namesys_eth`](https://x.com/namesys_eth)

### CONFLICT OF INTEREST STATEMENT:
- NameSys received `$10,000 USD` through a systematic grant from ENS DAO Ecosystem WG
- NameSys received `0.7 ETH` through Small Grants Ecosystem WG Round 10

### 10k ENDORSEMENT LINK:
[`https://snapshot.org/#/nominations.ens.eth/proposal/0x64fbc81a7ab8b57deea798df03141fa1b7d1f2fce6f1051b580e568ca89e8070`](https://snapshot.org/#/nominations.ens.eth/proposal/0x64fbc81a7ab8b57deea798df03141fa1b7d1f2fce6f1051b580e568ca89e8070)

### BUGDET REQUESTED:
Minimum ticksize `$100,000 USD`

### DISCLAIMER:
Open grants are the sole source of revenue for NameSys and all related or unrelated development work.