## Creating a wallet

Let's create our first wallet on the testnet.

```bash
> ./sushi wallet create -w testnet-wallet-1.json --testnet
```

The `-w` flag is used to specify the file location of the new wallet you want to create. In this instance it's going to be created in the local directory you are running the command from - but you can specify any location to generate it into to.

The `--testnet` flag is used to indicate that we want to create this wallet for use on the testnet. If we left this off - our wallet would be created using the default which is for mainnet.

We can also create an encrypted wallet - see the [encrypt/decrypt the wallet](#encrypt-decrypt-a-wallet) section for more details.

So now we have a wallet we can do a few things with it:

* [verify it's a valid wallet](#verify-the-wallet)
* [check the amount of coins we have in the wallet](#check-the-balance)
* [encrypt/decrypt the wallet](#encrypt-decrypt-a-wallet)

### Verify the wallet

```bash
> ./sushi wallet verify -w testnet-wallet-1.json
```

and we should see

```bash
testnet-wallet-1.json is perfect!
address: TTAzZDBlN2YwNTQ2MjI2YTVmMTA1ZjU4ZGQwMTgzNzQ4NTA3YTZhYjU4NjE0YWE1
network (T0): testnet
```

### Check the balance

```bash
> ./sushi wallet amount -w testnet-wallet-1.json -n http://testnet.sushichain.io:3000
```

Here we are checking the balance against the testnet - but you can supply the url of any node or even a locally running private node.

When you check the balance it shows the amount after 1 confirmation. You can choose to supply more confirmations. Then number of confirmations is the number of blocks that have been added to the chain after the block that contains your transaction. Obviously the more blocks the more confidence you have that the block your transaction is in and the chain your are looking at as a whole is good. In the context of wallet amount it's looking at the balance at `latest block - number_of_confirmations`

```bash
> ./sushi wallet amount -w testnet-wallet-1.json -n http://testnet.sushichain.io:3000 
```

This is checking the amount of coins that have been successfully processed on the testnet - It defaults to 1 confirmation (i.e. `latest block - 1`)

```bash
> ./sushi wallet amount --confirmation=6 -w testnet-wallet-1.json -n http://testnet.sushichain.io:3000
```

The `--confirmation=` flag indicates we want to see the amount of coins that are present when looking at the balance as of  `latest block - 6 blocks`. 

### Encrypt / Decrypt a wallet

We can also choose to encrypt an existing wallet, or decrypt and existing encrypted wallet. Also if we just want to always use an encrypted wallet we can create an encrypted wallet by adding the `-e` flag when creating the wallet.

All of the commands that require a wallet can also accept an encrypted wallet - you just have to either give the command the `--password=` flag or set the environment variable: `WALLET_PASSWORD`

#### Create an encrypted wallet

```bash
> ./sushi wallet create -w my-wallet.json -e --password=my-very-secure-password --testnet
```

#### Encrypt a wallet

```bash
> ./sushi wallet encrypt -w my-clear-text-wallet.json --password=my-very-secure-password
```

This creates an encrypted version of the wallet prefixed with `encrypted` along side the original

#### Decrypt a wallet

```bash
> ./sushi wallet decrypt -w my-encrypted-wallet.json --password=my-very-secure-password
```

This creates an unencrypted version of the wallet prefixed with `unencrypted` along side the original