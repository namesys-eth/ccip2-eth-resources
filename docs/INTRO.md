# NameSys.eth: Off-Chain ENS Records Manager

Hello frENS, degENS, squatENS,

❗ Have you ever wanted to set your ENS Records for free

❗ Did you ever wish that you could update your avatar dynamically for free infinite number of times?

❗ Do you get sick of high gas costs getting in the way of your undeniable ENS addiction?

❗ How often would you change your records if you could do it for free forever?

We are sure that you heard these musings in countless larping sessions/spaces, and lo and behold, we are esctatic to announce that we have **THE** cure for all your ailments. Everyone knows that gas has been THE biggest pain in the ass for ENS degens and regens alike. Previously, IPNS made it free to update our contenthashes at least, and in more recent times, CCIP-Read has promised us free stuff such as off-chain subdomains (e.g. NameStone.xyz) etc. While that is cool, Devs at NameSys continued asking themselves the following question:

#### 💡&nbsp; If we can use IPNS for free contenthash updates and CCIP-Read for free subdomains, why can't we combine the two and use IPNS & CCIP-Read for **Off-Chain Records**?

The answer is naturally YES, and today is the day when we deliver to you the ultimate free stuff! NameSys is an **Off-Chain ENS Records Manager** which allows users to host their ENS records off-chain on IPNS in an autonomous and gasless fashion. The off-chain records are resolved using `CCIP-Read` by a custom resolver (called `CCIP2`) capable of reading records from IPNS.

#### 💡&nbsp; While this sounds cool, one might wonder why this hasn't been done already...?

The main reason for that is: Text records such as addresses are sensitive information. `CCIP-Read` is designed to read from off-chain sources which are usually servers. Hosting records on centralised servers requires severe trust assumptions and is therefore extremely dangerous!

#### 💡&nbsp; Okay, that sounds reasonable! But what about other decentralised off-chain storage solutions like IPFS and Arweave?

While IPFS can be used, IPFS hashes are immutable and cannot be reused. So IPFS is indeed a relatively better solution but it is not gas-efficient since updating records will require posting new hashes to the blockchain.

#### 💡&nbsp; Well, we already have IPNS for that! Why not use IPNS similar to how we use it for free contenthash updates?

That is indeed a good idea, but note that IPNS pointers/hashes are actually keypairs. Currently, no public service exists that will allow users to autonomously pin IPNS public key without sharing their private key with the pinning provider. Services like 1W3.io and dWebServices.xyz require users to share their private key with them; this is highly unsuitable for storing sensitive records and a massive threat vector!

#### 💡&nbsp; Hmmm, I see. It seems the key to solving this problem is to design a non-custodial solution for hosting IPNS records where users do not have to share their IPNS private key with the service provider. Unless such a solution exists, off-chain & upgradeable ENS records cannot be safely implemented. Is this correct?

Yes, that is correct, and we have the solution! NameSys stack is that non-custodial and autonomous off-chain solution which provides similar level of security as on-chain records, while saving you all that gas!

#### 💡&nbsp; How does NameSys do it?

NameSys accomplishes secure record storage on IPNS by cleverly generating deterministic IPNS keypairs from users' wallet signatures and using `w3name` API for keyless IPNS hosting. NameSys streamlines the entire mechanism of **a)** securely generating IPNS keypair, **b)** encoding records with **secure** signatures, posting IPFS content to IPNS in a **keyless** manner and finally handling **verified** resolution of IPNS records with `CCIP2` custom resolver. No more sharing your IPNS private key with a third-party service!

#### 💡&nbsp; That sounds cool! Can you explain the technicals a bit more? What do I have to do to start using off-chain records?

Okay, sure! Here go the step-by-step details: You can start by simply visiting the [NameSys Client](https://namesys.eth.limo) and connecting your wallet.

🧪&nbsp; The first step to start using off-chain records is the initial Setup: it consists of setting your resolver to `CCIP2` (`TXN1`) and setting your parent IPNS contenthash on-chain (called `recordhash`; `TXN2`) which will contain all your usual ENS records. NameSys client will handle generating the corresponding IPNS private key using your signature (`SIG1` in Metamask) and a prompted `password`.

> Note: `password` is your unique (and **secret**!) identifier for the IPNS keypair and you must remember this for future record updates

> Note: Users must make sure that the auto-generated `SIG1` is treated on equal footing with `password` in terms of secrecy

🧪&nbsp; Upon completing this simple setup process, you are ready to use free and secure off-chain records for your ENS domain forever! In order to set a new record, simply continue in the client. Each time you attempt to update a record, the client will ask for your secret `password` and prompt for a determin signature in Metamask, and generate the deterministic IPNS private key from it. Client will then sign your new records (for verification by the resolver) and pin them to your IPNS public key using `w3name` API. After this step, the IPNS private key is destroyed and no record of it exists anywhere in the universe! It is precisely this step that makes NameSys secure. Upon each update, the IPNS keypair can only be re-generated by the user with their unique signature and secret `password` that only they know!

🧪&nbsp; Lastly, the `CCIP2` resolver is tasked with the job of reading the records that you just updated on IPNS using `CCIP-Read`. The resolver additionally verifies the signatures appended with the records before resolving them, thereby adding an additional layer of on-chain security!

&nbsp;
![](https://raw.githubusercontent.com/namesys-eth/ccip2-eth-resources/main/graphics/png/fullStack.png)

#### 💡&nbsp; Hold up, are you saying that I can use off-chain records for FREE FOREVER after completing the one-time initial Setup?

That is precisely what we are saying! Note that NameSys provides you with a similar level of security as on-chain records. It doesn't use any centralised storage like servers. It doesn't force you to share your IPNS private key with a third-party. It is fully autonomous!

#### 💡&nbsp; This seems too good to be true! What's the catch here? Off-chain storage cannot theoretically equate to on-chain storage; this will defeat the whole purpose of blockchain.

Well notes, there is of course a catch! IPNS records can take anywhere between 60 seconds to 60 minutes to propagate after setting them. Unlike on-chain records that have 100% live-time and instantaneous resolution, IPNS records can occassionally be slow to resolve or at least take a few minutes to become live after you have set them. This is the sacrifice we make to keep the records secure! In the grand optimisation scheme, we have tuned for safety and prioritised security over instant post-update availability. Having said that, these issues are easily solvable since NameSys allows users to re-generate & export their IPNS private key (and IPFS hash) if they seek to pin their records elsewhere such as Pinata, Fleek, dWebServices etc. This should resolve the up-time and live-time issue.

#### 💡&nbsp; Does this mean I can set DYNAMIC avatars?!

YES! NameSys makes dynamic avatars possible. NameSys also makes dynamic addresses possible, e.g. users can programatically set their resolved addresses to vary with time or other parameters. This is some low-level Account Abstraction built with ENS!

#### 💡&nbsp; This sounds very promising and full of possibilities!

It sure is! We hope that the ENS community will finally be able to take advantage of FREE & SECURE RECORDS FOREVER! 🎉
