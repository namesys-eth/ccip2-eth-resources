---

description:

Optional specification for gasless ENS records in IPNS using CCIP-Read.

---



# ENSIP-XX: Off-chain ENS Records Manager

| **Author**    | [freetib.eth](@0xc0de4c0ffee), [sshmatrix.eth](@sshmatrix) |
| -- |  -- |
| **Status**    | Draft |
| **Submitted** | 2023-04-XX |


### Abstract

This ENSIP introduces optional specification to store ENS /domain related/ records for ENSIP-10 based `CCIP-Read` using IPNS and RFC8615 `.well-known/` directory format. This specification is fully optional, ENS users have to manually switch their resolver address to activate this feature set.


### Motivation

ENS users with IPNS hash set in their resolver can update their website off-chain for zero gas fees but updating other ENS record types is usually higher than yearly fees for >4 char `.eth` names, that's really slowing down ENS adoption.

ENSIP-10 can read off-chain `json` data from web2 servers/database or by reading ENS records from L2 in backend.

*idea is to integrate IPNS with IPFS/IPLD type to store ENS `records.json`  in IPFS Nodes as RFC8615 `/.well-known/eth/<domain>/<sub>/<record>.json` format. This specification strictly follows ENSIP-10 to implement gasless off-chain ENS records..



### Specification
a) CCIP resolver (ENSIP-10) :

This specification is ENSIP-10 extension
```
function resolve(bytes calldata name, bytes calldata data) external view returns(bytes memory)
``

1) DNS decode `_path` and full `domain` as string from `name`
```solidity
function DNSDecode(
    bytes calldata name
) public view returns (
    string memory _domain, string memory _path, string memory _label
){
    uint level = 1; // domain level
    uint i = 1; // counter
    uint len uint8(bytes1(name[:1])); // length of label
    _label = string(name[1: i += len]); // final value is tld "eth"
    _path = _label; // suffix after /.well-known/..
    _domain = _label; // full domain as string

    while(name[i] > 0x0) { // dns decode
        len = uint8(bytes1(name[i: ++i]));
        _label = string(name[i: i += len]);
        _domain = string.concat(_domain, ".", _label);
        _path = string.concat(_label, "/", _path);
        ++level;
    }
}
```

2) RFC8615 : `.well-known` directory format for ENS records json stored as [Reverse domain name notation](https://en.wikipedia.org/wiki/Reverse_domain_name_notation) type directory path using `/` instead of `.` as separator.

	Examples :

	- ENS text record for `vitalik.eth`'s avatar is stored in `https://vitalik.eth.limo/.well-known/eth/vitalik/avatar.json` formatted as `{ data : abi.encode(string("eip155:1/erc1155:0xb32979486938aa9694bfc898f35dbed459f44424/10063"))}`

	- ETH address records for `sub.domain.eth` is stored in `https://sub.domain.eth/.well-known/eth/domain/sub/addr-60.json` formatted as `{data:abi.encode(owner_address)}`

    Implementation detail : If CCIP json data is signed by owner of domain it must be prefixed with bytes4 `callback` function selector as, ```{data: bytes.concat(Resolver.___callback.selector, signed_data}```

	Resolver function to json file name
	| Type | Function | Json file |
	| -- | -- | --- |
	|Text Records (ENSIP-05) | `text(bytes32 node, string memory key)` | \<key>.json |
	|Ethereum address | `addr(bytes32 node)` | addr-60.json |
	|Multichain Address (ENSIP-9) | `addr(bytes32 node, uint coinType)`| addr-\<coinType>.json |
	|Public Key | `pubkey(bytes32 node)`| pubkey.json |
	|Contenthash (EIP-07) | `contenthash(bytes32 node)` | contenthash.json |


3) CCIP Gateways :

    | Type | Identifier | Gateway URL|
    |--- | --- | --- |
    | ipns://\<contenthash> | 0xe5 | https://`<base36-cid-v1>`.ipns.dweb.link/.well-known/..|
    | ipfs://\<contenthash> | 0xe3 | https://`<base32-cid-v1>`.ipfs.dweb.link/.well-known/..|
    | ENS + IPFS node| -- | https://`domain-eth`.ipns.dweb.link/.well-known/..|
    | ENS | -- |https://`domain.eth`.limo/.well-known/..|
    | ENS + IPFS2 resolver| 0xe3, 0xe5 |https://`<cid-v1>`.ipfs2.eth.limo/.well-known/..|



```
	//...

	funMap[iResolver.addr.selector] = "addr-60"; // eth address
	funMap[iResolver.pubkey.selector] = "pubkey";
	funMap[iResolver.name.selector] = "name";

	//...

	bytes4 fun = bytes4(data[: 4]); // 4 bytes identifier

	if (fun == iResolver.contenthash.selector) {
		if (level == 3) resolveContenthash(labels[0]);
		__lookup(HomeContenthash);
	}

	string memory jsonFile;
	if (fun == iResolver.text.selector) {
		jsonFile = abi.decode(data[36: ], (string));
	} else if (fun == iOverloadResolver.addr.selector) {
		jsonFile = string.concat(
			"addr-",
			uintToNumString(abi.decode(data[36: ], (uint)))
		);
	} else {
		jsonFile = funMap[fun];
		require(bytes(jsonFile).length != 0, "Invalid Resolver Function");
	}
```


```
	function resolve(bytes calldata name, bytes calldata data) external view returns(bytes memory) {
        uint level;
        uint len;
        bytes[] memory labels = new bytes[](3);
        //string memory _path;
        // dns decode
        for (uint i; name[i] > 0x0;) {
            len = uint8(bytes1(name[i: ++i]));
            labels[level] = name[i: i += len];
            //_path = string.concat(string(labels[level]), "/", _path);
            ++level;
        }
        bytes4 fun = bytes4(data[: 4]); // 4 bytes identifier
        if (fun == iResolver.contenthash.selector) {
            if (level == 3)
                resolveContenthash(labels[0]);

            __lookup(HomeContenthash);
        }
        string memory jsonFile;
        if (fun == iResolver.text.selector) {
            jsonFile = abi.decode(data[36: ], (string));
        } else if (fun == iOverloadResolver.addr.selector) {
            jsonFile = string.concat(
                "addr-",
                uintToNumString(abi.decode(data[36: ], (uint)))
            );
        } else {
            jsonFile = funMap[fun];
            require(bytes(jsonFile).length != 0, "Invalid Resolver Function");
        }

        string memory _prefix;
        if (level == 3) {
            _prefix = string.concat(
                "https://",
                string(labels[0]),
                ".",
                string(labels[1]),
                ".eth"
            );
        } else {
            _prefix = string.concat("https://", string(labels[0]), ".eth");
        }
        revert OffchainLookup(
            address(this), // callback contract
            listGate(_prefix, jsonFile), // gateway URL array
            "", // {data} field, blank//recheck
            IPFS2.__callback.selector, // callback function
            abi.encode( // extradata
                block.number, // checkpoint
                keccak256(data), // namehash + calldata
                keccak256(
                    abi.encodePacked(
                        blockhash(block.number - 1),
                        address(this),
                        msg.sender,
                        keccak256(data)
                    )
                )
            )
        );
    }

```
