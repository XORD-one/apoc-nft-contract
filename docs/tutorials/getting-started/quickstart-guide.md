# Casper NFT Quick Start Guide

This quick start guide introduces you to the Casper client commands and Wasm files necessary to deploy a CEP-78 Casper Enhanced NFT contract to the [Casper Testnet](https://testnet.cspr.live/). To execute transactions on a Casper network involving NFTs, you will need some CSPR tokens to pay for the transactions. The Testnet provides test tokens using a [faucet](https://docs.casper.network/users/testnet-faucet/).

For greater detail into the creation and mechanics of the Casper NFT contract, see the complete [Casper NFT Tutorial](./full-installation-tutorial.md).

## Prerequisites

Before using this guide, ensure you meet the following requirements:

- Set up the [development prerequisites](https://docs.casper.network/developers/prerequisites/), including the [Casper client](https://docs.casper.network/developers/prerequisites/#install-casper-client)
- Get a valid [node address](https://docs.casper.network/developers/prerequisites/#acquire-node-address-from-network-peers) from the network
- Know how to install a [smart contract](https://docs.casper.network/developers/cli/sending-deploys/) on a Casper network
- Hold enough CSPR tokens to pay for transactions

## Setup

Clone the Casper NFT (CEP-78) [contract repository](https://github.com/casper-ecosystem/cep-78-enhanced-nft/).

```bash
git clone https://github.com/casper-ecosystem/cep-78-enhanced-nft/ && cd cep-78-enhanced-nft
```

Run the following commands to build the `contract.wasm` in the `contract/target/wasm32-unknown-unknown/release` directory and run the tests.

```bash
make prepare
make test
```

The output of the command would end with the following message:

```bash
test result: ok. 159 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 15.33s
```

## Installing the NFT Contract

The following command will install a sample NFT contract on the Testnet:

```bash
casper-client put-deploy --node-address http://localhost:11101/rpc/ \
--chain-name "casper-net-1" \
--payment-amount 5000000000 \
--secret-key ~/casper/casper-node/utils/nctl/assets/net-1/nodes/node-1/keys/secret_key.pem \
--session-path contract/target/wasm32-unknown-unknown/release/contract.wasm \
--session-arg "collection_name:string='CEP-78-collection'" \
--session-arg "collection_symbol:string='CEP78'" \
--session-arg "total_token_supply:u64='100'" \
--session-arg "ownership_mode:u8='2'" \
--session-arg "nft_kind:u8='1'" \
--session-arg "nft_metadata_kind:u8='0'" \
--session-arg "json_schema:string='nft-schema'" \
--session-arg "identifier_mode:u8='0'" \
--session-arg "metadata_mutability:u8='0'"
```

## Next Steps

Learn to query the contract, perform token transfers, set up approvals, and understand the testing framework.

- [Query](./querying-NFTs.md) the NTF Contract
- Learn to [Mint, Transfer, and Burn](./interacting-with-NFTs.md) NFT tokens
- Review the [Tests](./testing-NFTs.md)