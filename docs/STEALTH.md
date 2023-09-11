# Stealth Payments With NameSys

##### author(s) : [`sshmatrix.eth`](@sshmatrix), [`freetib.eth`](@0xc0de4c0ffee)

## Motivation

With the ability to update ENS records infinitely with NameSys, two parties can interact in an **encrypted** manner using their respective `RSA` (`2048 BITS`) public key records. For example, if Bob wants Alice to pay an `INVOICE` (to one of Bob's private addresses), he can encrypt the invoice with Alice's `RSA` public key and post the resulting `STEALTH` cipher as a record. Alice can then read this encrypted record, decrypt its contents with her private `RSA` key and pay the resulting `INVOICE`.

### Requirements

To use stealth payments via NameSys, users must set their `RSA` public key as an ENS Text Record. User's private key will be generated in-app using their deterministic wallet signature and then purged after the decryption process; this follows the standard NameSys protocol for handling keypairs. Please read the [main guide](https://github.com/namesys-eth/ccip2-eth-resources/blob/main/docs/GUIDE.md) before proceeding further.


&nbsp;
<img src="https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/png/stealth.png" width="700">

### Signature

- Signed by `WALLET` to generate RSA Keypair

```js
Requesting Signature To Generate RSA Key\n\nOrigin: ${ORIGIN}\nKey Type: RSA-2048\nExtradata: ${EXTRADATA}\nSigned By: ${CAIP10}
```

## GUIDE

### STEP 1

Find your way to the Stealth Records button. This button will be active only after you have completed the resolver migration (see [full guide here](https://github.com/namesys-eth/ccip2-eth-resources/blob/main/docs/GUIDE.md) for migration)

&nbsp;
<img src="https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/guide/enterStealth.png" width="500">

### STEP 2

You'll arrive at the Stealth modal where you'll be able to set your stealth records. To use stealth features, it is advisable to set the RSA public key. In strict sense, you only need to set this record if you intend to **send** a private payment; receving private payments doesn't require this record. To set the RSA public key, click on `SET`.

&nbsp;
<img src="https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/guide/editRSA.png" width="500">
&nbsp;

Upon completing this, you will see your `RSA` records set with a value; this value is your RSA public key that the Payer(s) need to send you money privately.

### STEP 3

Once your RSA key is set, you are ready to receive as well as send stealth payments.

### STEP 3a: RECEIVING STEALTH PAYMENTS

Click on `SET` in the `STEALTH` field.

&nbsp;
<img src="https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/guide/RSA.png" width="500">
&nbsp;

This will open the password modal as usual followed by the Invoice modal where can set the Payer, your private address or private ENS and the amount to receive.

&nbsp;
<img src="https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/guide/Invoice.png" width="400">
&nbsp;

Fill in the values of your choice and complete the process with signatures. Once your are finished, your encrypted invoice will appear in the `STEALTH` field

&nbsp;
<img src="https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/guide/Encrypted.png" width="500">

The Payer can now pay you to your private address or ENS 🥳

> Note that the Payee did not require their own `RSA` key to receive the payment. Like previously mentioned, only the Payer needs their `RSA` public key set as a Record to make the private payment.

### STEP 3b: SENDING STEALTH PAYMENTS

Let's now go through how one can pay privately using NameSys. To begin, enter the ENS of the receiver of private payment and click on `DECRYPT`.

&nbsp;
<img src="https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/guide/Decrypt.png" width="500">
&nbsp;

This will initiate a search for encrypted invoice and if successful, you will see the decrypted invoice in your window. Simply click on `PAY` to pay the invoice to the private address of the Payee 🥳

&nbsp;
<img src="https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/guide/Pay.png" width="500">

## RELATED GUIDES

[`GUIDE:: HOW-TO NAMESYS`](https://github.com/namesys-eth/ccip2-eth-resources/blob/main/docs/GUIDE.md)

## MORE RESOURCES

[`SUMMARY`](https://github.com/namesys-eth/ccip2-eth-resources/blob/main/docs/EASYREAD.md)

[`FAQ`](https://github.com/namesys-eth/ccip2-eth-resources/blob/main/docs/INTRO.md)

[`SPECS`](https://github.com/namesys-eth/ccip2-eth-resources/blob/main/docs/README.md)
