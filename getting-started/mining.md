## Mining against the testnet

Now it's time to do some mining. For mining we use the `sushim` binary.

```bash
> ./sushim -w testnet-wallet-1.json --testnet -n http://testnet.sushichain.io:3000 --process=2
```

This is going to startup a miner that connects to the testnet node with 2 processes. We supply the wallet we want our rewards to go to with the `-w` flag. The `-n` flag is how we specify our connecting node - which in this case is the testnet node.

Leave the miner running for about 5-10 minutes and then let's have a look in our wallet.

```bash
> ./sushi wallet amount -w testnet-wallet-1.json -n http://testnet.sushichain.io:3000
```

If we look at the amount of coins you will see you will have something like 0.7 

Depending on when you look - you might see it still says 0.0 - but after mining for a while the transactions will be processed and the blocks added to the testnet and then you will see the balance start to increase.

```bash
> ./sushi wallet amount -w testnet-wallet-1.json -n http://testnet.sushichain.io:3000
```



## Mining against other nodes

You can mine against any node simply by passing in the node's url with the `-n` flag. For exaple you could startup a local private node that is connected to the public testnet and mine against the testnet via your local private node. In essence this is how mining pools work on SushiChain.

Let's try it:

Now we are going to start up a local node that we can use for mining and that will connect to the testnet

```bash
> ./sushid -w testnet-wallet-1.json --testnet -n http://testnet.sushichain.io:3000 --private
```

The `-n` flag is to specify the connecting node e.g. the public testnet address. The `--private` flag means we start a private local node - e.g. not available to others on the internet.

When the local node starts it syncs with the connecting node (testnet in this case) and brings down the latest blockchain. The mining process is the same as described for mining against the testnet above execpt you supply your local node using the `-n ` flag.

```bash
> ./sushim -w testnet-wallet-1.json --testnet -n http://127.0.0.1:3000 --process=2
```

