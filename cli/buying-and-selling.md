## Buying and selling domains

In the previous part of this guide we saw how to buy a domain (for a price of 0) from the platform. But we can also buy from someone who has put their domain up for sale. 

To see what is up for sale:

```
> ./axe scars sales -n http://testnet.axentro.io:3000

SCARS domains for sale!

 Domain     | Address        | Price
 awesome.ax | VDAxNmM1OGV... | 5
```

Buying a domain is exactly the same as in the first part of this guide except you must specify the price correctly:

```bash
> ./axe scars buy -w testnet-wallet-1.json -n http://testnet.axentro.io:3000 -f 0.001 --price=5 --domain=awesome.ax
```

Follow the same procedure of checking the transaction and confirmations.

Selling a domain is also easy:

```bash
> ./axe scars sell -w testnet-wallet-1.json -n http://testnet.axentro.io:3000 -f 0.0001 --price=8 --domain=mydomain.ax
```

and if you change your mind before someone else buys it you can cancel the sell:

```bash
> /axe scars cancel -w testnet-wallet-1.json -n http://testnet.axentro.io:3000 -f 0.0001 --domain=mydomain.ax
```

Remember to pay the correct fees when doing all these transactions.

