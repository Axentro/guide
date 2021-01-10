## Mining against the testnet

Now it's time to do some mining. For mining we use the `axem` binary.

```bash
> ./axem -w testnet-wallet-1.json --testnet -n http://testnet.axentro.io --process=2
```

This is going to startup a miner that connects to the testnet node with 2 processes. We supply the wallet we want our rewards to go to with the `-w` flag. The `-n` flag is how we specify our connecting node - which in this case is the testnet node.

Leave the miner running for about 2-3 minutes and then let's have a look in our wallet.

```bash
> ./axe wallet amount -w testnet-wallet-1.json -n http://testnet.axentro.io
```

If we look at the amount of coins you will see you will have something like 0.7 

Depending on when you look - you might see it still says 0.0 - but after mining for a while the transactions will be processed and the blocks added to the testnet and then you will see the balance start to increase.

```bash
> ./axe wallet amount -w testnet-wallet-1.json -n http://testnet.axentro.io
```

## Mining against other nodes

You can mine against any node simply by passing in the node's url with the `-n` flag. For example you could startup a public node that is connected to the public testnet and mine against the testnet via your public node. In essence this is how mining pools work on Axentro.

More information will be provided on running public nodes in the near future

## Rewards

The main motivation for mining is to receive rewards. When a new block is mined the total payout is `0.5 AXNT`. The node on which the block was mined always receives `25%` of the total payout and all the miners connected to the node receive a prorated amount depending on how many hashes each miner has worked through.

For example a single miner on the network would expect to receive the full `75%` of the block reward. Three miners all working at approximately the same hash rate would receive `25%` each. In some cases if there are a great many miners connected to the node and some of them have an insignificant hash rate compared to the majority then they will not receive any reward.