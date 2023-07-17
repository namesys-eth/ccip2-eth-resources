![](https://raw.githubusercontent.com/namesys-eth/ccip2-resources/main/graphics/png/banner-dark.png)

# [NameSys.eth](https://namesys.eth.limo): Off-chain ENS Records Manager

### ⚙️&nbsp; CLIENTS

| Release | Link-1 | Link-2 |
| -------- | -------- | -------- |
| **Beta-0.9** | [`https://ccip2.eth.limo`](https://ccip2.eth.limo) | [`https://namesys.eth.limo`](https://namesys.eth.limo) |
| **v1.0** | `Coming Soon` | - |

### 📊&nbsp; RESOLVERS

| Network | Contract |
| -------- | -------- |
| 🧪 **Goerli** | [`0xd23aa5545350cdb4eb6bf705d1fe8b75c99500a8`](https://goerli.etherscan.io/address/0xd23aa5545350cdb4eb6bf705d1fe8b75c99500a8#code) |
| 🧬 **Mainnet** | `Coming Soon` |

### 💿&nbsp; CODEBASE

- GitHub: [`github.com/namesys-eth`](https://github.com/namesys-eth)

## 🧬&nbsp; About `NameSys`

[NameSys](https://namesys.eth.limo) is an **off-chain ENS records manager** which allows users to host their ENS records off-chain on IPNS in an autonomous and gasless fashion. The off-chain records are resolved using `CCIP-Read` by a custom resolver capable of reading records from IPNS. The resulting implementation is **secure**, **free** and **infinitely ungradeable**. The NameSys stack broadly comprises of two parts:

- [**CCIP2.eth**](https://github.com/namesys-eth/ccip2-eth-resolver) is a custom ENS resolver that fetches and renders off-chain records hosted on IPNS with `CCIP-Read`. This resolver doesn't need web2 gateways to relay off-chain records and instead relies on hosting of pre-signed records on IPNS. This is an optional/opt-in resolver and ENS users must manually switch their resolver address to enable off-chain features.

- [**NameSys Client**](https://namesys.eth.limo) is a dedicated UI for the CCIP2 resolver, where users can set their records themselves on IPNS. NameSys client uses a novel key-generation algorithm which allows users to host their content on IPNS without forfeiting control of their IPNS private keys to a third party. This results in secure, gasless, upgradeable and autonomous ENS records, making NameSys a **first-of-its-kind** implementation.

![](https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/png/namesys.png)

## 💡&nbsp; Why `NameSys`?

The usage of ENS records seems to have pleatued despite their enormous potential tp provide a decentralised web3 identity. This is a consequence of high gas costs associated with adding and updating the records on the blockchain. During periods of increased demand for Ethereum blockspace, it can easily cost more to set a text record than an entire year's registration for a 5-character ENS name. While IPNS has reduced the gas costs associated with updating `contenthash`, other records appear to either be unset or rarely updated once set. NameSys is designed to solve this precise problem and serve as an **off-chain, zero-cost and secure alternative** to on-chain records.

## ⚙️&nbsp; How `NameSys`?

🤔&nbsp; With NameSys, we ensure that taking your ENS records off-chain doesn't compromise their integrity. In order to do this, we choose IPFS as the off-chain storage for the records. While IPFS is a trivial choice for decentralised storage, IPFS hashes are uniquely defined by their content and therefore not reusable. Traditionally in such situations, IPNS is the next natural choice. However, this is not an easy alternative since there are no providers which offer accessible and secure IPNS pinning service. There do exist pinning services like [dWebServices](https://dwebservices.xyz) and [1W3.io](https://1w3.io) but these third-party providers require you to give up control of your IPNS private keys; this is a massive central point of vulnerability and not an option for hosting sensitive ENS records such as addresses.

![](https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/png/fullStack.png)

💡&nbsp; NameSys client solves this security vulnerability by using a [novel keygen algorithm](https://github.com/dostr-eth/nips/blob/ethkeygen/111.md) which allows users to generate their IPNS keys in the browser itself and pin their records straight to the IPNS storage; users do not need to share their IPNS keys with us since content pinning in performed on client-side by the user themselves. The records storage on IPFS is handled by NameSys's IPFS node permanently although the users are free to additionally host their records through other providers such as Pinata, Fleek etc.

![](https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/png/keygen.png)

🥳&nbsp; With this software stack, users are able to host their records on as many IPFS providers as they like and pin the hosted records to their IPNS public key in a secure and custodial manner that doesn't require private key sharing. Consequently, NameSys enables record updates as often as possible at zero cost and allow for cool features such as dynamic avatars. We believe that CCIP2 will enable frequent updates of records other than the web `contenthash` and propel ENS adoption as an identity layer.
