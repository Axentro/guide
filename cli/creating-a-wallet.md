## Creating a wallet

Let's create our first wallet on the testnet.

```bash
> ./axe wallet create -w testnet-wallet-1.json --testnet
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
> ./axe wallet verify -w testnet-wallet-1.json
```

and we should see

```bash
testnet-wallet-1.json is perfect!
address: VDBkMzRmOWZlYWEwYmM4OWY4MjZhNDlmZThhNTY1MmI3NzZjYTNkZjVlNzYzMjZi
network (T0): testnet
```

### Check the balance

```bash
> ./axe wallet amount -w testnet-wallet-1.json -n http://testnet.axentro.io
```

Here we are checking the balance against the testnet - but you can supply the url of any node or even a locally running private node.

When you check the balance it shows the amount of confirmations. This is the number of blocks ontop of the block that contains the latest transaction that affects your wallet balance. In an active wallet e.g. used in mining - it will most likely always be 0 as new transactions are constantly arriving. But for less active wallets the number will vary depending on when the last transaction was.

```bash
> ./axe wallet amount -w testnet-wallet-1.json -n http://testnet.axentro.io 
```

### Encrypt / Decrypt a wallet

We can also choose to encrypt an existing wallet, or decrypt and existing encrypted wallet. Also if we just want to always use an encrypted wallet we can create an encrypted wallet by adding the `-e` flag when creating the wallet.

All of the commands that require a wallet can also accept an encrypted wallet - you just have to either give the command the `--password=` flag or set the environment variable: `WALLET_PASSWORD`

#### Create an encrypted wallet

```bash
> ./axe wallet create -w my-wallet.json -e --password=my-very-secure-password --testnet
```

#### Encrypt a wallet

```bash
> ./axe wallet encrypt -w my-clear-text-wallet.json --password=my-very-secure-password
```

This creates an encrypted version of the wallet prefixed with `encrypted` along side the original

#### Decrypt a wallet

```bash
> ./axe wallet decrypt -w my-encrypted-wallet.json --password=my-very-secure-password
```

This creates an unencrypted version of the wallet prefixed with `unencrypted` along side the original