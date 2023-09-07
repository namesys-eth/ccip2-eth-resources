# Stealth Payments With NameSys

##### author(s) : [`sshmatrix.eth`](@sshmatrix), [`freetib.eth`](@0xc0de4c0ffee)

## Motivation

With the ability to update ENS records infinitely with NameSys, two parties can interact in an encrypted manner using their respective `RSA` (`2048` bits) public key records. For example, if Bob wants Alice to pay an invoice (to one of Bob's private addresses), he can encrypt the invoice with Alice's `RSA` public key and post the resulting Cipher as a record. Alice can then read this record, decrypt its contents with her private `RSA` key and pay the resulting invoice.

&nbsp;
![](https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/png/stealth.png)

### `SIGNATURE`:

- Signed by `WALLET` to generate RSA Keypair

```js
Requesting Signature To Generate RSA Key\n\nOrigin: ${ORIGIN}\nKey Type: RSA-2048\nExtradata: ${EXTRADATA}\nSigned By: ${CAIP10}
```
