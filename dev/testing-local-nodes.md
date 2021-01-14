# Setting up and testing local nodes

In order to test locally you can set up a number of nodes locally and connect them together to form a network.

Before you start you need to git clone the axento github repo and build the binaries as described in [Installing](/using-the-cli/install.md)

There are 2 things a node needs to start up:

* a wallet
* an official_nodes.yml
* a developer_fund.yml (not needed but very helpful for testing)

### Official nodes

When you start up a new chain and it writes the genesis block - you must anchor a set of addresses to the chain. At the moment these are fixed once written into the genesis block. There are 2 categories:

* fastnodes
* slownodes

The minimal config is putting your address in both like this:

```bash
vim official_nodes.yml
```

```yaml
fastnodes:
  - VDAyNThiOWFiN2Q5YWM3ZjUyYTNhYzQwZTY1NDBmYWJkMjczZmVmZThlOTgzMWM4
slownodes:
  - VDAyNThiOWFiN2Q5YWM3ZjUyYTNhYzQwZTY1NDBmYWJkMjczZmVmZThlOTgzMWM4
```

If there is not a node with an address that belongs to the official nodes then your nodes will all complain they are not connected to an official network. There is only 1 fast node possible at this time - so you should put only 1 fastnode entry.

Thn supply the official_nodes.yml file to the node on startup (you should also do the developer_fund at the same time as they both apply only to the genesis block)

```bash
axen -w your-wallet-address.json --testnet -u http://localhost:3000 -p 3000 -d my_db.sqlite3 --official-nodes=./official_nodes.yml --developer-fund=./developer_fund.yml
```

### Developer Fund

This allows you to specify a set of addresses to populate with instant tokens (you need to do both official_nodes and developer_fund at the same time as they both apply only to the genesis block)

```bash
vim developer_fund.yml
```

```yaml
addresses:
  - address: VDAyNThiOWFiN2Q5YWM3ZjUyYTNhYzQwZTY1NDBmYWJkMjczZmVmZThlOTgzMWM4
    amount: "9000000"
  - address: VDA4M2YwYTkzZTQxZTQ0NzdjOGRjMDU4ZTkwZTI4OWY1NDNkMDZjYmU3ODQyM2Rk
    amount: "9000000"
```
Thn supply the official_nodes.yml file to the node on startup

```bash
axen -w your-wallet-address.json --testnet -u http://localhost:3000 -p 3000 -d my_db.sqlite3 --official-nodes=./official_nodes.yml --developer-fund=./developer_fund.yml
```

### Running multiple nodes for testing

You can run multiple nodes for testing. If you specify a different address for fastnode and slownodes in the official_nodes config then you can also run a separate node for the fastnode and the other slownodes. Depending on what needs testing.

Start up several nodes connected to each other:

This node is standalone and not connected to a parent:

```bash
axen -w your-wallet-address-1.json --testnet -u http://localhost:3000 -p 3000 -d my_db_1.sqlite3
```

And now connect more nodes to it, or connect nodes to other nodes connected to it. The nodes form a big circle each with a predecessor node and a successor node following the Chord peer to peer networking protocol. So they are not connected in a hierachy but a circle - so it doesn't matter the order you connect the nodes to each other. 

It's best to put the nodes in a different folder each. This node connects to the first node

```bash
axen -w your-wallet-address-2.json --testnet -u http://localhost:3001 -p 3001 -d my_db_2.sqlite3 -n http://localhost:3000
```

```bash
axen -w your-wallet-address-3.json --testnet -u http://localhost:3002 -p 3002 -d my_db_2.sqlite3 -n http://localhost:3000
```

```bash
axen -w your-wallet-address-4.json --testnet -u http://localhost:3002 -p 3002 -d my_db_2.sqlite3 -n http://localhost:3000
```

Now you can start miners against one or more of the nodes e.g.

```
axem -w your-wallet.json --testnet -n http://localhost:3000 --process=2
```

or you can use the minaxnt miner for this too.

You can also import any of the wallets into the desktop wallet and change the config in the desktop wallet to point to any of the local nodes. Or you can use the cli client `axe` to send transactions or interact with the nodes.



