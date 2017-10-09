# Sendrawtransaction method

<<<<<<< HEAD
Broadcasting.

## Parameter Description

Hex: A hexadecimal string that has been serialized after the signed transaction in the program.

## Call the example
=======
Broadcasts a transaction over the NEO network. There are many kinds of transactions, as specified in the network protocol [documentation](../network-protocol.md).

## Parameter Description

Hex: A hexadecimal string that has been serialized, after the signed transaction in the program.

## Example
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359

Request text:

```json
{
<<<<<<< HEAD
  "Jsonrpc": "2.0",
  "Method": "sendrawtransaction",
  "Params": [ "80000001195876cb34364dc38b730077156c6bc3a7fc570044a66fbfeeea56f71327e8ab0000029b7cffdaa674beae0f930ebe6085af9093e5fe56b34a5c220ccdcf6efc336fc500c65eaf440000000f9a23e06f74cf86b8827a9108ec2e0f89ad956c9b7cffdaa674beae0f930ebe6085af9093e5fe56b34a5c220ccdcf6efc336fc50092e14b5e00000030aab52ad93f6ce17ca07fa88fc191828c58cb71014140915467ecd359684b2dc358024ca750609591aa731a0b309c7fb3cab5cd0836ad3992aa0a24da431f43b68883ea5651d548feb6bd3c8e16376e6e426f91f84c58232103322f35c7819267e721335948d385fae5be66e7ba8c748ac15467dcca0693692dac"],
  "Id": 1
=======
  "jsonrpc": "2.0",
  "method": "sendrawtransaction",
  "params": [ "80000001195876cb34364dc38b730077156c6bc3a7fc570044a66fbfeeea56f71327e8ab0000029b7cffdaa674beae0f930ebe6085af9093e5fe56b34a5c220ccdcf6efc336fc500c65eaf440000000f9a23e06f74cf86b8827a9108ec2e0f89ad956c9b7cffdaa674beae0f930ebe6085af9093e5fe56b34a5c220ccdcf6efc336fc50092e14b5e00000030aab52ad93f6ce17ca07fa88fc191828c58cb71014140915467ecd359684b2dc358024ca750609591aa731a0b309c7fb3cab5cd0836ad3992aa0a24da431f43b68883ea5651d548feb6bd3c8e16376e6e426f91f84c58232103322f35c7819267e721335948d385fae5be66e7ba8c748ac15467dcca0693692dac"],
  "id": 1
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
}
```

Response text:

```json
{
<<<<<<< HEAD
  "Jsonrpc": "2.0",
  "Id": 1,
  "Result": false
=======
  "jsonrpc": "2.0",
  "id": 1,
  "result": false
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
}
```

Response Description:

<<<<<<< HEAD
When the result is true that the current transaction broadcast success,

When result is false, the current transaction broadcast failure, the reasons may have a double cost, incomplete signature and so on.

In this example, a confirmed transaction was broadcast, because the double cost so the broadcast failed.
=======
When the result is true, the current transaction has been successfully broadcasted to the network.

When result is false, the current transaction has failed to broadcast. There are many reasons for this, such as double spend, incomplete signature, etc.

In this example, a confirmed transaction was already broadcasted, so the second broadcast failed due to double spend.
>>>>>>> e5e43331cd35f87f336ded6b98df4277306e0359
