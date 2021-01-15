# Crypto

This document outlines the crypto we use to make keypairs, wallets and addresses. We use the ED25519 curve in Axentro.

The following examples are written in Javascript and use these libraries:

* `tweetnacl` package [tweetnacl](https://github.com/dchest/tweetnacl-js)
* `crypto-js` package [crypto-js](https://github.com/brix/crypto-js)
* `base64` package [base64](https://github.com/dankogai/js-base64#readme)

## Creating a keypair

```javascript
var generateValidKeyPair = function myself() {
  var nacl = all_crypto.tweetnacl;
  var keyPair = nacl.sign.keyPair();
  var fullPrivateKey = toHexString(keyPair.secretKey);
  var publicKey = toHexString(keyPair.publicKey);
  var privateKey = fullPrivateKey.replace(publicKey, "");

  return {
    hexPrivateKey: privateKey,
    hexPublicKey: publicKey
  };
};

function toHexString(byteArray) {
  return Array.prototype.map.call(byteArray, function(byte) {
    return ('0' + (byte & 0xFF).toString(16)).slice(-2);
  }).join('');
}
```

## Network Prefix

The network prefix is added to the address to make the final walle address and can be either:

* Mainnet network prefix is: `M0`
* Testnet network prefix is: `T0`

## Creating a wallet address

Once you have a keypair you can use the public key and the network prefix to make a wallet address:

```javascript
var makeAddress = function(publicKey, networkPrefix) {
  var hashedAddress = all_crypto.cryptojs.RIPEMD160(all_crypto.cryptojs.SHA256(publicKey).toString()).toString();
  var networkAddress = networkPrefix + hashedAddress;
  var hashedAddressAgain = all_crypto.cryptojs.SHA256(all_crypto.cryptojs.SHA256(networkAddress).toString()).toString();
  var checksum = hashedAddressAgain.substring(0, 6);
  return all_crypto.base64.Base64.encode(networkAddress + checksum);
};
```

## WIF (Wallet Information Format)

In the Axentro standard wallet format we put the private key in WIF format. You can build the WIF like this:

```javascript
var makeWif = function(privateKey, networkPrefix) {
  var networkKey = networkPrefix + privateKey;
  var hashedKey = all_crypto.cryptojs.SHA256(all_crypto.cryptojs.SHA256(networkKey).toString()).toString();
  var checksum = hashedKey.substring(0, 6);
  return all_crypto.base64.Base64.encode(networkKey + checksum);
};
```

## Getting items out

From a WIF we can get the private key and network type:

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

From a private key we can get the public key 

```javascript
var getPublicKeyFromPrivateKey = function(privateKey) {
  var ec = new all_crypto.elliptic.eddsa('ed25519');
  var key = ec.keyFromSecret(privateKey);
  var publicKey = toHexString(key.getPublic());
  return publicKey;
};
```