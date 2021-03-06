# Data transaction

Data transaction adds, modifies and deletes data entries in sender's [account data storage](/en/blockchain/account/account-data-storage).

> Entry deletion becomes available since node version 1.2.0, after activation of feature #15 “Ride V4, VRF, Protobuf, Failed transactions”.

Limitations are as follows:
* The maximum number of entries is 100.
* For a transaction version 2 the maximum data size (keys + values) is 165,890 bytes.
* For a transaction version 1 the maximum transaction size (except proofs) is 153,600 bytes.

## Fee

The minimum fee for a Data transaction is 0.001 WAVES per kilobyte, the fee value is rounded up to three decimals.

If the transaction sender is a [dApp](/en/blockchain/account/dapp) or a [smart account](/en/blockchain/account/smart-account), the minimum fee is increased by 0.004 WAVES.

## JSON Representation

```json
{
  "senderPublicKey": "38bYRUxFCaoa9h822nMnsoTX1qfczqtHJLgouNcNnd8h",
  "data": [
    {
      "type": "boolean",
      "value": true,
      "key": "bool"
    },
    {
      "type": "binary",
      "value": "base64:SGVsbG8gV2F2ZXM=",
      "key": "bin"
    },
    {
      "type": "integer",
      "value": 1234567,
      "key": "int"
    },
    {
      "type": "string",
      "value": "some text",
      "key": "str"
    }
  ],
  "sender": "3N4iKL6ikwxiL7yNvWQmw7rg3wGna8uL6LU",
  "feeAssetId": null,
  "proofs": ["kE1hjN1yW68j8DsYGNB7Gg1ydC4hqRmt3wBaFQUPkftnbiM7QfJCn1gTHgveJ7pCLXvvqffhKBmiF8qS1Uqk6SR"],
  "fee": 100000,
  "id": "3EPJuvQiJYiu9Y5g6mYDQgHVu8GFUfnZurHrVwwF1ViH",
  "type": 12,
  "version": 2,
  "timestamp": 1591351545000,
  "height": 1029815
}
```

| Field | Description |
| :--- | :--- |
| data.key | Entry key. String, up to 400 bytes for version 2, up to 100 characters for version 1 |
| data.type | Entry type:<br>- binary<br>- boolean<br>- integer<br>- string<br>`null` – delete entry |
| data.value | Entry value. Up to 32,767 bytes. Binary value is base64 encoded.<br>`null` – delete entry |

The fields that are common to all types of transactions are described in the [Transaction](/en/blockchain/transaction/#json-representation) article.

## Binary Format

See the [Data Transaction Binary Format](/en/blockchain/binary-format/transaction-binary-format/data-transaction-binary-format) article.

## Ride Structure

The [DataTransaction](/en/ride/structures/transaction-structures/data-transaction) structure is used for transaction handling in smart contracts.
