### Project Name

CCIP2: Off-chain ENS Records Manager

### Project Website

Web3 Client: https://ccip2.eth.limo

- Demo Client: https://namesys-eth.github.io/ccip2-eth-client/

### Project Logo

![](https://raw.githubusercontent.com/namesys-eth/ccip2-resources/main/graphics/png/logo.png)

### Project Banner

![](https://raw.githubusercontent.com/namesys-eth/ccip2-resources/main/graphics/png/1500x500.png)

### Project Description

ENS has the potential to revolutionise decentralised access to the web with an attached identity system through linked records, but the usage of ENS records seems to have pleatued. This is a consequence of intrinsically high gas costs associated with adding and updating the records since there are no additional fees to set records. While IPNS has reduced the gas costs associated with updating `contenthash`, other records appear to either be unset or rarely updated once set.

CCIP2 Off-chain Records Manager solves the aforementioned problem of high gas costs by storing the ENS records off-chain on IPFS and linking them with user's on-chain IPNS contenthash. Records stored under under IPNS can then be queried through [ENSIP-10 `CCIP-Read`](https://docs.ens.domains/ens-improvement-proposals/ensip-10-wildcard-resolution) implemented in [CCIP2 Resolver](https://github.com/namesys-eth/ccip2-eth-resolver). The CCIP2 implementation doesn't require any additional gateways to fetch and render the ENS records, and the user is fully in control of their records, e.g. hosting the records on IPFS and linking the IPFS hash to their IPNS key. With this method, users are able to update their records as often as possible at no cost whatsoever without ever losing custody of their data (see figure below). The IPNS private keys for the users' contenthash are handled client-side and don't need to be shared with any third-party whatsoever; this is made possible through [NIP-111](https://github.com/dostr-eth/nips/blob/ethkeygen/111.md)-like deterministic key generation from wallet signatures. We believe that CCIP2 will enable frequent updates of records other than the `contenthash` and propel ENS adoption as an identity layer.

![](https://raw.githubusercontent.com/namesys-eth/ccip2-resources/main/graphics/png/banner.png)
