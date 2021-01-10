## Using the domain

So now you have a domain - you can do a few things:

* receive coins/token to the domain
* query the wallet amounts via the domain
* sell the domain for profit

Let's try to receive some coins to our wallet via the domain

### Sending coins to the domain

You will need another wallet to be able to send coins to your wallet with the domain. If you don't have another one - go and follow the instructions to [create and populate a wallet](getting-started/creating-a-wallet) with some coins and [sending coins](getting-started/sending-coins).

So firstly lets see how many unconfirmed coins our wallet with the domain has:

```
> ./axe wallet amount --domain=mydomain.ax -n http://testnet.axentro.io

 showing amount of each token for VDA4NTAxMzI1NmExZmY0ZTVkMGRjMGU4MGE0MWZlZThmYjNlZGYwYTAzMjYzYTI4.
 confirmation: 1

  + -------------------- - -------------------- +
  |                token |               amount |
  | -------------------- | -------------------- |
  |                 AXNT |          59.29161346 |
  + -------------------- - -------------------- +
```

and now lets send some coins to the wallet with the domain:

```bash
./axe transaction create -w testnet-wallet-2.json -n http://testnet.axentro.io -m 2 -f 1 --domain=fullmetal.ax
```

So now once the transaction has been processed we should see the amount of coins in `mydomain.ax` increase by 2.

```
> ./axe wallet amount --domain=mydomain.ax -n http://testnet.axentro.io

 showing amount of each token for VDA4NTAxMzI1NmExZmY0ZTVkMGRjMGU4MGE0MWZlZThmYjNlZGYwYTAzMjYzYTI4.

  + -------------------- - -------------------- +
  |                token |               amount |
  | -------------------- | -------------------- |
  |                 AXNT |          61.29161346 |
  + -------------------- - -------------------- +
```