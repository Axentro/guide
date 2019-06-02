## Sushi - Blockchain Client

## Overview

The command line app `sushi` is a blockchain client and provides many useful capabilities for interation with a blockchain node.

The following actions are available:

```reStructuredText
available sub actions
 - wallet               | create, encrypt or decrypt your wallet (wt for short)
 - blockchain           | get a whole blockchain or each block (bc for short)
 - transaction          | get or create transactions (tx for short)
 - node                 | show information of nodes (nd for short)
 - scars                | SushiCon Address Resolution System (SCARS), buy/sell a readable domain for your address (sc for short)
 - token                | create tokens.
 - config               | save default configuration used by sushi, sushid and sushim (cg for short)
 - pubsub               | receive blocks in realtime
 - client               | connect to node as peer clients
```



## Wallet

The following actions are available for the wallet functions:

```reStructuredText
available sub actions
 - create               | create a wallet file
 - verify               | verify a wallet file
 - encrypt              | encrypt a sushi wallet
 - decrypt              | decrypt a sushi wallet (that was encrypted using sushi)
 - amount               | show remaining amount of Sushi tokens for specified address
```

### Create

This will create a new wallet

`sushi wallet create -w path/to/new-wallet.json --testnet`

You must supply the `-w` to indicate where the wallet should be created and the name of the wallet. The `--testnet` indicates you want the wallet to work on the testnet only. If youd omit this then the wallet will be created for the MainNet by default. The wallet is a json file which by default is unencrypted and contains information about the wallet:

```json
{
  "public_key": "041b09e3326e72d45810035cf43fefa399f1be00c5431b41d6e1bfb531c187d9d07114036dc1b0120e9289f8703ea253eb04debf639c87709b3bc9eee541a0c70f",
  "wif": "VDA0MmQyM2UyY2JkMjZjNmZjYWE2NDBiZTM2NjJkNjg3ZTA5NjU2MTI2ZGE5NWYwY2I0YWIyYzM3NDg5MzIwNDA2YzgyN2Zi",
  "address": "VDA2NjU5N2JlNDA3ZDk5Nzg4MGY2NjY5YjhhOTUwZTE2M2VmNjM5OWM2M2EyMWQz"
}
```

If you want to encrypt the wallet on creation you can supply `-e` and then `--password=` to generate a wallet that is encypted with the supplied password.

`sushi wallet create -w /path/to/new-wallet.json --testnet -e --password=super-password`

Here is an example of an encrypted wallet:

```json
{
  "source": "sushi",
  "ciphertext": "Y7UB7fyK3PxgH9ZEkQ7gi4XQeAHe3wxLGEr+DTM31TtFzmn6MyFsbGgRmsYBbKt/dnLgFV1B7FLQZc0KtLzNM9fLODXEMP9Xu00KZ1YvtDXVmDznRgSWh0lA/o2JPdbzU6JcOa03/GOC4Vjl7nlTfIBpxTNuMXoV/VANmkvu8ORR2QAcNAEQsYaBDvxFuvjlAFHUZLhQ6QpsACcXvbHaqwPKGsAYLVk2hV2oN99dFUNImX4Z5GHfphhhpDcKyLypJBIWxsPqSCj5TIeUk2565J8e6shUk09Uw0dwIJhqxsfaP+Na11vlh/dUt6P+I0jhrEqcNofXW+Ga4+UFTx5gnu5F8J0xzi7JD+lpSpUiestrZZWLHZe7QRjJWfcEdo76FFCu8Bb0ndQHXjJOeOaGqNt26UOZ86NI8Qi50gT6+tacLJAcvn9XdESTWhI2EKZt",
  "address": "VDAwNDA2NjZkM2I2MDZhZjMyOWZiNDc2Y2JkNjIwNjc2Zjc0NjBhM2EwZWNjZWRk",
  "salt": "9jZmkySR8z94Ta4sgrnEK."
}
```

When using an encrypted wallet with any of the CLI binaries you will have to supply the password either using `--password=password` or by setting the environment variable: `WALLET_PASSWORD`

### Amount

You can use this to find the amount of SUSHI and other tokens you have in your wallet:

`sushi wallet amount -w /path/to/wallet.json -n http://testnet.sushichain.io:3000`

```reStructuredText
  showing amount of each token for VDA2NjU5N2JlNDA3ZDk5Nzg4MGY2NjY5YjhhOTUwZTE2M2VmNjM5OWM2M2EyMWQz.
  confirmation: 1

  + -------------------- - -------------------- +
  |                token |               amount |
  | -------------------- | -------------------- |
  |                SUSHI |          82.50343166 |
  + -------------------- - -------------------- +
```



### Encrypt

You can use this to encrypt a wallet:

`sushi wallet encrypt -w /path/to/existing-unencrypted-wallet.json --password=some-password`

### Decrypt

You can use this to decrypt an encrypted wallet:

`sushi wallet decrypt -w /path/to/existing-encrypted-wallet.json --password=some-password`

### Verify

This can be used to check if you wallet is valid:

`sushi wallet verify -w /path/to/existing-wallet.json`

```reStructuredText
/Users/kings/sc-wallets/w1.json is perfect!
address: VDA2NjU5N2JlNDA3ZDk5Nzg4MGY2NjY5YjhhOTUwZTE2M2VmNjM5OWM2M2EyMWQz
network (T0): testnet
```







