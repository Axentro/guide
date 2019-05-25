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

Here we are checking the balance against the testnet - but in the next section we will start up a private local node and use that.

When you check the balance it shows the amount after 1 confirmation. You can choose to supply more confirmations. Each confirmation means that there was 1 block added to the blockchain above the one your last transaction was in. Obviously the more blocks the more confidence you have that the block your transaction is in and the chain your are looking at as a whole is good.

```bash
> ./sushi wallet amount -w testnet-wallet-1.json -n http://testnet.sushichain.io:3000 
```

This is checking the actual amount of coins that have been confirmed (successfully processed on the testnet) - It defaults to showing after 1 confirmation.

```bash
> ./sushi wallet amount --confirmation=6 -w testnet-wallet-1.json -n http://testnet.sushichain.io:3000
```

The `--confirmation=` flag indicates we want to see the confirmed amount of coins after 6 confirmations (or blocks) have been added on top of the block our last transaction is in

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