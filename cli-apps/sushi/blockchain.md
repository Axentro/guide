## Blockchain

The following actions are available for the blockchain action:

```reStructuredText
available sub actions
 - size                 | show current blockchain size
 - all                  | get whole blockchain. headers (without transactions) only with --header option
 - block                | get a block for a specified index or transaction id
```

### Size

This retreives the size of the chain on the node you are querying:

`axe blockchain size -n http://testnet.axentro.io:3000`

### All

This retrieves the whole blockchain as json

`axe blockchain all -n http://testnet.axentro.io:3000`

You can also retrieve only the headers (no transactions) with:

`axe blockchain all --header -n http://testnet.axentro.io:3000`

### Block

This retrieves a block containing either the specified transaction or by block index

`axe blockchain block -t 173914b8d56ebb503d0b94e56bbce160d4a4f12998fecfe6d77767d5d91c73f6 -n http://testnet.axentro.io:3000`

will return the block as json:

```json
show a block for transaction: 173914b8d56ebb503d0b94e56bbce160d4a4f12998fecfe6d77767d5d91c73f6
{
  "index": 1,
  "transactions": [{
    "id": "173914b8d56ebb503d0b94e56bbce160d4a4f12998fecfe6d77767d5d91c73f6",
    "action": "head",
    "senders": [],
    "recipients": [{
      "address": "VDBkNzU2ZTdiYTFmNDY3MTU3ZGFhNzVmMDExZDZiYmZlZjY1NGY4NDI1ZGY2YWZh",
      "amount": 50462650
    }],
    "message": "0",
    "token": "axe",
    "prev_hash": "0",
    "timestamp": 1555008570,
    "scaled": 1
  }],
  "nonce": -1328265420410860965,
  "prev_hash": "d1add9c421955537672297468788f8e9e173dce7949f5b2c347fe278469d9932",
  "merkle_tree_root": "fbbd73c7210bca6b67158cc0909ba31580663ee3",
  "timestamp": 1555008570,
  "next_difficulty": 9
}
```

`axe blockchain block -i 1 -n http://testnet.axentro.io:3000`

will return the block at index 1 in the chain as json:

```json
show a block for index: 1
{
  "index": 1,
  "transactions": [{
    "id": "173914b8d56ebb503d0b94e56bbce160d4a4f12998fecfe6d77767d5d91c73f6",
    "action": "head",
    "senders": [],
    "recipients": [{
      "address": "VDBkNzU2ZTdiYTFmNDY3MTU3ZGFhNzVmMDExZDZiYmZlZjY1NGY4NDI1ZGY2YWZh",
      "amount": 50462650
    }],
    "message": "0",
    "token": "AXE",
    "prev_hash": "0",
    "timestamp": 1555008570,
    "scaled": 1
  }],
  "nonce": -1328265420410860965,
  "prev_hash": "d1add9c421955537672297468788f8e9e173dce7949f5b2c347fe278469d9932",
  "merkle_tree_root": "fbbd73c7210bca6b67158cc0909ba31580663ee3",
  "timestamp": 1555008570,
  "next_difficulty": 9
}
```

