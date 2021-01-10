## Registering a domain

Since registering a domain is free you can easily do this from the `axe` command line client. Lets see an example:

* First create a wallet (if you already have one you can skip this step) on the testnet

```bash
> ./axe wallet create -w testnet-wallet-1.json --testnet
```

* Let's check the fees so we know the amount we need to specify

```
> ./axe transaction fees -n http://testnet.axentro.io:3000

  + ------------------------------ - ------------------------------ +
  |                         action |                            fee |
  | ------------------------------ | ------------------------------ |
  |                           send |                         0.0001 |
  |                      scars_buy |                          0.001 |
  |                     scars_sell |                         0.0001 |
  |                   scars_cancel |                         0.0001 |
  |                   create_token |                            0.1 |
  + ------------------------------ - ------------------------------ +
```

As you can see the fee for buying a domain is `0.001` so with a new wallet we will need to do a bit of mining to generate some coins we can use. So let's fire up a miner against the testnet:

```bash
> ./axem -w testnet-wallet-1.json --testnet -n http://testnet.axentro.io:3000 --process=2
```

Keep checking your wallet and when you have some coins in your wallet then you are ready to keep going (it could take about 10-15 mins):

```bash
> ./axe wallet amount -w testnet-wallet-1.json -n http://testnet.axentro.io:3000
```

* Now lets create a domain for the wallet (the fee is 0.001) - and just set the price to 0

```bash
> ./axe scars buy -w testnet-wallet-1.json -n http://testnet.axentro.io:3000 -f 0.001 --price=0 --domain=mydomain.ax 
```

If it was successful you will get a success message that includes a transaction id - once this transaction is processed the domain will be available. So we can check the transaction id to see if it's been processed:

```bash
> ./axe transaction transaction -n http://testnet.axentro.io:3000 -t dd49e07900bf0187c97acce175422231f2983f0b5b8f6a7cd6aaf885c4728d76
```

after a while the transaction will be processed and you will see a result saying the transaction was found. However this just means that the transaction was processed - the domain is not yet available for use - we have to wait until the block with our transaction in it has been minted - which could take a while - so the next thing to check is the number of confirmations:

```bash
> ./axe transaction confirmation -n http://testnet.axentro.io:3000 -t dd49e07900bf0187c97acce175422231f2983f0b5b8f6a7cd6aaf885c4728d76

show the number of confirmations
transaction id: dd49e07900bf0187c97acce175422231f2983f0b5b8f6a7cd6aaf885c4728d76
--------------
confirmations: 1
```

Once it reports that the transaction has at least 1 confirmation we can check the domain can be resolved and if all is good we can start using it:

```bash
> ./axe scars resolve -n http://testnet.axentro.io:3000 --domain=mydomain.ax

show information of domain fullmetal.ax
resolved : true
address  : VDA4NTAxMzI1NmExZmY0ZTVkMGRjMGU4MGE0MWZlZThmYjNlZGYwYTAzMjYzYTI4
status   : acquired
price    : 0
```