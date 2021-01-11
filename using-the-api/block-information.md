# API Overview

You can read the full API documentation here:

* [TestNet API Documentation](https://testnet.axentro.io)
* [MainNet API Documentation](https://mainnet.axentro.io)

The API has many endpoints for retreiving various information about the blockchain but the most common questions are listed below with which API's to use: (links are for the mainnet version)

Most of the API's are paginated when returning lots of data.

## Get the balance of an address

The wallet adddress API endpoint returns the wallet balances along with the most 50 recent transactions.

* [api/v1/wallet/_address_](http://mainnet.axentro.io/#/get~wallet~address)

The token amount API endpoint returns the balance for a specified token in the specified wallet

* [api/v1/address/{address}/token/{token}](http://mainnet.axentro.io/#/get~address~address~token~token)

## Getting a specific transaction detail

Transaction detail for a specific transaction can be found using the transaction API

* [api/v1/transaction/{transaction_id}](http://mainnet.axentro.io/#/get~transaction~id)

## Getting a list of transactions

You can also find a list of transactions for the following:

* All transactions [api/v1/transactions](http://mainnet.axentro.io/#/get~transactions)
* Transactions for a block [/api/v1/block/](http://mainnet.axentro.io/#/get~block~index~transactions)



