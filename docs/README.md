# NameSys: Off-chain ENS Records Manager

### Universal Resolver with Gasless ENS Records Management using IPNS and CCIP-Read

##### author(s) : [`sshmatrix.eth`](@sshmatrix), [`freetib.eth`](@0xc0de4c0ffee)

## Abstract

This document introduces an optional specification for Resolvers to fetch and render ENS records with `CCIP-Read` (ENSIP-10) using IPNS and RFC-8615 `.well-known` standard. The outlined implementation doesn't need web2 gateways to relay off-chain records and instead relies on hosting of records on IPNS. Users can host these records themselves on IPNS using the proper format or alternatively use the dedicated NameSys client, both of which result in a gasless, upgradeable and autonomous implementation. This specification is fully optional and ENS users must manually switch their Resolver address to enable the features included therein.

## Motivation

ENS has the potential to revolutionise decentralised access to the web with an attached identity system through linked records, but the usage of ENS records seems to have pleatued. This is a consequence of intrinsically high gas costs associated with adding and updating the records since there are no additional fees to set records. While IPNS has reduced the gas costs associated with updating `contenthash`, other records appear to either be unset or rarely updated once set.

This specification solves the aforementioned problem of high gas costs by storing the ENS records off-chain inside `.well-known` (RFC8615) directory of the users' IPNS contenthash. Records stored under `.well-known` standard can then be queried through [ENSIP-10](https://docs.ens.domains/ens-improvement-proposals/ensip-10-wildcard-resolution) (`CCIP-Read`) implemented in this specification. The implementation outlined here doesn't require any additional gateways to fetch and render the ENS records, and the user is fully in control of their records, e.g. hosting the records on IPFS and linking the IPFS hash to their IPNS key. With this method, users are able to update their records as often as possible at no cost whatsoever without ever losing custody of their data (see figure below). We believe that this specification will enable frequent updates of records other than the `contenthash`, propel ENS adoption as an identity layer and allow abstracted services such as private payments using ENS.

&nbsp;
![](https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/png/fullStack.png)

## Specification

The proposed Resolver and ENS records storage outlined in this document expects the following implementation:

### CCIP-Read Resolver (ENSIP-10)

This specification is an extension of ENSIP-10 `CCIP-Read` applied to IPNS/IPFS as decentralised storage.

&nbsp;
![](https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/png/namesys.png)

### Off-Chain Records Storage

For this specification to make pratical sense, we expect the `contenhash` to be of IPNS type. IPNS hashes are key-based decentralised storage pointers that only need to be added once to on-chain storage by the user. IPNS hashes can in turn serve as proxy and point to upgradeable IPFS or IPLD content. In the parent IPNS directory, the records must be stored in the [RFC-8615](https://www.rfc-editor.org/rfc/rfc8615) compliant `.well-known` directory format. ENS records for any name `sub.domain.eth` must then be stored in JSON format under a [reverse-DNS](https://en.wikipedia.org/wiki/Reverse_domain_name_notation) type directory path using `/` instead of `.` as separator, i.e. in format `.well-known/eth/domain/sub/<record>.json`.

#### Some Examples:

- ENS text record for `vitalik.eth`'s avatar is stored at `ipns://<ipns_hash>/.well-known/eth/vitalik/text/avatar.json` formatted as

```solidity
{ data: abi.encode(<avatar>) }
```

- ETH address record for `sub.domain.eth` is stored at `https://<ipns_hash>/.well-known/eth/domain/sub/address/60.json` formatted as

```solidity
{ data: abi.encode(<address/60>) }
```

### Stealth Payments

With the ability to update ENS records infinitely with NameSys, two parties can interact in an **encrypted** manner using their respective `RSA` (`2048 BITS`) public key records. For example, if Bob wants Alice to pay an `INVOICE` (to one of Bob's private addresses), he can encrypt the invoice with Alice's `RSA` public key and post the resulting `STEALTH` cipher as a record. Alice can then read this encrypted record, decrypt its contents with her private `RSA` key and pay the resulting `INVOICE`.

#### `INVOICE`

```js
let INVOICE = {
                    "payer": "nick.eth",
                    "payee": "vitalik.eth",
                   "amount": "0.420",
                "extradata": "bla1234", // Optional in v1.1-beta
                "signature": "0x2a4e...9ac6" // Optional in v1.1-beta
              }
```

&nbsp;
![](https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/png/stealth.png)

### Security

To ensure secure record resolution, records must be signed by a domain-specific signer (called `approvedSigner`) set by the manager of a legacy ENS or the owner of a wrapped ENS. The `approvedSigner` may be stored on-chain or off-chain by the manager (of a legacy ENS) or the owner (of a wrapped ENS) in the CCIP2 contract. Upon each resolution, CCIP2 resolver verifies the signature against on-chain and/or off-chain `approvedSigner`, aka on-chain signer and/or off-chain signer approved by the manager/owner of the legacy/wrapped (sub)domain.

## Resolver Function → JSON Mapping

| Type | Function | JSON File |
| --- | --- | --- |
| Text Records | `text(bytes32 node, string memory key)` | `text/<key>.json` |
| Ethereum Address | `addr(bytes32 node)` | `address/60.json` |
| Contenthash* | `contenthash(bytes32 node)` | `contenthash.json` |
| Multichain Address‡ | `addr(bytes32 node, uint coinType)`| `address/<coinType>.json` |
| Public Key | `pubkey(bytes32 node)`| `pubkey.json` |
| Name† | `name(bytes32 node)`| `name.json` |
| Interface‡ | `interfaceImplementer(bytes32 node, bytes4 _selector)`| `interface/0x<bytes4Selector>.json` |
| ABI‡ | `ABI(bytes32 node, uint256 contentTypes)`| `abi/<contentTypes>.json` |
| Zonehash‡ | `zonehash(bytes32 node)`| `dns/zonehash.json` |
| DNS Record‡ | `dnsRecord(bytes32 node, bytes name, uint16 resource) `| `dns/<record>.json` |

\* This is the user's web-facing contenthash contained inside the recordhash

† Name is not implemented as reverse record; users must use the official ENS on-chain reverse record for that feature

‡ Available in v1.1

## CCIP2.ETH Gateways

| Type | Identifier | Gateway URL |
| --- | --- | --- |
| `ipns://<contenthash>` | `0xe5` | `https://<base36-CID-v1>.ipns.dweb.link/.well-known/..` |
| `ipfs://<contenthash>` | `0xe3` | `https://<base32-CID-v1>.ipfs.dweb.link/.well-known/..` |
| ENS + IPNS Node | &nbsp; | `https://domain-eth.ipns.dweb.link/.well-known/..` |
| ENS | &nbsp; | `https://domain.eth.limo/.well-known/..` |
| ENS + [`IPFS2`](https://ipfs2.eth.limo) Resolver| `0xe3`, `0xe5` | `https://<CID-v1>.ipfs2.eth.limo/.well-known/..` |

## Details of Setup, Signatures and Keys

| Key | Type | Nature |
| --- | --- | --- |
| `KEY_WALLET` | `secp256k1` | Ethereum Wallet Key |
| `KEY_IPNS` | `ed25519` | Deterministic Key(gen) |
| `KEY_SIGNER` | `secp256k1` | Deterministic Key(gen) |
| `KEY_SCH` | `schnorr` | Deterministic Key(gen) |
| `KEY_RSA` | `rsa-2048` | Deterministic Key(gen) |

&nbsp;
![](https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/png/keygen.png)

## Signature Texts & Formats

### `VARIABLES`:

```js
// CAIP-10
CAIP10 = `eip155:${CHAIN_ID}:${WALLET_ADDRESS}`
```
```js
// ENS Domain
ENS = 'nick.eth'
```
```js
// IPNS Key Identifier
PASSWORD = 'key1'
```
```solidity
// EXTRADATA
bytes32 EXTRADATA = keccak256(
            abi.encodePacked(
              keccak256(
                abi.encodePacked(PASSWORD)
              ),
              WALLET_ADDRESS
              )
            );
```
```js
// ORIGIN
if (RECORDHASH) {
  ORIGIN = ENS
} else if (OWNERHASH) {
  ORIGIN = `eth:${WALLET_ADDRESS}`
} else if (HTTP_GATEWAY) {
  ORIGIN = ''
}
```
```js
// Record Encodings
RECORD_ENCODE in [
  'string',
  'address',
  'bytes'
]
```
```js
// Record Types
RECORD_TYPE in [
  'text/avatar',
  'address/60',
  'contenthash'
]
```
```js
// Record Values
RECORD_VALUE in [
  'https://example.com/avatar.png', // string-like
  '0xD62fB2a45ECd0000f858700002119d0000d21234', // address-like
  'e50101720024080112203c5aba6c9b5055a5fa12281c486188ed8ae2b6ef394b3d981b00d17a4b51735c' // hexBytes-like
]
```
```js
// Encoded Records
RECORD_VALUE_BYTES = abi.encodePacked([RECORD_ENCODE, RECORD_VALUE])
```
```solidity
// _EXTRADATA_
bytes32 _EXTRADATA_ = bytesToHexString(
                        abi.encodePacked(
                          keccak256(
                            RECORD_VALUE_BYTES
                          )
                        )
                      );
```

### `SIGN 1`:

- Signed by `WALLET` to generate IPNS Keypair

```js
Requesting Signature To Generate IPNS Key\n\nOrigin: ${ORIGIN}\nKey Type: ed25519\nExtradata: ${EXTRADATA}\nSigned By: ${CAIP10}
```

### `SIGN 2`:

- Signed by `WALLET` to generate ENS Records Signer Keypair

```js
Requesting Signature To Generate ENS Records Signer\n\nOrigin: ${ENS}\nKey Type: secp256k1\nExtradata: ${EXTRADATA}\nSigned By: ${CAIP10}
```

### `SIGN 3`:

- Signed by `WALLET` to approve `SIGNER`

```js
Requesting Signature To Approve ENS Records Signer\n\nOrigin: ${ENS}\nApproved Signer: ${SIGNER}\nApproved By: ${CAIP10}
```

### `SIGN 4`:

- Signed by `SIGNER` for Record verification by `CCIP2.eth` Resolver

```js
Requesting Signature To Update ENS Record\n\nOrigin: ${ENS}\nRecord Type: ${RECORD_TYPE}\nExtradata: ${_EXTRADATA_}\nSigned By: ${CAIP10}
```

### `SIGN 5`:

- Signed by `SIGNER` to redirect to a dApp service

```js
Requesting Signature To Install dApp Service\n\nOrigin: ${ENS}\nApp: ${DAPP}\nExtradata: ${_EXTRADATA_}\nSigned By: ${CAIP10}
```

### `SIGN 6`:

- Signed by `WALLET` to generate RSA Keypair

```js
Requesting Signature To Generate RSA Key\n\nOrigin: ${ORIGIN}\nKey Type: RSA-2048\nExtradata: ${EXTRADATA}\nSigned By: ${CAIP10}
```
