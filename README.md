<p align="center">
  <img src="https://github.com/benchlab/benchx-media/raw/master/benos-logo.png" width="300px" alt="benOS Logo"/>
</p> <br>

# Kepler
Kepler Is The Global Identity Manager For Everything From Objects (Files, Data and Media), to Bench Computers, dApps, Users, Wallets and More Across The Bench Network. 

## Under Development 
Kepler is currently under development in the `development` branch. 

## What Purpose Will Kepler Serve?
Kepler's sole job is to create UIDs for anything across the Bench Network, from [Neutron](https://github.com/benchlab/neutron)-based decentralized networks (RootChains, SideChains and dappChains), [Aero](https://github.com/benchlab/aero) Objects (Files, Data and Media), [Nova](https://github.com/benchlab/nova) Compute Nodes (Bench Computers), dApps, hardware resources from [Nova](https://github.com/benchlab/nova) Compute Nodes (Bench Computers), BenchWallet addresses and users within the Bench network. Anything and everything on the Bench Network, can be identified and truly brings together a network that will never be controlled by a single entity.   

## Kepler UID Structure & Attributes
Every Kepler UID has its own set of attributes, which make it easy on Kepler when deciphering what a UID was created for, what type of Kepler UID it is, who created the Kepler UID, [Quarantine](https://github.com/benchlab/quarantine)-based data arrays that help with associating data that is related to the UID, for example an Object UID for a file will have a file location or location(s) on the Bench Network inside these data-arrays. We call these data-arrays `klobs`. A `uni_key` is the last but sometimes the most important attribute within the Kepler UID structure, especially for Kepler UIDs for objects, where the `uni_key` is used as a verification mechanism for users wanting to access the object, and users wanting access would have to verify their `sec_key` that is required to match the `uni_key` stored with the Kepler Object UID, in order for the user to access that object or any user to access the object. Although, Kepler UID `types` allow for Kepler UIDs that represent objects, to be made public, where key authentication for accessing the data isn't needed. Below are the structures and attributes for Kepler Object UIDs and Kepler Account UIDs. Although these are the only examples shown, there are other types of Kepler UIDs used within the network.

### How Kepler Generates RFC4122-Compliant UUIDs
Kepler utilizes a Javascript library called [KeplerGen](https://github.com/benchlab/keplergen), that is used to generate RFC4122 (v4) UUIDS. It is used within [KeplerBase](https://github.com/benchlab/keplerbase) that is utilized by [Kepler-CLI](https://github.com/benchlab/Kepler-CLI) 

### Kepler Object UID Attributes 
***Attributes:*** <br>
**Key:** `uuid`: an RFC4122-compliant UUID used for identifying a Bench Network object. <br>
`account_uuid`: account UUID that created the Object UUID for a Bench Network object. <br>
`type`: the type of Object UUID. <br>
`klob`: klobs are data related to the UUID. This could be the location of a file or more. Klob has its own structure.<br>
`uni_key`: universal (public) key that is generated along with the Kepler Object UUID. <br>
`nonce`: nonce related to the Kepler Account UUID. 


### Kepler Account UID Attributes
***Attributes:*** <br>
**Key:** `uuid`: Key value UUID for KeplerAccount ID Object, generated via `KeplerUUID` library. <br>
`account_uuid`: RFC-compliant v4 Account UUID for KeplerAccount ID Object, generated via `KeplerUUID` library. <br>
`id`: SHA256 hash of the `account_uuid` <br>
`wallet_addr_sec`: ed25519 secret key, derived from seed, which derives from `id` <br>
`wallet_addr_uni`: ed25519 universal key, derived from `wallet_addr_sec` <br>
`sec_key`: ed25519 secret key, derived from `wallet_addr_sec`, which derives from `id` <br> 
`uni_key`: ed25519 universal key, derived from `sec_key` <br> 
`nonce`: SALSA20 hash of uni_key <br> 
`hex_key`: BASE64 of Account ID Object UUID Key <br> 
`klob`: klobs are data related to the Account UUID. This could be the benOS-related node that the Account UUID was generated from. Klob-based data generated with Account UUIDs can differ, depending on the circumstances surrounding the generation of the Account UUID. <br>
`klob`>`uuid`: Reference of the `uuid`  <br>
`klob`>`account_uuid`: Reference of the `account_uuid` <br>
`klob`>`time_created`: Time that the KeplerAccount ID Object was created <br>
`klob`>`benchx_uuid`: Only included and auto-generated, if generated via benOS-based device <br>

## Kepler-CLI
[Kepler-CLI](https://github.com/benchlab/kepler-cli) is the command line tool which interacts with the Kepler network identity service to initialize and update data within the Kepler network identity service. 

### Kepler-CLI Usage

```
# kepler-cli new account
┌──────────────────────────────────────┬───────────────────────────────────────────────────────────────────────────┐
│             kepler uuid              │             account_uuid             │           wallet_addr              │
├──────────────────────────────────────┼───────────────────────────────────────────────────────────────────────────┤
│ 2fd305ea-912c-405b-bfed-7d98143d0d56 │ e4f48839-db29-47c4-abc9-7e33dada1858 │  ba9ce39273b2a1cf04cc948893fea3c8  │
└──────────────────────────────────────┴───────────────────────────────────────────────────────────────────────────┘
uuid: 2fd305ea-912c-405b-bfed-7d98143d0d56 // Key value UUID for KeplerAccount ID Object, generated via `KeplerUUID` library.
account_uuid: e4f48839-db29-47c4-abc9-7e33dada1858 // RFC-compliant v4 Account UUID for KeplerAccount ID Object, generated via `KeplerUUID` library.
id: 3ebb0942f24e02c2f69d7d79bf4ace02645d42d247336738c0777084826aaac0 // SHA256 hash of the `account_uuid` 
wallet_addr_sec: upzjknOyoc8EzJSIk/6jyOGLIrS4mpml/hcQoMOaNDE= // ed25519 secret key, derived from seed, which derives from `id` 
wallet_addr_uni: VYBioijzebrLwDX2K8wkMRLD98iRjbatQV4guXw2iDw= // ed25519 universal key, derived from `wallet_addr_sec`
sec_key: ThO6DslXOwZucznK/E0jjUNYR3tw2sySjgW6HXjmd6wkapkxYvMLH7XCFamlYgd4K2YZ/1WA/wRD6Pb/Pc9nLg== // ed25519 secret key, derived from `wallet_addr_sec`, which derives from `id`
uni_key: JGqZMWLzCx+1whWppWIHeCtmGf9VgP8EQ+j2/z3PZy4= // ed25519 universal key, derived from `sec_key`
nonce: 0fef761a1f95b18948412e521a37ee49369d46b0025dd71cfd5d246c9744f3d1294eeab44acb0f320352f82a29dca4a2f503468098a99f4496c997fbe891846a // SALSA20 hash of uni_key
hex_key: MmZkMzA1ZWEtOTEyYy00MDViLWJmZWQtN2Q5ODE0M2QwZDU2 // BASE64 of Account ID Object UUID Key 
klob: { 
uuid: 2fd305ea-912c-405b-bfed-7d98143d0d56, // Reference of the `uuid` 
account_uuid: 'e4f48839-db29-47c4-abc9-7e33dada1858', // Reference of the `account_uuid`
time_created: '2018-05-20T07:11:22.526Z', // Time that the KeplerAccount ID Object was created
benchx_uuid: 'b33a4dcd-7057-4618-a635-9ad476cb45c3' // Only included and auto-generated, if generated via benOS-based device
}
```
`kepler-cli` `benchmark` - Kepler-CLI has an onboard benchmarking tool, used to monitor the performance of Kepler-CLI's key generation, messaging signing and key pair serialization statistics. 

```
# kepler-cli benchmark 

===== Key Generation =====
Iterations: 3400000
Total runtime: 211s
Keys per sec: 7309
===== Message Signing =====
Iterations: 3400000
Message size: 4096 bytes
Total runtime: 17s
Signatures per sec: 43171
===== Key Pair Serialization  =====
Iterations: 3400000
Total runtime: 41s
Roundtrips per sec: 12819

```
`kepler-cli` `new website` - Kepler-CLI has the ability to upload websites to a Nova Compute Node (benOS-powered hardware) on the Bench Network. It returns a `website_uuid` and signs the upload with the `uni_key`, `sec_key` to create a `signature`. To upload a new version of a website, you would have to have the uni_key and sec_key to do so. A `klob_website` is created with data related to the website upload, including the `time_created` and the `benchx_uuid` which is the Nova Compute Node, it was uploaded from.
```
# kepler-cli new website -l ~/websites/bench-website/
Uploading files to network... 
>> 10%
>> 23%
>> 41%
>> 83%
>> 97%
_| Website uploaded to the network! 

_| Kepler Website Object UUID Attributes:
uuid: 2c70f86b-d052-4527-b5dd-cabc0eafc94e
website_uuid: fe069f33-4916-47ab-8663-a90ea34d0f07
sec_key: +pNWvwQL9piAf5E3vpnlmwxUj7WXEiPpEKguqtTMLYK3vs4Lj4ryk5wwc0WTWM9QExDotp80S8K7yNASV//fuw==
uni_key: t77OC4+K8pOcMHNFk1jPUBMQ6LafNEvCu8jQElf/37s=
signature: LvtL91SuslqE+t7LBBDxx6Hod2wu9iMvdYbW/EZ/fbgqo2+vyT+VjxP8pU8VOZrtYaSU4oACQQkqZOc0hziQCA==
memo: benchx
nonce: wC526HWiquE/A1q2FxJRKpRIfCs50H1t
hex_key: ea75a7a1522886a9e5d7784c922d430a17fc1478cae6a4fe671c5a99282eef44
klob_website: { 
uuid: 2c70f86b-d052-4527-b5dd-cabc0eafc94e,
website_uuid: 'e4f48839-db29-47c4-abc9-7e33dada1858',
time_created: '2018-05-20T07:11:22.526Z',
benchx_uuid: 'b33a4dcd-7057-4618-a635-9ad476cb45c3'
}
```

# What Is benOS
[benOS](https://github.com/benchlab/benos) is a decentralized operating system, originally based on Linux, uses some design strategies from [RedoxOS](https://github.com/redox-os) and even some design concepts from [OpenStack](https://github.com/openstack), [Ethereum](https://github.com/ethereum/go-ethereum) and [EOS](https://github.com/eosio). Although we utilize some of their design strategies, benOS is completely custom from a codebase perspective. 

benOS has many components that make the wheels turn. Below are a list of those components:

## Other benOS Network Components
[Nova](https://github.com/benchlab/nova) - Global Decentralized Hypervisor For The Bench Network <br>
[Kepler](https://github.com/benchlab/kepler) - Global Decentralized Identity Management For The Bench Network <br>
[Designate](https://github.com/benchlab/designate) - Global Decentralized Naming Service For The Bench Network <br>
[Flutter](https://github.com/benchlab/flutter) - Global Decentralized Image Service For The Bench Network <br>
[Neutron](https://github.com/benchlab/neutron) - Global Network Creation & Management For The Bench Network <br>
  - [BenchCore](https://github.com/benchlab/BenchCore) - Core Decentralized Network Component For The Bench Network <br>
  - [BenchChain](https://github.com/benchlab/BenchChain) - Neutron's RootChain On The Bench Network <br>

[Aero](https://github.com/benchlab/aero) - Global Object Storage Distributor & Manager For The Bench Network <br>
[Explorer](https://github.com/benchlab/explorer) - Global dApp Distributor, Manager and Viewer For The Bench Network <br>
[benFS](https://github.com/benchlab/benFS) - benOS FileSystem <br>
[dappJS](https://github.com/benchlab/dappjs) - dApp Development Kit For The Bench Network <br>
[Mercury](https://github.com/benchlab/mercury) - benOS Graphical User Interface <br>
[Asteroid](https://github.com/benchlab/go-asteroid) - benOS Native Programming Language <br>
[Meteor](https://github.com/benchlab/meteor) - benOS Native IDE for dApp Development <br>
<br>

## benOS Core Components
[benOS-Microkernel](https://github.com/benOS-Microkernel) - benOS Microkernel <br>
[benOS-Bootloader](https://github.com/benchlab/benOS-Bootloader) - benOS Bootloader <br>
[ParseArgs](https://github.com/benchlab/parseargs) - benOS-based Argument Parsing  <br>
[X](https://github.com/benchlab/X) - benOS Graphical User Interface <br>

**NOTE:** ***There are other pieces under development as well, as our development team grows.*** 

## CREDITS AND ATTRIBUTES
benOS may use software from other open source libraries. For a full list of software credits and acknowledgements, please visit [https://github.com/benchlab/benOS/blob/master/ATTRIBUTES.md](https://github.com/benchlab/benOS/blob/master/ATTRIBUTES.md). The original LICENSE or LICENSES for the originating software(s) and library or libraries that were used to create `Kepler` are still active, although, considering this Bench software and the softwares and/or libraries/packages it is `imported` into may be used to issue illegal securities, the BENCH LICENSE is activated for this purpose. This does not take away the credits, disable the originating LICENSE or in any way disown the original creation, creators, developers or organizations that originally developed many of the libaries used throughout Bench's large array of software libraries packaged together for the purposes of building a decentralized operating system (benOS)

## VERSION
1.0.0

## LICENSE
BENCH LICENSE<br>
For Kepler
<br><br>
Copyright (c) 2018 Bench Computer, Inc. <legal@benchx.io>
<br><br>
Permission to use, copy, modify, and distribute this blockchain-related
software or blockchain-based software for any purpose with or without 
fee is hereby granted, provided that the above copyright notice and this 
permission notice appear in all copies.

THE USAGE OF THIS BLOCKCHAIN-RELATED OR BLOCKCHAIN-BASED SOFTWARE WITH THE
PURPOSE OF CREATING ICOS OR "INITIAL COIN OFFERINGS", UNREGISTERED SECURITIES 
SPECIFICALLY IN THE UNITED STATES OR IN OTHER COUNTRIES THAT HAVE A LEGAL 
FRAMEWORK FOR SECURITIES, IS PROHIBITED. BENCH FOUNDATION, LLC RESERVES THE 
RIGHT TO TAKE LEGAL ACTION AGAINST ANY AND ALL COMPANIES OR INDIVIDUALS WHO
USE THIS BLOCKCHAIN-RELATED OR BLOCKCHAIN-BASED SOFTWARE FOR THE PURPOSE OF 
DISTRIBUTING CRYPTOCURRENCIES WHERE THOSE CRYPTOCURRENCIES AND THEIR METHOD
OF DISTRIBUTION ARE IN DIRECT VIOLATION OF UNITED STATES SECURITIES LAWS. 
IF A GOVERNMENT BODY TAKES ACTION AGAINST ANY USERS, DEVELOPERS, MARKETERS,
ORGANIZATIONS, FOUNDATIONS OR ANY PROFESSIONAL ENTITY WHO CHOOSES TO UTILIZE
THIS SOFTWARE FOR THE DISTRIBUTION OF ILLEGAL SECURITIES, BENCH COMPUTER INC.
WILL NOT BE HELD LIABLE FOR ANY ACTIONS TAKEN BY THE USERS, DEVELOPERS, MARKETERS,
ORGANIZATIONS, FOUNDATIONS OR ANY PROFESSIONAL ENTITIES WHO CHOOSE TO DO SO.

UNITED STATES SECURITIES VIOLATIONS SPECIFICALLY REFER TO ANY VIOLATIONS OF
SECTION 10(b) OF THE SECURITIES EXCHANGE ACT OF 1934 [15 U.S.C. § 78j(b)] AND
RULE 10b-5(b) PROMULGATED THEREUNDER [17 C.F.R. § 240.10b-5(b)], AND
SECTIONS 5(a), 5(c), and 17(a)(2) OF THE SECURITIES ACT OF 1933 [15 U.S.C.
§§ 77e(a), 77e(c), and 77q(a)(2)]; BY MAKING USE OF ANY MEANS OR INSTRUMENTS
OF TRANSPORTATION OR COMMUNICATION IN INTERSTATE COMMERCE OR OF THE MAILS TO
SELL THROUGH THE USE OR MEDIUM OF ANY WRITTEN CONTRACT, OFFERING DOCUMENT,
PROSPECTUS, WHITEPAPER, OR OTHERWISE, ANY SECURITY AS TO WHICH NO REGISTRATION
STATEMENT WAS IN EFFECT. OR FOR THE PURPOSE OF SALE OR DELIVERY AFTER SALE,
CARRYING OR CAUSING TO BE CARRIED THROUGH THE MAILS OR IN INTERSTATE COMMERCE,
BY MEANS OR INSTRUMENTS OF TRANSPORTATION OR COMMUNICATION IN INTERSTATE
COMMERCE OR OF THE MAILS TO OFFER TO SELL OR OFFER TO BUY THROUGH THE USE OR 
MEDIUM OF ANY WRITTEN CONTRACT, OFFERING DOCUMENT, PROSPECTUS, WHITEPAPER,
OR OTHERWISE, SECURITIES AS TO WHICH NO REGISTRATION STATEMENT HAS BEEN FILED.

OUTSIDE OF THESE LEGAL REQUIREMENTS, THIS SOFTWARE IS PROVIDED "AS IS" AND 
THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING 
ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL 
THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL 
DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, 
WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, 
ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

