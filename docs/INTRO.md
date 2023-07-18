# NameSys.eth: Off-Chain ENS Records Manager

Hello frENS,

❗ Have you ever wanted to set records for your ENS names for free forever?

❗ Did you ever wish that you could update your avatar for free infinite number of times?

❗ Do you get sick of high gas costs getting in the way of your ENS addiction?

❗ How often would you change your records if you could do it for free?

We are sure that you have asked these questions to yourselves, and we are glad to announce that we have **the** cure for all your ailments. Everyone knows that gas is and has been a big pain in the ass for ENS degens and regens alike. Previously, IPNS made it free to update our contenthashes, and in more recent times, CCIP-Read has promised us free stuff such as off-chain subdomains (e.g. NameStone.xyz). While that is cool, Devs at NameSys continued asking themselves the following question:

#### 💡&nbsp; If we can use IPNS for free contenthash updates and CCIP-Read for free subdomains, why can't we combine the two and use IPNS & CCIP-Read for **Off-Chain Records**?

Today is the day when we deliver to you the ultimate free stuff, which is the answer to the question above! NameSys is an **Off-Chain ENS Records Manager** which allows users to host their ENS records off-chain on IPNS in an autonomous and gasless fashion. The off-chain records are resolved using `CCIP-Read` by a custom resolver (called `CCIP2`) capable of reading records from IPNS.

#### 💡&nbsp; While this sounds cool, one might wonder why this hasn't been done already...?

The main reason is that unlike contenthash, text records such as addresses are sensitive information. `CCIP-Read` is built to read from off-chain sources which are usually servers. Hosting records on centralised servers requires severe trust assumptions and is therefore highly dangerous!

#### 💡&nbsp; Okay, that sounds reasonable! But what about other decentralised off-chain storage solutions like IPFS and Arweave?

While IPFS can be used, IPFS hashes are immutable and cannot be reused. Using IPFS is a better solution but it is not gas-efficient since updating records will require posting new hashes to the blockchain.

#### 💡&nbsp; Well, we already have IPNS for that! Why not use IPNS similar to how we use it for free contenthash updates?

That is indeed a good idea, but note that IPNS pointers/hashes are actually keypairs. Currently, no public service exists so far that will allow users to autonomously pin IPNS key without sharing the private key. Services like 1W3.io and dWebServices.xyz require users to share their private key with them; this is highly unsuitable for storing sensitive records and a massive threat vector!

#### 💡&nbsp; Hmmm, I see. It seems the key to solving this problem is to design a non-custodial solution for hosting IPNS records where users do not have to share their IPNS private key with the service provider. Unless such a solution exists, off-chain & upgradeable ENS records cannot be safely implemented. Is this correct?

Yes, that is correct, and we have the solution. NameSys stack is capable of solving this exact problem.  

#### 💡&nbsp; How does NameSys do it?

NameSys accomplishes secure record storage on IPNS by cleverly generating IPNS keypair from user's wallet signatures (NIP-111 Keygen Algorithm) and using `w3name` API for keyless IPNS hosting. NameSys streamlines the entire mechanism of securely generating IPNS keypair, encoding records with **secure** signatures, posting IPFS content to IPNS in a keyless manner and finally handling **verified** resolution of the records on IPNS with `CCIP2` custom resolver. No more sharing your IPNS private key with a service!

#### 💡&nbsp; That sounds cool! Can you explain the technicals a bit more? What do I have to do to start using off-chain records?

Okay, sure. Here go the step-by-step details: You can start by simply visiting the [NameSys Client](https://namesys.eth.limo) and connecting your wallet.

🧪&nbsp; The first step to start using off-chain records is the initial setup: it consists of setting your resolver to `CCIP2` (TXN1) and setting your main IPNS contenthash on-chain (called `recordhash`; TXN2) which will contain all your off-chain records. NameSys client will handle generating the corresponding IPNS private key using your signature (SIG1 in Metamask) and a prompted `password`.

> Note: `password` is your unique (and **secret**!) identifier for the IPNS keypair and you must remember this for future record updates

🧪&nbsp; Upon completing the setup process, you are ready to use free and secure off-chain records for your ENS domain forever! In order to set a new record, simply continue in the client. Each time you attempt to update a record, the client will ask for your secret `password` and prompt for a signature in Metamask, and generate the IPNS private key from it. Client will then sign your new records for verification by the resolver and pin them to your IPNS public key using `w3name` API. After this step, the IPNS keypair is destroyed and no record of it exists anywhere in the universe! It is precisely this step that makes NameSys secure. Upon each update, the IPNS keypair can only be re-generated by the user with their unique signature and secret `password` that only they know!

🧪&nbsp; Lastly, the `CCIP2` resolver is tasked with the job of reading the records that you just updated on IPNS using `CCIP-Read`. The resolver additionally verifies the signatures appended with the records before resolving them, thereby adding an additional layer of on-chain security!

&nbsp;
![](https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/png/fullStack.png)

## 🥳&nbsp; OFF-CHAIN FREE AND SECURE RECORDS BY NAMESYS!
