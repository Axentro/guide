# Registering a domain

Since registering a domain is free you can easily do this from the `axe` command line client. Lets see an example:

* First create a wallet \(if you already have one you can skip this step\) on the testnet

```bash
> ./axe wallet create -w testnet-wallet-1.json --testnet
```

* Let's check the fees so we know the amount we need to specify

```text
> ./axe transaction fees -n http://testnet.axentro.io

  + ------------------------------ - ------------------------------ +
  |                         action |                            fee |
  | ------------------------------ | ------------------------------ |
  |                           send |                         0.0001 |
  |                        hra_buy |                          0.001 |
  |                       hra_sell |                         0.0001 |
  |                     hra_cancel |                         0.0001 |
  |                   create_token |                             10 |
  + ------------------------------ - ------------------------------ +
```

As you can see the fee for buying a domain is `0.001` so with a new wallet we will need to do a bit of mining to generate some coins we can use. So let's fire up a miner against the testnet:

```bash
> ./axem -w testnet-wallet-1.json --testnet -n http://testnet.axentro.io --process=2
```

Keep checking your wallet and when you have some coins in your wallet then you are ready to keep going \(it could take about 10-15 mins\):

```bash
> ./axe wallet amount -w testnet-wallet-1.json -n http://testnet.axentro.io
```

* Now lets create a domain for the wallet \(the fee is 0.001\) - and just set the price to 0

```bash
> ./axe hra buy -w testnet-wallet-1.json -n http://testnet.axentro.io -f 0.001 --price=0 --domain=mydomain.ax
```

If it was successful you will get a success message that includes a transaction id - once this transaction is processed the domain will be available. So we can check the transaction id to see if it's been processed:

```bash
> ./axe transaction transaction -n http://testnet.axentro.io -t dd49e07900bf0187c97acce175422231f2983f0b5b8f6a7cd6aaf885c4728d76
```

after a while the transaction will be processed and you will see a result saying the transaction was found.

Once it reports that the transaction has been processed we can check the domain can be resolved and if all is good we can start using it:

```bash
> ./axe hra resolve -n http://testnet.axentro.io --domain=mydomain.ax

show information of domain fullmetal.ax
resolved : true
address  : VDA4NTAxMzI1NmExZmY0ZTVkMGRjMGU4MGE0MWZlZThmYjNlZGYwYTAzMjYzYTI4
status   : acquired
price    : 0
```

