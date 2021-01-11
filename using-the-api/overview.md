# API Overview

You can read the full API documentation here:

* [TestNet API Documentation](https://testnet.axentro.io)
* [MainNet API Documentation](https://mainnet.axentro.io)

The API has many endpoints for retreiving various information about the blockchain but the most common questions are listed below with which API's to use: (links are for the mainnet version)

Most of the API's are paginated when returning lots of data.

## Get the balance of an address

The wallet adddress API endpoint returns the wallet balances along with the most 50 recent transactions.

* [api/v1/wallet/{**address**}](https://mainnet.axentro.io/#/get~wallet~address)

The token amount API endpoint returns the balance for a specified token in the specified wallet

* [api/v1/address/{**address**}/token/{**token**}](https://mainnet.axentro.io/#/get~address~address~token~token)

## Getting a specific transaction detail

Transaction detail for a specific transaction can be found using the transaction API

* [api/v1/transaction/{**transaction_id**}](https://mainnet.axentro.io/#/get~transaction~id)

## Getting a list of transactions

You can also find a list of transactions for the following:

* All transactions [api/v1/transactions](https://mainnet.axentro.io/#/get~transactions)
* Transactions for a block [/api/v1/block/{**index**}/transactions](https://mainnet.axentro.io/#/get~block~index~transactions)
* Transactions for an address [/api/v1/address/{**address**}/transactions](https://mainnet.axentro.io/#/get~address~address~transactions)
* Transactions for a domain [/api/v1/domain/{**domain**}/transactions](https://mainnet.axentro.io/#/get~domain~domain~transactions)

## Confirmations & Transaction Speed

Most of the API responses for blocks and transactions also return the number of confirmations. This is the number of blocks that are ontop of the block that contains your transaction. The number of confirmation required to be confident in the chain depends on whether the transaction was send via FAST transaction or SLOW transaction.

SLOW transactions are included in the block that the miners mine and will take approximately 2 minutes to be mined. FAST transactions are send instantly as a new FAST block is minted every 2 seconds on demand. Therefore for FAST transactions confirmations are not applicable because FAST transactions are written into FAST blocks which are guaranteed to be written into the chain.

When sending transactions it's recommended to use FAST transactions.

* Confirmations for SLOW transacations: 7 
* Confirmations for FAST transactions: 0

## Signing and Sending Transactions

Please see the [Signing and Sending Transactions](/using-the-api/signing-and-sending-transactions.md) page for detailed information.