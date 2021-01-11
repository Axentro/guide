# Signing and Sending Transactions

In order to send tokens from your address to another address using the API there are a few steps described below:

  * generate an unsigned transaction json
  * sign the generated unsigned transaction json
  * post the json to the transaction endpoint

## Generating an unsigned transaction json

The first step is to use the API endpoint: [https://mainnet.axentro.io/api/v1/transaction/send_token/unsigned](https://mainnet.axentro.io/api/v1/transaction/send_token/unsigned) by making a POST request with the json for the transaction:

```json
{
 "from_address": "VDBkYWQxZjZlZjllOTAzYzNiODQ0NmZkZTI4NDBhYmMzYjUxYThjM2E1ZjNkODlj",
 "public_key": "48c45b7e45cd415187216452fa22523e002ca042c2bd7205484f29201c3d5806f90e7aeebad37e3fbe01286c25d4027d3f3fec7b5647eff33c07ebd287b57242",
 "amount": "10",
 "fee": "0.0001", 
 "to_address": "VDBlY2I4ZjA5MTUxOWE0MTIwNTRmZjlhYTM1YjYxMjcwNjM1YzcxYjlkMDZhZDUx", 
 "kind": "FAST"
}
```
You can get this information from your wallet. If you use the desktop wallet you can go to tools backup and it will produce a backup json that has this information. If you created your wallet using the cli tool `axe` then it produces the same json as the desktop wallet.

for example given this wallet json:

```json
{
 "public_key":"8b3c61787fb6b07bb20e4a908deca52ef96335e4faaaaca18a227f9d674dcc57",
 "wif":"VDBhMjY5YzE4NzA1YmY4MTRiMmE2Y2I2NGY1NjllMjdmMzAzMDIwMmMwZTZkNDczNjBlM2M5OGNkZWMzNmUwODY1OTNkMjdi",
 "address":"VDAyNThiOWFiN2Q5YWM3ZjUyYTNhYzQwZTY1NDBmYWJkMjczZmVmZThlOTgzMWM4"
}
```

You can see the `address` and `public_key` needed for the POST request mentioned above. 

  * It is recommened to use FAST for the kind - this is the transaction kind and fast transactions are instant
  * the fee for sending a transaction is 0.0001 - The API has an endpoint that lists the fees

So now you can make a POST request to the endpoint `https://mainnet.axentro.io/api/v1/transaction/send_token/unsigned` with the json mentioned above as the payload.

The request will return a response with a transaction json that you can sign and POST to make the actual transaction.

## Signing the generated transaction json

The json returned from the `api/v1/transaction/send_token/unsigned` endpoint should look similar to this:

```json
{
  "status": "success",
  "result": 
    {
      "id": "8069e6049f7175229f8e05e5cf4cd5dacbc82cad08bfbd251408b6e980d90b04",
      "action": "send",
      "senders": 
        [
          {
            "address": "VDBkYWQxZjZlZjllOTAzYzNiODQ0NmZkZTI4NDBhYmMzYjUxYThjM2E1ZjNkODlj",
            "public_key": "48c45b7e45cd415187216452fa22523e002ca042c2bd7205484f29201c3d5806f90e7aeebad37e3fbe01286c25d4027d3f3fec7b5647eff33c07ebd287b57242",
            "amount": 500000000000,
            "fee": 100000000,
            "signature": "0"
          }
        ],
      "recipients": 
        [
          {
            "address": "VDBlY2I4ZjA5MTUxOWE0MTIwNTRmZjlhYTM1YjYxMjcwNjM1YzcxYjlkMDZhZDUx",
            "amount": 500000000000
          }
        ],
      "message": "",
      "token": "AXNT",
      "prev_hash": "0",
      "timestamp": 1529781499,
      "scaled": 1,
      "kind": "FAST",
      "version": "V1"
    }
}
```

You need to first remove all the line breaks and all the spaces between the json properties so that it looks like this:

```json
{"id":"8069e6049f7175229f8e05e5cf4cd5dacbc82cad08bfbd251408b6e980d90b04","action":"send","senders":[{"address":"VDBkYWQxZjZlZjllOTAzYzNiODQ0NmZkZTI4NDBhYmMzYjUxYThjM2E1ZjNkODlj","public_key":"48c45b7e45cd415187216452fa22523e002ca042c2bd7205484f29201c3d5806f90e7aeebad37e3fbe01286c25d4027d3f3fec7b5647eff33c07ebd287b57242","amount":500000000000,"fee":100000000,"signature":"0"}],"recipients":[{"address":"VDBlY2I4ZjA5MTUxOWE0MTIwNTRmZjlhYTM1YjYxMjcwNjM1YzcxYjlkMDZhZDUx","amount":500000000000}],"message":"","token":"AXNT","prev_hash":"0","timestamp":1529781499,"scaled":1,"kind":"FAST","version":"V1"}
```

Remove the surounding json for status and result and just take the payload in the result so you have just the payload of the json with all spaces and new lines removed. If you get this wrong the hash will not match and the transaction will be rejected with invalid signing.

Next you need turn the json above into a `SHA256` hash and then sign it with your private key that you must convert from your WIF from your wallet json.

### Getting a SHA256

The following example is using Javascript using the `crypto-js` package [crypto-js](https://github.com/brix/crypto-js)

```javascript
  var SHA256 = require("crypto-js/sha256");
  var transaction_hash = SHA256('compact_json_string_with_no_spaces_or_new_lines')
```

### Getting your private key from the WIF

In your wallet json next to the public key and address there is a wif. This is a wallet information format key that has the private key inside that is needed for signing.

Here is a function that would acheive this using the Javascript `base64` package [base64](https://github.com/dankogai/js-base64#readme)

```javascript
var getPrivateKeyAndNetworkFromWif = function(wif) {
  var decodedWif = all_crypto.base64.Base64.decode(wif);
  var networkPrefix = decodedWif.substring(0, 1);
  var network = networkPrefix === "M0" ? mainnet : testnet;
  var privateKeyHex = decodedWif.substring(2, decodedWif.length - 6);
  return {
    privateKey: privateKeyHex,
    network: network
  };
};
```

### Signing the transaction hash

Next sign the transaction hash with your private key. This example uses the ED25519 Javascript package `elliptic` [Elliptic](https://github.com/indutny/elliptic)

```javascript
var sign = function(privateKey, message) {
  var ec = new all_crypto.elliptic.eddsa('ed25519');
  var key = ec.keyFromSecret(privateKey);
  var signature = key.sign(all_crypto.buffer.Buffer.from(message, 'utf8')).toHex().toLowerCase();
  return signature;
};
```

The private key is the one you got from the WIF and the message is the transaction_hash you made earlier. This funciton produces a signature which you then paste into the signature field of the `sender` in the compact json and post to the transaction endpoint `http://mainnet.axentro.io/api/v1/transaction` with the payload wrapped in a `transaction` elements as follows:

```json
{"transaction":{"id":"8069e6049f7175229f8e05e5cf4cd5dacbc82cad08bfbd251408b6e980d90b04","action":"send","senders":[{"address":"VDBkYWQxZjZlZjllOTAzYzNiODQ0NmZkZTI4NDBhYmMzYjUxYThjM2E1ZjNkODlj","public_key":"48c45b7e45cd415187216452fa22523e002ca042c2bd7205484f29201c3d5806f90e7aeebad37e3fbe01286c25d4027d3f3fec7b5647eff33c07ebd287b57242","amount":500000000000,"fee":100000000,"signature":"SIGNATURE_GOES_HERE"}],"recipients":[{"address":"VDBlY2I4ZjA5MTUxOWE0MTIwNTRmZjlhYTM1YjYxMjcwNjM1YzcxYjlkMDZhZDUx","amount":500000000000}],"message":"","token":"AXNT",}"prev_hash":"0","timestamp":1529781499,"scaled":1,"kind":"FAST","version":"V1"}
```

This json payload does not need to be compacted and can have spaces and line breaks.


