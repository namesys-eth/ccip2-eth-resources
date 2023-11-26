# [NameSys](https://namesys.xyz)

![](https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/png/banner.png)
&nbsp;

[NameSys.eth](https://namesys.xyz) is introducing an innovative solution for Ethereum Name Service (ENS) users to store their ENS records off-chain in a **gasless**, **secure** and **autonomous** manner. By combining IPNS and CCIP-Read, NameSys allows users to enjoy free and secure ENS record updates. This unique approach addresses the long-standing issue of high gas costs associated with on-chain updates, making it accessible to ENS enthusiasts of all levels. NameSys is also accessible via faster HTTP gateways for users who prefer speed over decentralised security of IPFS. Due to its gasless nature, NameSys allows builders to develop features previously thought impossible or unfeasible. One of these features is the no-cost & no-logs **private/stealth payments to ENS domains** via NameSys!

The NameSys infrastructure uses a custom resolver called [CCIP2](https://etherscan.io/address/0x839B3B540A9572448FD1B2335e0EB09Ac1A02885#code), which is capable of reading off-chain records from IPFS/IPNS or any other HTTP gateway. Since hosting sensitive records on centralised servers poses significant trust concerns, NameSys designed a non-custodial and secure solution for IPNS record storage. Users can securely generate IPNS keypairs using deterministic wallet signatures. The IPNS private key is used to host off-chain records without sharing it with any third-party service, ensuring data integrity.

&nbsp;
![](https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/extra/graphic.png)
&nbsp;

The NameSys process involves a one-time initial setup, where users set their resolver to CCIP2 and optionally establish their parent IPNS contenthash (or HTTP gateway) on-chain. This contenthash serves as a container for the typical ENS records. With each record update, users regenerate their IPNS keys and sign the data with their unique signatures; this ensures that their **records cannot be tampered with**, even in the event of IPNS key compromise. The records are then pinned to the IPNS public key using the w3name API. Subsequent IPNS key regenerations require the user's signature and secret password, offering a robust and secure hands-off key management.

Users additionally have the option to export their IPNS private key and IPFS hash for re-use with other pinning services such as Pinata, Fleek etc. Users at their own discretion may also choose the HTTP gateway option which eliminates the need for IPFS altogether. NameSys platform's exciting features, such as stealth payments and programmable addresses, open up new possibilities for users. With add-ons such as wallet-specific records and on-chain signers for extra security, NameSys infrastructure is near **zero-cost** and yet **highly secure**.

Overall, NameSys.eth provides a game-changing solution for ENS users, enabling **free and secure off-chain record management**. With its focus on security, autonomy and dynamic possibilities, NameSys aims to transform the ENS community's experience, making free and secure records forever accessible to all users!

# Recent Developments

## `w3name` by NameSys
NameSys will undergo a minor version bump from `v1.1-beta` to `v1.2` in December 2023! In this upgrade, NameSys will deploy its own ENS-dedicated `w3name` API and IPNS Publishing Service to Cloudflare and integrate it with the NameSys Client. This upgrade is under final testing and is expected to come online by December 10, 2023.

## `dAppSys.eth` : dApp Store for ENS Domains 
NameSys's Off-Chain infrastructure can be bootstrapped to provide a dApp Store-like feature where users can 'install' a dApp by posting a signed ENS Record, and then access the installed dApp at `dapp.domain.eth`. On-chain codebase for this feature is already deployed in [`CCIP2.eth` `v1`](https://etherscan.io/address/0x839b3b540a9572448fd1b2335e0eb09ac1a02885). Development work is underway to implement this feature in NameSys Client.

## `notAPI.eth` : Web3 On-Chain JSON API 
Work [is in progress](https://github.com/namesys-eth/notapi-eth) on a Serverless GET-Only API using ENS Wildcard Resolution that returns JSON responses to queries formatted as subdomains, e.g. `https://erc20.dai.balanceof.<0xaddress>.notapi.eth.limo` shall return the DAI (ERC20) balance of an arbitrary `<0xaddress>`.

## We at [NameSys](https://namesys.xyz) are dedicated to proactively adding more utility to ENS domains and transform it into a barrier-free global Layer 1 namespace!