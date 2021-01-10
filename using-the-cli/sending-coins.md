# Sending Coins

Ok so now we have some coins - what can we do with them? Well we could send them to someone else!

create a second wallet:

```bash
> ./axe wallet create -w testnet-wallet-2.json --testnet
> cat testnet-wallet-2.json
```

the `cat` command will show you the contents of the wallet including the address field. copy and paste the address field so you can use it to send coins to.

```bash
> ./axe transaction create -f 0.0001 -m 2 -a VDA3NmZkZmQ5MTQyNjgwZGQ4ZDYzYjA1MjA4NjAxYjg1OWVlMWYyMmJkNTcxMWQ2 -w testnet-wallet-1.json -n http://testnet.axentro.io
```

* The `-f` flag is the fee - every transaction has a fee - sending coins has a minimum fee of 0.0001 AXNT.
* The `-m` flag is the amount of coins to send - here we said 2 coins.
* The `-a` flag is the address we want to send to \(the address from our second wallet we created above\)

Now when you check the first wallet's amount you will see it is 2 coins \(plus the fee\) less than it was before. Everytime you send some coins the sender gets charged a small fee.

Have a look at the coins for wallet1:

```bash
> ./axe wallet amount -w testnet-wallet-1.json -n http://testnet.axentro.io
```

Now have a look at the coins for wallet2:

```bash
> ./axe wallet amount -w testnet-wallet-2.json -n http://testnet.axentro.io
```

You will see wallet2 now has 2 coins in it.

We can see the fees here:

```bash
> ./axe transaction fees
```

Currently it costs 0.0001 coin per `send` transaction

