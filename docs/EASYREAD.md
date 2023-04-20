### Project Name

CCIP2.eth: Off-chain ENS Records Manager

### Project Website

Web3 Client: https://ccip2.eth.limo

- Demo Client: https://namesys-eth.github.io/ccip2-eth-client/

### Project Logo

![](https://raw.githubusercontent.com/namesys-eth/ccip2-resources/main/graphics/png/logo.png)

### Project Banner

![](https://raw.githubusercontent.com/namesys-eth/ccip2-resources/main/graphics/png/banner-dark.png)

### Project Description

The usage of ENS records seems to have pleatued despite their enormous potential tp provide a decentralised web3 identity. This is a consequence of high gas costs associated with adding and updating the records on the blockchain. Currently, it costs more to set a text record than an entire year's registration for a 5-character ENS name. While IPNS has reduced the gas costs associated with updating `contenthash`, other records appear to either be unset or rarely updated once set.

CCIP2.eth Off-chain Records Manager solves the problem by storing the ENS records off-chain on IPFS and linking them with user's on-chain IPNS contenthash. Records stored under IPNS are then resolved by [ENSIP-10 `CCIP-Read`](https://docs.ens.domains/ens-improvement-proposals/ensip-10-wildcard-resolution) implementation of [CCIP2.eth Resolver](https://github.com/namesys-eth/ccip2-eth-resolver). CCIP2.eth doesn't require any additional web2 gateways to resolve ENS records, and the user is fully in control of their data storage. CCIP2.eth enables record updates as often as possible at zero cost and allow for cool features such as dynamic avatars. CCIP2.eth is especially secure since user's IPNS private key is handled client-side and doesn't need to be shared with any third-party pin provider. This is made possible by [NIP-111](https://github.com/dostr-eth/nips/blob/ethkeygen/111.md)-like deterministic key generation from Ethereum wallet signatures.

![](https://raw.githubusercontent.com/namesys-eth/ccip2-resources/main/graphics/png/ccip2.png)

We believe that CCIP2 will enable frequent updates of records other than the web `contenthash` and propel ENS adoption as an identity layer.
